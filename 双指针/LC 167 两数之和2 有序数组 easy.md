<img src = 'https://github.com/leopardv10/DataStructure-and-ComputerAlgorithm/blob/master/%E5%8F%8C%E6%8C%87%E9%92%88/images/167.png?raw=true' width=50%>

### 双指针

### 因为是有序数组，所以：

1. 若numbers[ i ] + numbers[ j ] > target: numbers[ i ] + j后面的数均大于target，因此可直接忽略j与j后面的数

2. 若numbers[ i ] + numbers[ j ] < target: i前面的数 + numbers[ j ] 均大于target，因此直接忽略i和i前面的数
3. 设i = 0, j = numbers.length - 1，从这里开始排除

```java
class Solution { 
    public int[] twoSum(int[] numbers, int target) {
        int i = 0, j = numbers.length - 1;

        while (true) {
            int sum = numbers[i] + numbers[j];
            if (sum > target) {
                j--;
            } else if (sum < target) {
                i++;
            } else {
                return new int[]{i + 1, j + 1};
            }
        }
    }
}
```

