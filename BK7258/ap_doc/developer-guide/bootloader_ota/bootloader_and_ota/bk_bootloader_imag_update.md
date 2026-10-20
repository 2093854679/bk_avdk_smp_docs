---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/developer-guide/bootloader_ota/bootloader_and_ota/bk_bootloader_imag_update.html
sdk_family: bk_avdk_smp
chip: BK7258
processor: AP
sdk_version: v3.1.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="bootloader-bin"></a>

# 六.Bootloader.bin的镜像更新说明

- 1.为了优化bootloader.bin镜像的版本发布，从tag:v2.0.1.8版本开始：bootloader镜像的打包路径发生改变，由原先的默认路径middleware/boards/更改为cp/components/bk\_libs目录下。

  重要

  自从tag:v2.0.1.10之后的版本，已实现全自动插入bootloader.bin中的分区表，无需再手动修改bootloader中分区表。

  - 1.以7258的app工程为例修改分区步骤如下：
    :   - 1.通过修改bk\_avdk\_smp/projects/app/partitions/bk7258/auto\_partitions.csv文件来修改分区；
        - 2.直接make bk7258即可；
        - 3.无需手动修改bk\_avdk\_smp/cp/components/bk\_libs/bk7258/bootloader/normal\_bootloader/bootloader.bin；
  - 2.以app\_ab工程为例修改分区步骤如下：
    :   - 1.当通过修改bk\_avdk\_smp/projects/app\_ab/partitions/bk7258/auto\_partitions.csv文件来修改分区；
        - 2.直接make bk7258 PROJECT \= app\_ab即可；
        - 3.无需手动修改bk\_avdk\_smp/cp/components/bk\_libs/bk7258/bootloader/normal\_bootloader/bootloader.bin；

  重要

  bootloader镜像的打包路径发生改变，由原先的默认路径middleware/boards/更改为cp/components/bk\_libs目录下。

  - 1.以7258的app工程为例：
    :   - bootloader原路径为：middleware/boards/bk7258/bootloader.bin；
        - bootloader现路径为：bk\_avdk\_smp/cp/components/bk\_libs/bk7258/bootloader/normal\_bootloader/bootloader.bin；
  - 2.以7258的app\_ab工程为例：
    :   - bootloader现路径为：bk\_avdk\_smp/cp/components/bk\_libs/bk7258/bootloader/ab\_bootloader/bootloader.bin；
- 2.若升级过程中出现问题，请联系我们FAE支持。
