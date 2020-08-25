<img src = 'https://github.com/leopardv10/DataStructure-and-ComputerAlgorithm/blob/master/%E5%8A%A8%E6%80%81%E8%A7%84%E5%88%92/images/115.png?raw=true' width = 50%>

### 本题解法可采用暴力递归和动态规划：

### 1.暴力递归

从s[0]开始与t[0]匹配，若匹配则可用s[1]与t[1]继续，否则尝试s[1]与t[0]；

```java
if (s[j] == t[i]) dfs(res, s, t, i + 1, j + 1);
```

要注意的是：即使s[0]与t[0]匹配，我们也可以尝试s[1]，t[0]或者s[2]，t[0]等，即删去s[0]并尝试用s[1: ]去和target匹配；

```java
dfs(res, s, t, i, j + 1);
```

```java
class Solution {
    public int numDistinct(String s, String t) {
        int res = 0;
        dfs(res, s, t, 0, 0);
        return res;
    }
    public void dfs(int res, String s, String t, int i, int j) {
        if(i==t.length()){
            res++;
            return;
        }
        if(j==s.length()) return ;
        // s[j] & t[i]是否相等都要走这一步，（不相等时只能走这一步，相等时可走这一步）；
        dfs(res, s, t, i, j+1);
        // 发生匹配时，可将字符串 t 的下标 +1 然后进行匹配；
        if(s[j]==t[i]) dfs(res, s, t, i+1, j+1);
    }
};
```

### 2.动态规划

dp [ i ] [ j ]表示source的前j个字符和target的前i个字符去匹配； 

**还是动态规划两要素**：

1. 初始条件：

   - dp [ 0 ] [ j ]：表示target为空，与source的前 j 个字符去匹配的可能选择数，

     因为tagert == none，因此无论 j 是多少，结果都是1（删去所有 j 个字符）；

   - dp [ i ] [ 0 ]：source为空，对于 i > 0，结果都为0（因为source为空，没法匹配）；

   - dp [ 0 ] [ 0 ] = 1；

2. 状态转移方程：

   - 当 t[ i ] == s[ j ]时：

     dp[ i ] [ j ] = dp[ i-1 ] [ j-1 ] + dp[ i ] [ j-1 ]；

   - 当t[ i ] != s[ j ]时：

     dp[ i ] [ j ] = dp[ i ] [ j-1 ]；

3. 初始化表格如下：

|      |  0   |  a   |  b   |  b   |  a   |  b   |  c   |
| :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: |
|  0   |  1   |  1   |  1   |  1   |  1   |  1   |  1   |
|  a   |  0   |      |      |      |      |      |      |
|  b   |  0   |      |      |      |      |      |      |
|  c   |  0   |      |      |      |      |      |      |



```java
class Solution {
    public int numDistinct(String s, String t) {
        int len1 = s.length();
        int len2 = t.length();
        int[][] dp = new int[len2 + 1][len1 + 1];  // 初始化数组的默认值为0

        for (int j = 0; j <= len1; j++) dp[0][j] = 1;

        for (int i = 1; i <= len2; i++) {
            for (int j = i; j <= len1; j++) {  // 这里不用从1开始，因为必须满足j >= i，否则不可能匹配上
                if (t.charAt(i - 1) == s.charAt(j - 1)) {
                    dp[i][j] = dp[i - 1][j - 1] + dp[i][j - 1];
                }
                else {
                    dp[i][j] = dp[i][j - 1];
                }
            }
        }
        return dp[len2][len1];
    }
}
```







