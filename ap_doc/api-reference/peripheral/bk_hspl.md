# HSPL


BK7259 AP 侧 HSPL（Hardware Spin Lock）API。详细说明见
[HSPL 开发指南](../../developer-guide/peripheral/bk_hspl.md "../../developer-guide/peripheral/bk_hspl.md")。


## HSPL Driver API


- `bk_hspl_driver_init` / `bk_hspl_driver_deinit`

- `bk_hspl_try_lock` / `bk_hspl_unlock`

- `bk_hspl_get_state`


## HSPL Resource Lock API


- `bk_hspl_res_lock` / `bk_hspl_res_try_lock` / `bk_hspl_res_unlock`

- `bk_hspl_res_lock_irqsave` / `bk_hspl_res_unlock_irqrestore`

- `bk_hspl_res_must_lock`

- `bk_hspl_res_get_map`


## 头文件


- `middleware/driver/hspl/hspl_driver.h`

- `middleware/driver/hspl/hspl_res_lock.h`
