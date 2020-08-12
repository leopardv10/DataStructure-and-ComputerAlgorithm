<img src = 'https://github.com/leopardv10/DataStructure-and-ComputerAlgorithm/blob/master/%E5%8A%A8%E6%80%81%E8%A7%84%E5%88%92/images/%E5%89%91%E6%8C%87offer14-1.png?raw=true' width = 50%>

### 动态规划：难点在于找到递推关系式  

1. 对于本题，对于一段n的绳子，至少要剪一刀，假设在长度为 i 的地方剪了一刀  

   * 若只剪一刀：res = i * (n - i)

   * 若不止剪一刀：res = dp[n - i] * i ；

     之所以是dp[n - i] * i 而不是dp[n - i] * dp[i] 是因为**可以将当前绳子视为在长度为n - i的绳子的基础上再剪一刀**。

     也就是说**长度为n的绳子与长度为n - i的绳子关系为，多剪了一刀**。  

   * 于是转移方程为 max( i * (n - i), dp[n - i] * i )；

2. 确定初始状态dp[2] = 1，dp[0]，dp[1]默认为0就行；

```java
class Solution {
    public int cuttingRope(int n) {
        int[] dp = new int[n + 1];
        for (int i = 2; i <= n; i++) {
            for (int j = 1; j <= i - 1; j++) {
                dp[i] = Math.max(Math.max(j * (i - j), j *dp[i - j]), dp[i]);
            }
        }
    return dp[n];
    }
}
```

