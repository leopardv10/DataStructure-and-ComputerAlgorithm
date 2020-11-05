<img src='https://github.com/leopardv10/DataStructure-and-ComputerAlgorithm/blob/master/%E5%8A%A8%E6%80%81%E8%A7%84%E5%88%92/images/139.png?raw=true' width=50%>

本题使用动态规划求解，形式如下：

|           0            |   1   |   2   |   3   |  4   |   5   |   6   |   7   |  8   |
| :--------------------: | :---: | :---: | :---: | :--: | :---: | :---: | :---: | :--: |
| 字符串为空（初始状态） |   l   |   e   |   e   |  t   |   c   |   o   |   d   |  e   |
|          True          | false | false | false | true | false | false | false | true |

由上表可见dp[8] = dp[4] && ("code" in wordDict?)，因dp[4]=true && "code"在wordDict中，所以dp[8]=true；

dp[4] = dp[0] && ("leet" in wordDict?) = true。

**所以思路如下：**

1. 创建dp数组，dp[s.length() + 1]，dp[i] = true表示s[0: i] 在wordDict中可匹配；
2. 初始化dp[0] = true，即s为空时为true；
3. 转移方程：dp[j] = dp[i] && (s[i: j] in wordDict?)
4. 若dp[n]=true说明s[0: n]在wordDict中可匹配；

```java
class Solution {
    public boolean wordBreak(String s, List<String> wordDict) {
        int n = s.length();
        boolean[] dp = new boolean[n + 1];
        dp[0] = true; // 初始化状态
        for(int i = 0; i < n; i++) {
            if(!dp[i]) continue;  // dp[i] = false则不用进行后序匹配；
            for(int j = i + 1; j < n + 1; j++) {
                // dp[i]=true && s[i: j]在wordDict中-->dp[j]=true
                if(wordDict.contains(s.substring(i, j))) {
                    dp[j] = true;
                }
            }
        }
        return dp[n];
    }
}
```

