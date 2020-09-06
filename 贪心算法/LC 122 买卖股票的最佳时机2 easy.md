<img src = 'https://github.com/leopardv10/DataStructure-and-ComputerAlgorithm/blob/master/%E8%B4%AA%E5%BF%83%E7%AE%97%E6%B3%95/images/122-1.png?raw=true' width = 50%>

<img src = 'https://github.com/leopardv10/DataStructure-and-ComputerAlgorithm/blob/master/%E8%B4%AA%E5%BF%83%E7%AE%97%E6%B3%95/images/122-2.png?raw=true' width=50%>

### 1.贪心算法：

思路是从第0天开始依次向后看，天数为i，若第i+1天的股价高于第i天则在第i天买入，第i+1天卖出，res += prices[ i+1 ] - prices[ i ] 否则不动；

即对于示例2相当于res = (prices[1] - prices[0]) + (prices[2] - prices[1]) + (prices[3] - prices[2]) + (prices[4] - prices[3])

```java
class Solution {
    public int maxProfit(int[] prices) {
        int len = prices.length;
        int res = 0;
        for (int i=0; i<=len-2; i++) {
            int money = prices[i+1] - prices[i];
            if (money > 0) res += money;
        }
    return res;
    }
}
```

**贪心算法的核心在于证明其正确性**

<img src = 'https://github.com/leopardv10/DataStructure-and-ComputerAlgorithm/blob/master/%E8%B4%AA%E5%BF%83%E7%AE%97%E6%B3%95/images/122-3.png?raw=true' width = 80%>

### 2. 动态规划

1. 创建二维数组dp[ i ] [ j ]：

   i取值为0，1：0表示当天持有现金，1表示当天持有股票；

   j取值范围为0到prices.length-1；

2. 初始状态：dp[0] [0] = 0，dp[1] [0] = -prices[0]；

3. 状态转移：

   dp[0] [i] = max(dp[0] [i-1], dp[1] [i-1] + prices[i])，第i天持现金时，看i-1天就持现金和i-1天持股票，然后第i天卖出哪个大

   dp[1] [i] = max(dp[1] [i-1], dp[0] [i-1] - prices[i])，第i天持股票时，看第i-1天就持股票和第i-1天持现金，第i天买入股票哪个大

4. 以示例2为例：

   | prices |  1   |  2   |  3   |  4   |  5   |
   | :----: | :--: | :--: | :--: | :--: | :--: |
   | 持现金 |  0   |  1   |  2   |  3   |  4   |
   | 持股票 |  -1  |  -1  |  -1  |  -1  |  -1  |

   ```java
   class Solution {
       public int maxProfit(int[] prices) {
           int len = prices.length;
           int[][] dp = new int[2][len];
   
           dp[0][0] = 0;
           dp[1][0] = -prices[0];
   
           for (int i=1; i<=len-1; i++) {
               dp[0][i] = Math.max(dp[0][i-1], dp[1][i-1] + prices[i]);
               dp[1][i] = Math.max(dp[1][i-1], dp[0][i-1] - prices[i]);
           }
           return dp[0][len-1];
       }
   }
   ```

   

