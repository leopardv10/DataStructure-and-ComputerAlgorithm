<img src = 'https://github.com/leopardv10/DataStructure-and-ComputerAlgorithm/blob/master/%E5%8A%A8%E6%80%81%E8%A7%84%E5%88%92/images/%E5%89%91%E6%8C%87offer19.png?raw=true' width = 50%>

### 动态规划：

dp [ i ] [ j ]表示p的前i个字符和s的前j个字符匹配结果

1. 若p[ i-1 ] == s[ j-1 ]或者p[ i-1 ] == '.'时，dp[ i ] [ j ] = dp[ i-1 ] [ j-1 ]；
2. 若p [ i-1 ] == '*' 时：
   - 设p的最后两个字符为c*，若不保留这两个字符，则dp [ i ] [ j ] = dp [ i-2 ] [ j ]；
   - **若保留这两个字符，则dp[ i ] [ j ] = dp[ i ] [ j - 1]，这里保留c*的话可知c与s最后一个字符肯定匹配，所以s减去最后一个字符，若和p仍然匹配，能推出p和s匹配；**

```java
class Solution {
    public boolean isMatch(String s, String p) {
        int len1 = s.length(), len2 = p.length();
        int[][] dp = new int[len2+1][len1+1];
        // s, p均为空
        dp[0][0] = 1;
        // s为空，p不为空
        for (int i=2; i<=len2; i++) {
            if (p.charAt(i-1) == '*') {
                dp[i][0] = dp[i-2][0];  // p的前i-2和空字符匹配，*可以使p[i-1]出现次数为0
            }
        }

        for (int i=1; i<=len2; i++) {
            for (int j=1; j<=len1; j++) {
                if (p.charAt(i-1) == s.charAt(j-1) || p.charAt(i-1) == '.') {
                    dp[i][j] = dp[i-1][j-1];
                }
                else if (p.charAt(i-1) == '*') {  // p的最后一个字符为*
                    // p的*前面的字符和s最后一个字符匹配
                    if (p.charAt(i-2) == s.charAt(j-1) || p.charAt(i-2) == '.') {
                        dp[i][j] = dp[i][j-1] | dp[i-2][j];
                    }
                    // p *前面的一个字符和s最后一个字符不匹配
                    else {
                        dp[i][j] = dp[i-2][j];
                    }
                }
            }
        }
        return dp[len2][len1] == 1;
    }
}
```

