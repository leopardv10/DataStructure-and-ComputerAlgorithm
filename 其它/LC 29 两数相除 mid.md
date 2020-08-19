<img src = 'https://github.com/leopardv10/DataStructure-and-ComputerAlgorithm/blob/master/%E5%85%B6%E5%AE%83/images/29-1.png?raw=true' width=50%>

<img src = 'https://github.com/leopardv10/DataStructure-and-ComputerAlgorithm/blob/master/%E5%85%B6%E5%AE%83/images/29-2.png?raw=true' width=50%>

### 本题思路是用除数减去被除数，但是如果遇到2^31 与 1这样的数肯定会超时，因此我们除的时候对除数不断翻倍  

比如：被除数15，除数3

15， 3

15 - 3 = 12，3 * 2 = 6

12 - 6 = 6，6 * 2 = 12

这时6（被除数）< 12 （除数）

6，3（除数回归3）

3，3

0，3 

这样可有效减小程序的时间复杂度；

```java
class Solution {
    public int divide(int dividend, int divisor) {
        int sign = 1;
        if (dividend > 0 && divisor < 0) sign = -1;
        if (dividend < 0 && divisor > 0) sign = -1;
        long Dividend = Math.abs((long)dividend);  // 先用long型存储防止溢出
        long Divisor = Math.abs((long)divisor);  // 先用long型存储防止溢出
        long res = 0;  // 先用long型存储防止溢出

        while(Dividend >= Divisor) {
            long tmp = Divisor;
            long i = 1;  // 若i=1表示减去除数，i=2表示除数以及翻倍，i=3表示除数以及为原来的3倍...
            while (Dividend >= tmp) {
                Dividend -= tmp;
                res += i;
                i <<= 1;
                tmp <<= 1;  // 除数翻倍
            }
        }

        if (sign == -1) res *= -1;
        if (res < Integer.MIN_VALUE) return Integer.MIN_VALUE;
        else if (res > Integer.MAX_VALUE) return Integer.MAX_VALUE;
        return (int)res;
    }
}
```



