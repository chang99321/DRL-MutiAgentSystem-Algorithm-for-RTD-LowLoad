# Real-Time Dispatching Dataset
This dataset is developed for the research paper:

**「用於智慧製造即時派工之集中式多代理人系統的深度強化學習演算法」**

**"A Centralized, Multi-agent System with Deep Reinforcement Learning Algorithms for Real-time Dispatch in Smart Manufacturing"**  
[Paper Link](https://etd.lib.ncu.edu.tw/detail/fd6a7af26260c5591af3ce9e67075f0c/?seq=4)

The dataset represents a production scheduling environment with multiple Recipes, parallel machine groups, due-date constraints, and setup requirements.

## Dataset Overview

| File | Description | Records |
|---|---|---:|
| `schedule.csv` | Schedules waiting for dispatching | 1,000 |
| `mach.csv` | Machine group status data | 150 |

The dataset contains **25 different Recipes**.

## Problem Overview

The dataset represents a real-time production dispatching problem involving multiple Recipes, Schedules, and parallel machine groups.

Each Schedule has a required Recipe, processing time, and due date, while each machine group has a limited processing capacity, an earliest available time, and a current Recipe.

Each Schedule must be assigned to a compatible machine group. If the Recipe of a Schedule differs from the current Recipe of the assigned machine group, a setup is required. Each dispatching decision updates the machine group's availability and current Recipe, which affects subsequent scheduling decisions.

The main objectives are to **minimize total tardiness and the number of setups** while completing all Schedules.

## Algorithm Overview

The proposed method uses a **hierarchical centralized multi-agent deep reinforcement learning framework** consisting of three main stages:

1. **Recipe Clustering**  
   K-Means is used to group Recipes with similar production characteristics based on workload-related features, such as the number of Schedules and total processing time.

2. **Machine-Group Allocation**  
   An upper-level coordinator determines the required machine groups for each Recipe cluster based on workload, urgent Schedules, and machine-group status. The available machine groups are then allocated to suitable clusters using a greedy strategy.

3. **Real-Time Dispatching**  
   Each Recipe cluster is assigned an independent **Proximal Policy Optimization (PPO)** agent. Each agent is responsible for the Schedules and machine groups assigned to its cluster and selects Schedule–machine-group pairs for real-time dispatching.

This hierarchical decomposition reduces the action space of individual agents and allows each PPO agent to learn dispatching strategies adapted to different production-load characteristics.

## schedule.csv

`schedule.csv` records all Schedules waiting to be dispatched.

| Column | Description |
|---|---|
| `TT_LOT_NO` | Parent lot ID. A parent lot can be divided into multiple Schedules. |
| `SCHEDULE` | Schedule ID, which serves as the identifier for each pending job. |
| `DUE_DATE` | Due date of the Schedule, indicating the deadline by which the Schedule should be completed. |
| `RECIPENAME` | Processing Recipe required by the Schedule. |
| `PROD_TIME` | Processing time in hours. |

## mach.csv

`mach.csv` records the initial status of each machine group at the beginning of the scheduling process.

| Column | Description |
|---|---|
| `EQP_GROUP_ID` | Machine group ID, which serves as the identifier for each machine group. |
| `m_count` | Number of parallel machines within the machine group. A larger value indicates that more Schedules can be processed simultaneously. |
| `NEW_RECIPE` | Current processing Recipe of the machine group. If the Recipe of the next Schedule is different, a setup is required. |
| `Arrive` | Earliest available time of the machine group, in hours. For example, `Arrive = 2` indicates that the machine group becomes available 2 hours after the beginning of the scheduling process. |

## KMeans_K=5.xlsx

`KMeans_K=5.xlsx` contains the results of applying **K-Means clustering with K = 5** to the Recipes.

The clustering is based on two production-load features for each Recipe:

- **Total number of Schedules**
- **Total processing time of Schedules**

Recipes with similar production-load characteristics are grouped into the same cluster. The resulting five Recipe clusters are used as the basis for the subsequent machine-group allocation and multi-agent PPO dispatching process.

## Scheduling Rules

* Each Schedule must be assigned to one compatible machine group for processing.
* The effective processing capacity of a machine group is affected by the number of parallel machines within the group.
* If the Recipe of a Schedule differs from the current Recipe of the assigned machine group, a setup time is required.
* After a Schedule is dispatched, the machine group's availability and current Recipe are updated.
* If the completion time of a Schedule exceeds its `DUE_DATE`, tardiness is incurred.
* The scheduling process continues until all Schedules have been assigned to machine groups.

## Main Code

`RL-multiAgentSystem-for-RTDproblem(lowLoad).ipynb` is a **Google Colab** notebook containing the implementation of:

* Production scheduling environment
* Recipe clustering
* Machine-group allocation
* PPO agent construction
* Multi-agent model training
* Training results and gantt charts

The notebook implements the proposed centralized multi-agent real-time dispatching framework.
