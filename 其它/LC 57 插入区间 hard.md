<img src = 'https://github.com/leopardv10/DataStructure-and-ComputerAlgorithm/blob/master/%E5%85%B6%E5%AE%83/images/57.png?raw=true' width = 50%>

### 本题不考察算法知识，基本只需将每一步思路理清楚即可：

1. 创建空的 res = [] 数组:

2. 对于intervals中所有的 intervals [ i ] [ 1 ] < newInterval [ 0 ]的全部放入res中，

   如例2中的[1, 2]。 

3. **接下来便是newInterval [ 0 ] <= intervals [ i ] [ 1 ] 的情况**

   **如[3, 5]和 newInterval --> [4, 8], 4 < 5；**

   **这时呢，对于所有这样有重叠部分的数组，我们将其merge成一个长度为2数组，取名为tmp；**

   **所以tmp[0] = min(3, 4), tmp[1] = max(5, 8), 得到tmp=[3, 8]**

4. **然后对于[3, 8]，因为其满足 newInterval[1] >= intervals[ i ] [ 0 ]，所以[3, 8]和[6, 7]有交集，按3继续merge，**

   **直到newInterval [ 1] < interval [ i ] [ 0 ];**

   **比如[3, 10]和[12, 16], 10 < 12所以无交集。**

5. 将剩下的数组放入res即可。

```java
class Solution {
    public int[][] insert(int[][] intervals, int[] newInterval) {
        List<int[]> res = new ArrayList<>();  // 集合
        int i = 0;
        // 对应2
        while (i <= intervals.length-1 && newInterval[0] > intervals[i][1]) {
            res.add(intervals[i]);
            i++;
        }
	// 对应3，4
        int[] tmp = new int[] {newInterval[0], newInterval[1]};
        while (i <= intervals.length-1 && newInterval[1] >= intervals[i][0]) {
            tmp[0] = Math.min(tmp[0], intervals[i][0]);
            tmp[1] = Math.max(tmp[1], intervals[i][1]);
            i++;
        }
        res.add(tmp);
	// 对应5
        while (i <= intervals.length-1) {
            res.add(intervals[i]);
            i++;
        }
        return res.toArray(new int[0][]);  // 集合转数组
    }
}
```

