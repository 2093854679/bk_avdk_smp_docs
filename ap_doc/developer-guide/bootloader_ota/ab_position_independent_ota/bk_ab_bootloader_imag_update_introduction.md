# Bootloader.bin的镜像更新说明



- 1.为了优化bootloader.bin镜像的版本发布，从tag:v2.0.1.8版本开始：bootloader镜像的打包路径发生改变，由原先的默认路径middleware/boards/更改为bk_avdk_smp/cp/components/bk_libs目录下。

  重要

  自从tag:v2.0.1.10之后的版本，已实现全自动插入bootloader.bin中的分区表，无需再手动修改bootloader中分区表。


  - 1.以bk_avdk_smp中app_ab工程为例修改分区步骤如下：
    :   - 1.当通过修改bk_avdk_smp/projects/app_ab/partitions/bk7259/auto_partitions.csv文件来修改分区；

        - 2.直接make bk7259 PROJECT = app_ab即可；

        - 3.无需手动修改bk_avdk_smp/cp/components/bk_libs/bk7259/bootloader/normal_bootloader/bootloader.bin；

  重要

  bootloader镜像的打包路径发生改变，由原先的默认路径middleware/boards/更改为bk_avdk_smp/cp/components/bk_libs目录下。


  - 1.以7258的app_ab工程为例：
    :   - bootloader现路径为：bk_avdk_smp/cp/components/bk_libs/bk7259/bootloader/ab_bootloader/bootloader.bin；

- 2.若升级过程中出现问题，请联系我们FAE支持。
