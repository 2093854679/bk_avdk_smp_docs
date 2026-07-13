# 系统配置



## 配置文件

Armino 支持下述几种配置文件：

> - Kconfig - 组件配置，生成 sdkconfig.h。详情情参考 [Kconfig 配置](bk_config_kconfig.md#bk-config-kconfig "bk_config_kconfig.md#bk-config-kconfig")。
> - csv - CSV 格式配置文件，包括:
>
>   - auto_partitions.csv - 自动分区配置表。详情请参考 [分区配置](bk_config_auto_partitions.md#bk-config-auto-partitions "bk_config_auto_partitions.md#bk-config-auto-partitions")。


## 文件部署

配置文件在 Armino 中部署如下图所示：


```

- armino/

    - ap/

        - components/

            - c1/

                - Kconfig

            - soc/

                - bk7259_ap/

                    - bk7259_ap.defconfig

    - cp/

        - components/

            - c1/

                - Kconfig

            - soc/

                - bk7259/

                    - bk7259.defconfig

    - projects/

        - my_project/

            - ap/

                - config/

                    - bk7259_ap/config

                - main/

                    - Kconfig

                - components/

                    - c1/

                        - Kconfig

            - cp/

                - config/

                    - bk7259/config

                - main/

                    - Kconfig

                - components/

                    - c1/

                        - Kconfig

            - partitions/

                - bk7259/auto_partitions.csv

```

对于同名配置文件或者配置项，优先级规则为：

> - 工程配置 > Middleware 配置 > 组件配置。
> - 对于同目录下配置文件：特定芯片配置项 > 通用配置项。

以上图所示目录为例，会使用 projects/my_project/partitions/bk7259/auto_partitions.csv 作为分区表.

备注

Kconfig 是使用高优先级文件中配置项取代低优先级配置文件中配置项；
其他配置文件是使用优先级高的配置文件取代优先级低的文件。
