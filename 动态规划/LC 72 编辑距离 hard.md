<img src = 'https://github.com/leopardv10/DataStructure-and-ComputerAlgorithm/blob/master/%E5%8A%A8%E6%80%81%E8%A7%84%E5%88%92/images/LC%2072.png?raw=true' width =50%>

### 动态规划告诉我们一个题目可以自底向上去思考：即初始是什么情况（两字符串均为空），然后逐个增加字符（在这个过程中完成状态转移），直到最后我们需要求解的情况；

对于本题，我们使dp [ i ] [ j ] 表示word1的0~i个字符和word2的0~j个字符转换需要的steps；

***动态规划两要素***

**1.初始化**

dp [ 0 ] [ j ]表示word1为空字符，变成word2[0 : j - 1]需要的steps

+ j = 0为0，j = 1为1，j=2为2，etc.

dp [ i ] [ 0 ]表示word1[0: i - 1]变成空字符串需要的steps

+ i = 0为0，i = 1为1，i=2为2，etc.

**2.状态转移方程：对于word1 [ i ]和word2 [ j ]有如下情况：**

1. word1 [ i ] == word2 [ j ]，则考虑i - 1和j - 1即可：

   dp[ i ] [ j ] = dp[ i - 1] [ j - 1]

2. 当word1 [ i ] != word2 [ j ] 时：   

   + 删除word1 [ i ]：则dp [ i ] [ j ] = dp [ i - 1] [ j ] + 1；
   + 替换word1 [ i ]：则dp [ i ] [ j ] = dp [ i - 1] [ j - 1] + 1；
   + 在word1 [ i ]后面增加一个字符：则dp [ i ] [ j ] = dp [ i ] [ j - 1] + 1；

```java
class Solution {
    public int minDistance(String word1, String word2) {
        int n1 = word1.length();
        int n2 = word2.length();

        int [][] dp = new int[n1 + 1][n2 + 1];
        for (int i = 1; i < n1 + 1; i++) dp[i][0] = dp[i - 1][0] + 1;
        for (int j = 1; j < n2 + 1; j++) dp[0][j] = dp[0][j - 1] + 1;

        for (int i = 1; i < n1 + 1; i++){
            for (int j = 1; j < n2 + 1; j++) {
                // dp[i][j]对应word1[i-1]和word2[j-1]
                if (word1.charAt(i-1) == word2.charAt(j-1)) dp[i][j] = dp[i - 1][j - 1];
                else dp[i][j] = Math.min(Math.min(dp[i - 1][j - 1] + 1, dp[i][j - 1] + 1), 
                dp[i - 1][j] + 1);
            }
        }
        return dp[n1][n2];
    }
}
```

