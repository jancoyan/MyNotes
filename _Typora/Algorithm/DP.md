## Dynamic Programming



![](DP.assets/「动态规划」问题思考方向.png)


特点：

1. 计数

- 有多少种方式走到右下角
- 有多少种方法选出k个数使得和是Sum

2. 求最大最小值

- 从左上角走到右下角路径的最大数字和
- 最长上升子序列长度

3. 求存在性

- 取石子游戏，先手是否必胜
- 能不能选出k个数使得和是Sum

解题步骤：

动态规划组成部分一：确定状态

状态在动态规划中的作用属于定海神针，简单的说，解动态规划的时候需要开一个数组，数组的每个元素或者f]代表什么——类似于解数学题中，X，Y，Z代表什么

确定状态需要两个意识：

- 最后一步（最优策略的最后一步）
- 子问题（转化为子问题）

第二步：转移方程

第三步：初始条件和边界情况

第四步：确定计算顺序
