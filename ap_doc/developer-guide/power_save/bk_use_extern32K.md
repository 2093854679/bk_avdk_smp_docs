# 使用外部32K



## 开启外部32K时钟源方法


- 确保硬件已经焊接了外部32K时钟源

- 在 `middleware/soc/bk7259/bk7259.defconfig` 中设置 `CONFIG_EXTERN_32K=y`

重要

当本地工程应用于其他项目时，为避免定义外部32K影响该工程，推荐在根目录下 `projects` 对应工程的 `config/bk72xx.config` 中配置 `CONFIG_EXTERN_32K=y`，不要直接修改公共 `middleware/soc/bk7259/bk7259.defconfig`。使用外部32K时，`CONFIG_LPO_SRC_26M32K` 应保持为n。
