# Real-Time Dispatching Dataset

本資料集用於論文**「用於智慧製造即時派工之集中式多代理人系統的深度強化學習演算法」**，包含待排子批與機群狀態資料。

## Dataset Overview

| File           | Description | Records |
| -------------- | ----------- | ------: |
| `schedule.csv` | 待排子批資料      |   1,000 |
| `mach.csv`     | 機群狀態資料      |     150 |

資料集共包含 25 種配方（Recipe）。

## `schedule.csv`

| Column       | Description |
| ------------ | ----------- |
| `TT_LOT_NO`  | 母批編號        |
| `SCHEDULE`   | 子批編號        |
| `DUE_DATE`   | 子批交期        |
| `RECIPENAME` | 子批所需配方      |
| `PROD_TIME`  | 子批加工時間（小時）  |

## `mach.csv`

| Column         | Description  |
| -------------- | ------------ |
| `EQP_GROUP_ID` | 機群編號         |
| `m_count`      | 機群內的機台數量     |
| `NEW_RECIPE`   | 機群目前使用的配方    |
| `Arrive`       | 機群最快可用時間（小時） |

當子批配方與機群目前配方不同時，排程過程需考慮改機時間。
