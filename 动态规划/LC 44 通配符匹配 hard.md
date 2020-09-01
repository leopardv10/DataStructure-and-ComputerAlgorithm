<img src = 'https://github.com/leopardv10/DataStructure-and-ComputerAlgorithm/blob/master/%E5%8A%A8%E6%80%81%E8%A7%84%E5%88%92/images/lc44-1.png?raw=true' width=50%>

<img src = 'https://github.com/leopardv10/DataStructure-and-ComputerAlgorithm/blob/master/%E5%8A%A8%E6%80%81%E8%A7%84%E5%88%92/images/lc44-2.png?raw=true' width = 50%>

### 此题可用动态规划求解：

1. dp[i] [j]表示p的前i个字符和s的前j个字符匹配结果，eg：dp[1] [1] 表示p[0]和s[0]的匹配结果；
2. 这里dp数组的dimension为[len(p) + 1] [len(s) + 1]，因为考虑p或s为空的情况，eg: dp[0] [0]表示p和s都为空；
3. 注意 '?'只能匹配字母，不能匹配空格；

```java
class Solution {
    public boolean isMatch(String s, String p) {
        int len1 = p.length(), len2 = s.length();
        int[][] dp = new int[len1+1][len2+1];
        //s，p都为空：初始化
        dp[0][0] = 1; 
        // s为空p不为空的匹配情况：初始化，这种情况需要注意
        for (int i=1; i<=len1; i++) {
            if (p.charAt(i-1) == '*') dp[i][0] = 1;
            else break;
        }
        // 下面的循环只适用s和p都不为空时的匹配情况
        for (int i=1; i<=len1; i++) {
            for (int j=1; j<=len2; j++) {
                // '||'一般在条件判断里用
                if (p.charAt(i-1) == s.charAt(j-1) || p.charAt(i-1) == '?') {
                    dp[i][j] = dp[i-1][j-1];
                }
                else if (p.charAt(i-1) == '*') {
                    // '|'按位或；这里dp[i-1][j-1]==0时, dp[i][j-1]肯定也==0，所以省略；
                    dp[i][j] = dp[i-1][j] | dp[i][j-1];
                }
            }
        }
        return dp[len1][len2] == 1;
    }
}
```



