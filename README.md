# Real-Time Dispatching Dataset

This dataset is developed for the research paper:

**「用於智慧製造即時派工之集中式多代理人系統的深度強化學習演算法」**

**"A Centralized, Multi-agent System with Deep Reinforcement Learning Algorithms for Real-time Dispatch in Smart Manufacturing"**  
[Paper Link](https://etd.lib.ncu.edu.tw/detail/fd6a7af26260c5591af3ce9e67075f0c/?seq=4)

The dataset represents a production scheduling environment with multiple recipes, parallel machine groups, due-date constraints, and setup requirements.

## Problem Overview

The dataset represents a real-time production dispatching problem involving multiple Recipes, Schedules, and parallel machine groups. Each Schedule has a required Recipe, processing time, and due date, while each machine group has a limited processing capacity, an earliest available time, and a current Recipe.

Each Schedule must be assigned to a compatible machine group. If the Schedule's Recipe differs from the current Recipe of the assigned machine group, a setup is required. The dispatching decisions continuously update machine availability and Recipe status, which affects subsequent decisions.

The main objectives are to **minimize total tardiness and the number of setups** while completing all Schedules. The problem is formulated as a sequential decision-making problem, where dispatching decisions consider due dates, processing times, machine capacity, machine availability, and setup requirements.

## Algorithm Overview

The proposed method uses a **hierarchical centralized multi-agent deep reinforcement learning framework** consisting of three main stages: **Recipe clustering, machine-group allocation, and real-time dispatching**.

First, **K-Means clustering** is used to group Recipes with similar production characteristics based on their workload, such as the number of Schedules and total processing time. An upper-level coordinator then determines the required machine groups for each cluster based on workload, urgent Schedules, and machine-group status, and allocates machine groups using a greedy strategy.

After resource allocation, each Recipe cluster is assigned an independent **Proximal Policy Optimization (PPO)** agent. Each PPO agent is responsible only for the Schedules and machine groups assigned to its cluster and selects Schedule–machine-group pairs for real-time dispatching. This hierarchical decomposition reduces the action space of individual agents while allowing them to learn dispatching strategies adapted to different production-load characteristics.

The proposed framework aims to improve scheduling performance by jointly considering **tardiness and setup requirements** during sequential dispatching.
