## LeetCode

### 53.最大子序和

给定一个整数数组 nums ，找到一个具有最大和的连续子数组（子数组最少包含一个元素），返回其最大和。

```cpp
示例:

输入: [-2,1,-3,4,-1,2,1,-5,4]
输出: 6
解释: 连续子数组 [4,-1,2,1] 的和最大，为 6。
进阶: 如果你已经实现复杂度为 O(n) 的解法，尝试使用更为精妙的分治法求解。
```

---

第一步：确定状态，即dp数组表示什么？

- dp[i] 表示以当前数字结尾的数字之和的最大值

第二步：转移方程 

- dp[i] = max(dp[i - 1] + nums[i], nums[i]);
- 加上当前的数字，和以当前的数字作为起点，哪个更大

第三步：初始条件和边界情况

-  dp[0] = nums[0]; //如果只有第一个数字，那么它就是最大的。
- 从下标为1的数字开始，因为0已经作为了dp[0]了

第四步：确定计算顺序

- 从头开始，逐渐递增。

```c++
class Solution {
public:
    int maxSubArray(vector<int>& nums) {
        vector<int> dp(nums.size(), 0);
        int rst = nums[0];
        dp[0] = nums[0]; //初始条件：第0个是只有第一个数字。
        for(int i = 1; i < nums.size(); i++){
            dp[i] = max(dp[i - 1] + nums[i], nums[i]); //状态转移方程：加上和不加，哪个更大
            if(dp[i] > rst) rst = dp[i]; //rst是当前的数组中的最大值
        }
        return rst;
    }
};
```

### 70.爬楼梯

假设你正在爬楼梯。需要 n 阶你才能到达楼顶。

每次你可以爬 1 或 2 个台阶。你有多少种不同的方法可以爬到楼顶呢？

注意：给定 n 是一个正整数。

```cpp
示例 1：
输入： 2
输出： 2
解释： 有两种方法可以爬到楼顶。

1 阶 + 1 阶
2 阶
  //  -------------------------
示例 2：
输入： 3
输出： 3
解释： 有三种方法可以爬到楼顶。

1 阶 + 1 阶 + 1 阶
1 阶 + 2 阶
2 阶 + 1 阶
```

---

第一步：确定状态，即dp数组表示什么？

- 代表到达当前的楼梯的方法个数

第二步：转移方程 

- dp[i] = dp[i - 1] + dp[i - 2];

第三步：初始条件和边界情况

- dp[1] = 1; dp[2] = 2;

第四步：确定计算顺序

- 从小到大，依次算出

```c++
class Solution {
public:
    int climbStairs(int n) {
        vector<int> dp(n + 3, 0); //为什么+3 ？ 避免传入的n为0，则dp[2] 无法访问
        dp[1] = 1;
        dp[2] = 2;
        for(int i = 3; i <= n; i++){
            dp[i] = dp[i - 1] + dp[i - 2];
        }
        return dp[n];
    }
};
```

### 72. 编辑距离


给你两个单词 word1 和 word2，请你计算出将 word1 转换成 word2 所使用的最少操作数 。

你可以对一个单词进行如下三种操作：

插入一个字符
删除一个字符
替换一个字符
 
```
示例 1：

输入：word1 = "horse", word2 = "ros"
输出：3
解释：
horse -> rorse (将 'h' 替换为 'r')
rorse -> rose (删除 'r')
rose -> ros (删除 'e')
示例 2：

输入：word1 = "intention", word2 = "execution"
输出：5
解释：
intention -> inention (删除 't')
inention -> enention (将 'i' 替换为 'e')
enention -> exention (将 'n' 替换为 'x')
exention -> exection (将 'n' 替换为 'c')
exection -> execution (插入 'u')

```
---


第一步：确定状态，即dp数组表示什么？

- 表示 word1[i]之前的字符串转化为 word2[j] 之前的字符串所进行的最小操作数。

第二步：状态转移方程 

- 当前指向的两个字母，相等的时候 dp[i][j] = dp[i - 1][j - 1]，也就是当前不用进行操作，直接复制上一步的操作结果

- 当前指向的两个字母不相等的时候，dp的值为其相邻的有值元素的最小值+1，也就是上一个状态所进行的最小操作再进行一步操作。

第三步：初始条件和边界情况

- 两个都是空串，想要进行转化，必须逐个加上去。

第四步：确定计算顺序

- 自底向上

```c++

class Solution {
public:
    int minDistance(string word1, string word2) {
        vector<int> t(word2.size() + 1, 0);
        vector<vector<int>> dp(word1.size() + 1, t);
        for (int i = 0; i <= word2.size(); i++) dp[0][i] = i;
        for (int i = 0; i <= word1.size(); i++) dp[i][0] = i;
        for (int i = 1; i <= word1.size(); i++) {
            for (int j = 1; j <= word2.size(); j++) {
                if (word1[i - 1] == word2[j - 1]) dp[i][j] = dp[i - 1][j - 1]; //这里在进行比较的时候要记得用 i - 1 , j - 1;
                else dp[i][j] = 1 + min(min(dp[i - 1][j], dp[i][j - 1]), dp[i - 1][j - 1]);
            }
        }
        return dp[word1.size()][word2.size()];
    }
};

```


### 121.买卖股票的最佳时机

给定一个数组，它的第 i 个元素是一支给定股票第 i 天的价格。

如果你最多只允许完成一笔交易（即买入和卖出一支股票一次），设计一个算法来计算你所能获取的最大利润。

注意：你不能在买入股票前卖出股票。

```
示例 1:

输入: [7,1,5,3,6,4]

输出: 5

解释: 在第 2 天（股票价格 = 1）的时候买入，在第 5 天（股票价格 = 6）的时候卖出，最大利润 = 6-1 = 5 。

注意利润不能是 7-1 = 6, 因为卖出价格需要大于买入价格；同时，你不能在买入前卖出股票。

示例 2:

输入: [7,6,4,3,1]

输出: 0

解释: 在这种情况下, 没有交易完成, 所以最大利润为 0。
```

---

这个题不用动态规划其实有空间复杂度O(1)的办法，这里为了练习使用动态规划，就强行用了DP

第一步：确定状态，即dp数组表示什么？

- 表示最大利润。

第二步：状态转移方程 

- dp[i] = max(dp[i - 1], prices[i] - m);

- 当前的最大利润是 max(上一天的最大值，今天的最大值减去历史最小值)；

第三步：初始条件和边界情况

- dp[0] = 0, 第一天只能买入，所以收益只能是0


```c++
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        if(prices.size() == 0||prices.size() == 1) return 0;
        vector<int> dp(prices.size(), 0);
        int m = prices[0];
        int rst = 0;
        dp[0] = 0;
        for (int i = 1; i < prices.size(); i++) {
            dp[i] = max(dp[i - 1], prices[i] - m);
            if (m > prices[i]) m = prices[i];
            if (dp[i] > rst) rst = dp[i];
        }
        return rst;
    }
};
```





### 198.打家劫舍

你是一个专业的小偷，计划偷窃沿街的房屋。每间房内都藏有一定的现金，影响你偷窃的唯一制约因素就是相邻的房屋装有相互连通的防盗系统，如果两间相邻的房屋在同一晚上被小偷闯入，系统会自动报警。

给定一个代表每个房屋存放金额的非负整数数组，计算你 不触动警报装置的情况下 ，一夜之内能够偷窃到的最高金额。

```cpp
示例 1：

输入：[1,2,3,1]
输出：4
解释：偷窃 1 号房屋 (金额 = 1) ，然后偷窃 3 号房屋 (金额 = 3)。 偷窃到的最高金额 = 1 + 3 = 4 。

示例 2：

输入：[2,7,9,3,1]
输出：12
解释：偷窃 1 号房屋 (金额 = 2), 偷窃 3 号房屋 (金额 = 9)，接着偷窃 5 号房屋 (金额 = 1)。 
偷窃到的最高金额 = 2 + 9 + 1 = 12 。

提示：

0 <= nums.length <= 100
0 <= nums[i] <= 400
```

---

第一步：确定状态，即dp数组表示什么？

- dp[i]代表偷取当前房子和不偷当前房子所获得的财宝中的最大的那个

第二步：转移方程 

- dp[i] = max(dp[i - 1], dp[i - 2] + nums[i]);

第三步：初始条件和边界情况

- 对数组大小为0或者1的时候进行特殊判定，以保证数组的大小是2以上的时候可以直接使用状态转移方程。

- 初始条件：dp[0]/dp[1] 是已知的

第四步：确定计算顺序

- 从头到尾，递推。

```c++
class Solution {
public:
    int rob(vector<int>& nums) {
        if(nums.size() == 0) return 0;
        if(nums.size() == 1) return nums[0];
        vector<int> dp(nums.size(), 0);
        dp[0] = nums[0];
        dp[1] = max(nums[0], nums[1]);
        for(int i = 2; i < nums.size(); i++){
            dp[i] = max(dp[i - 1], dp[i - 2] + nums[i]);
        }
        return dp[nums.size() - 1];
    }
};
```


### 213.打家劫舍II

要求和题目 198.打家劫舍 类似，只不过现在的第一个房子和最后一个房子连起来了，你不能同时偷走第一个房子和最后一个房子里面的东西。

---

第一步：确定状态，即dp数组表示什么？

- 表示偷和不偷当前房子，能取得财宝的最大值。

第二步：转移方程 

- dp[i]  = max(dp[i - 2] + nums[i], dp[i - 1]);

第三步：初始条件和边界情况

- 因为第一个房子和最后一个房子不能同时抢劫，所以此题可以分为两部分：有头没尾和有尾没头。

- 也就是说，要分别算出来两种状态下的最大值，进行两次动态规划

第四步：确定计算顺序

- 从小到大，依次累积。

```c++
class Solution {
public:
    int rob(vector<int>& nums) {
        if (nums.size() == 0) return 0;
        if (nums.size() == 1) return nums[0];
        if (nums.size() == 2) return max(nums[0], nums[1]);

        vector<int> dp(nums.size() - 1, 0);
        int rst = 0;
        //0 -- size - 1
        dp[0] = nums[0];
        dp[1] = max(nums[0], nums[1]);
        for (int i = 2; i < nums.size() - 1; i++) {
            dp[i] = max(dp[i - 2] + nums[i], dp[i - 1]);
        }
        rst = dp[nums.size() - 2];
        dp.clear();
        dp.resize(nums.size() - 1);

        //1 -- size
        dp[0] = nums[1];
        dp[1] = max(nums[1], nums[2]);
        for (int i = 3; i < nums.size(); i++) {
            dp[i - 1] = max(dp[i - 3] + nums[i], dp[i - 2]);
        }
        if (rst < dp[nums.size() - 2]) rst = dp[nums.size() - 2];
        return rst;
    }
};
```

