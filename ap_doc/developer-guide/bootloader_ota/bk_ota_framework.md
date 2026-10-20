---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/developer-guide/bootloader_ota/bk_ota_framework.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: AP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="ota"></a>

# OTA 公共框架

<a id="id1"></a>

## 源码与编译开关

AP OTA 组件在 `ap/components/ota`：

| 文件 | 职责 |
| --- | --- |
| `ota.c` | 会话生命周期：`ota_do_init_operation()` 按 Kconfig 挂接后端；`bk_ota_finish_and_reboot()` 调 `finish` 后重启 |
| `ota_nosecurity/ota_http.c` | HTTP 传输：`bk_http_ota_download()` 调 `httpclient_common()`，下载期间关闭 STA PS |
| `ota_nosecurity/ota_https.c` | HTTPS 传输 |
| `ota_base_drv.c` | **默认非安全后端**：按 1KB 缓冲写 Flash，进度 `cyg_recvlen_per` |
| `ota_secure_overwrite.c` | 安全 Overwrite 后端 |
| `ota_secure_xip.c` / `ota_boot_param.c` | 安全 XIP 后端 \+ `boot_param` TRIAL 写入 |
| `ota_common.c` | 当前槽位读取、非安全 AB 标志、HTTP 回调分发 |
| `ota_test.c` | CLI：`http_ota` / `http_new_ota` / `ab_version` |

后端选择发生在 `ota_do_init_operation()`：

```
#if CONFIG_SECURE_OTA_XIP
    f_ota_fun_ptr = bk_ota_secure_xip_backend();
#elif CONFIG_SECURE_OTA_OVERWRITE
    f_ota_fun_ptr = bk_ota_secure_overwrite_backend();
#endif
f_ota_fun_ptr->init(...);
```

未打开上述宏时，`f_ota_fun_ptr` 保持 `ota_base_drv.c` 中的默认 `s_ota_fun`。

<a id="id2"></a>

## 核心数据结构

<a id="f-ota-t"></a>

## f\_ota\_t（下载会话）

定义于 `ota_base_drv.h`。主要字段：

| 字段 | 含义 |
| --- | --- |
| `wr_buf` / `rd_buf` | 1KB 写缓冲 / 回读校验缓冲（`OTA_FLASH_BUFFER_LENGTH=1024`） |
| `wr_tmp_buf` | HTTP 回调临时缓冲（5KB） |
| `wr_last_len` | 当前 1KB 缓冲已填长度 |
| `image_size` / `received_total_size` | HTTP Content-Length 与已收字节 |
| `wr_address` | 非安全后端的 Flash 写指针 |
| `pt` | 非安全后端的目标分区 |
| `wr_err` | 粘性写失败标志，后续 chunk 直接失败 |
| `ota_type` | OTA\_TYPE\_WIFI / OTA\_TYPE\_BLE |
| `init_flag` | 是否已 init |

<a id="f-ota-func-t"></a>

## f\_ota\_func\_t（后端虚表）

```
typedef struct {
    int  (*init)(f_ota_t *);
    int  (*wr_flash)(f_ota_t *, uint16_t len);
    int  (*data_process)(f_ota_t *, uint16_t len, ota_update_type_t, ota_wr_callback);
    int  (*crc)(f_ota_t *, uint32_t);
    int  (*deinit)(f_ota_t *);
    int  (*finish)(f_ota_t *);   /* 可选；NULL 表示无收尾动作 */
    /* 另有 SD 卡路径的 open/write/umount ... */
} f_ota_func_t;
```

安全后端把校验折进 `data_process`，`crc` 置 `NULL`；成功路径必须实现 `finish`
（arm confirm / trial），失败则 `bk_ota_finish_and_reboot()` 打 `secure finalize failed` 并取消重启。

<a id="http"></a>

## HTTP 下载总流程

四套方案共用这段传输框架，后端在 `data_process` / `finish` 处分叉。

```
CLI / API: http_ota <url>
        |
        v
ota_do_init_operation()
  CONFIG_SECURE_OTA_XIP        -> ota_secure_xip 后端
  CONFIG_SECURE_OTA_OVERWRITE  -> ota_secure_overwrite 后端
  其它                         -> ota_base_drv 默认后端
  init() 解析分区、分配 1KB/5KB 缓冲
        |
   init 失败 ----> deinit，返回失败，不重启
        |
        v
EVT_OTA_START
bk_wifi_sta_pm_disable()          // 全程关 STA PS，避免下载卡住
httpclient_common(GET, 300s)
  每包 -> bk_ota_process_data()
       -> 后端 data_process()
          扇区对齐 erase + write + read-back
          wr_err=1 后后续包直接失败
        |
        +-- HTTP/写 Flash/校验失败 --+
        |                            v
        |                 恢复 STA PS
        |                 deinit，ota_fail
        |                 EVT_OTA_FAIL，不重启
        v
恢复 STA PS
        |
        +-- CONFIG_HTTP_AB_PARTITION --+
        |                              v
        |                    可选 hash 校验目标槽
        |                    写 ota_fina_executive TRIAL
        |                    ota_success + reboot
        |                    (不走 finish 钩子)
        v
其它方案: bk_ota_finish_and_reboot()
        |
        finish==NULL (非安全非 AB): deinit + reboot
        finish 成功 (安全 XIP/OW): 武装标志后 reboot
        finish 失败: secure finalize failed，deinit，不重启
```

进度日志：

- 安全后端：`secure overwrite: staged n%` 或 `secure xip: staged n%` （前 95% 每 10%，之后每 1%）
- 非安全后端：`cyg_recvlen_per` （同样的步进）

<a id="crc"></a>

## CRC 约定（必须与打包器一致）

| 用途 | 算法 |
| --- | --- |
| 安全 `ota.bin` 头 CRC / payload checksum | CheckSumUtils `CRC32_*`：init `0xFFFFFFFF`，多项式 `0xEDB88320`，**不做** 最终取反 |
| `boot_param` / `ota_fina_executive` AB 记录 | zlib/PKZIP CRC32：同样多项式，**做** 最终 `xor 0xFFFFFFFF` |
| Overwrite confirm 记录 | 与安全 `ota.bin` 相同（CheckSumUtils，无最终取反） |

两种 CRC 差 `^0xFFFFFFFF`。用错算法会导致“下载看似成功但头校验失败”或 AB 记录被当作无效。
