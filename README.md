# Real-Time-Dispatching-Method-for-Productive-Scheduling


## 這是論文"用於智慧製造即時派工之集中式多代理人系統的深度強化學習演算法"使用的排程資料集

## mach.csv是機群資料集，裡面包括以下資訊:
EQP_GROUP_ID: 機群名稱
m_count: 機群的機台數量，機台數量越多能更快平分去處理子批
NEW_RECIPE: 機群目前配方，會影響第一個排上去的子批是否需要改機
Arrive: 機群最快可用時間(小時)，至少要經過這麼長時間才能排上第一個子批
