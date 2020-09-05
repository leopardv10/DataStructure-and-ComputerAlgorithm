<img src = 'https://github.com/leopardv10/DataStructure-and-ComputerAlgorithm/blob/master/%E5%8A%A8%E6%80%81%E8%A7%84%E5%88%92/images/LC%20887.png?raw=true' width = 50%>

### 暴力解法：

```java
class Solution {
    public int superEggDrop(int K, int N) {
        int[][] dp = new int[K+1][N+1];
        for (int i=1; i<=N; i++) {  // 一个鸡蛋的情况
            dp[1][i] = i;
        }

        for (int i=2; i<=K; i++) {
            for (int j=1; j<=N; j++) {
                int res = N*N;
                for (int x=1; x<=j; x++) {
                    res = Math.min(res, 1+Math.max(dp[i-1][x-1], dp[i][j-x]));
                }
                dp[i][j] = res;
            }
        }
        return dp[K][N];
    }
}
```



### 二分查找

```java
class Solution {
    public int superEggDrop(int K, int N) {
        int[][] dp = new int[K+1][N+1];
        for (int i=1; i<=N; i++) {  // 一个鸡蛋的情况
            dp[1][i] = i;
        }

        for (int i=2; i<=K; i++) {
            for (int j=1; j<=N; j++) {
                int res = N;
                int low = 1, high = j;

                while (low <= high) {
                    int x = (high + low) / 2; 
                    int broken = dp[i-1][x-1], not_broken = dp[i][j-x];

                    if (broken > not_broken) {
                        high = x - 1;
                        res = Math.min(res, broken + 1);
                    } else {
                        low = x + 1;
                        res = Math.min(res, not_broken + 1);
                    }
                }
                dp[i][j] = res;
            }
        }
        return dp[K][N];
    }
}
```

