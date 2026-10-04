# Real-Time Dispatching Dataset

This dataset is developed for the research paper:

**「用於智慧製造即時派工之集中式多代理人系統的深度強化學習演算法」**

**"A Centralized, Multi-agent System with Deep Reinforcement Learning Algorithms for Real-time Dispatch in Smart Manufacturing"**  
[Paper Link](https://etd.lib.ncu.edu.tw/detail/fd6a7af26260c5591af3ce9e67075f0c/?seq=4)

The dataset represents a production scheduling environment with multiple recipes, parallel machine groups, due-date constraints, and setup requirements.

## Dataset Overview

| File | Description | Records |
|---|---|---:|
| `schedule.csv` | Schedules waiting for dispatching | 1,000 |
| `mach.csv` | Machine group status data | 150 |

The dataset contains **25 different recipes**.

## schedule.csv

`schedule.csv` records all Schedules waiting to be dispatched.

| Column | Description |
|---|---|
| `TT_LOT_NO` | Parent lot ID. A parent lot can be divided into multiple Schedules. |
| `SCHEDULE` | Schedule ID, which serves as the identifier for each pending job. |
| `DUE_DATE` | Due date of the Schedule, indicating the deadline by which the Schedule should be completed. |
| `RECIPENAME` | Processing recipe required by the Schedule. |
| `PROD_TIME` | Processing time in hours. |

## mach.csv

`mach.csv` records the initial status of each machine group at the beginning of the scheduling process.

| Column | Description |
|---|---|
| `EQP_GROUP_ID` | Machine group ID, which serves as the identifier for each machine group. |
| `m_count` | Number of parallel machines within the machine group. A larger value indicates that more Schedules can be processed simultaneously. |
| `NEW_RECIPE` | Current processing recipe of the machine group. If the recipe of the next Schedule is different, a setup is required. |
| `Arrive` | Earliest available time of the machine group, in hours. For example, `Arrive = 2` indicates that the machine group becomes available 2 hours after the beginning of the scheduling process. |

## Scheduling Rules

* Each Schedule must be assigned to one machine group for processing.
* The processing capacity of a machine group is affected by the number of parallel machines within the group.
* If the recipe of a Schedule differs from the current recipe of the assigned machine group, a setup time is required.
* If the completion time of a Schedule exceeds its `DUE_DATE`, tardiness is incurred.

## Main Code

`RL-multiAgentSystem-for-RTDproblem(lowLoad).ipynb` is a **Google Colab** notebook containing the implementation of the scheduling environment, model construction, model training, and training results.
