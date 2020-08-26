<img src = 'https://github.com/leopardv10/DataStructure-and-ComputerAlgorithm/blob/master/%E6%A0%88/images/lc84-1.png?raw=true' width = 50%>

<img src = 'https://github.com/leopardv10/DataStructure-and-ComputerAlgorithm/blob/master/%E6%A0%88/images/lc84-2.png?raw=true' width = 50%>

### 方法一：暴力解法

对于每跟柱子，向其两侧遍历，直到遇到高度低于它的柱子；

时间复杂度：https://latex.codecogs.com/gif.latex?\\o(n^2)，空间复杂度O(1)；

```java
public class Solution {
    public int largestRectangleArea(int[] heights) {
        int len = heights.length;
        if (len == 0) {
            return 0;
        }

        int res = 0;
        for (int i = 0; i < len; i++) {
            // 找左边最后 1 个大于等于 heights[i] 的下标
            int left = i;
            int curHeight = heights[i];
            while (left > 0 && heights[left - 1] >= curHeight) {
                left--;
            }

            // 找右边最后 1 个大于等于 heights[i] 的索引
            int right = i;
            while (right < len - 1 && heights[right + 1] >= curHeight) {
                right++;
            }

            int width = right - left + 1;
            res = Math.max(res, width * curHeight);
        }
        return res;
    }
}
```



### 方法二：单调栈

思路还是对任意一个柱子，求得其左右边界，只不过通过维护单调栈来实现一次遍历；

时间复杂度：O(n)，空间复杂度：O(n)；

1. 维护一个单调递增栈，栈中储存的是柱子的index；

2. 若当前柱子高度heights[ i ] < 栈顶index对应的柱高，栈顶元素弹出；

   循环直到当前柱高heights[ i ] >= 栈顶index对应柱高，入栈； 

3. **每弹出一个index，就计算高为height [index]的柱子对应的最大面积：**

   面积 = height[index] * 宽

   宽 = right_index - left_index + 1

   right_index = i - 1 (i为当前柱子)，left_index = 栈顶元素 + 1；

4. 有一个细节需要注意，及**如何处理栈中最后的剩余元素：**

   <img src = 'https://github.com/leopardv10/DataStructure-and-ComputerAlgorithm/blob/master/%E6%A0%88/images/lc84-3.png?raw=true' width = 80%>

   如上图所示，最后栈中会剩余1，2，3，因为我们只有出栈时才求其面积，所以要使其出栈；

   一种方法是栈不为空时继续出栈，另一种方法是在原heights数组头尾添加0；

   - heights数组头尾添加0，最后情况为stack = [0, 1, 2, 3]，当前需入栈的index对应height为0，所以3，2，1依次弹出，即可求得其面积。最终栈内剩余[0, 0]；

```java
import java.util.Stack;

class Solution {
    public int largestRectangleArea(int[] heights) {
        int [] heights_plus = new int[heights.length + 2];
        System.arraycopy(heights, 0, heights_plus, 1, heights.length);
        Stack<Integer> stack = new Stack<>();

        int res = 0;

        for (int i=0; i < heights_plus.length; i++) {
            // 这里必须是<而不是<=；
            // 若是<=，最后stack = [0]，而heights末尾的0要入栈，先弹出stack = [],此时栈为空；
            // 接下来执行int left = stack.peek() + 1时会报错；
            while (!stack.empty() && heights_plus[i] < heights_plus[stack.peek()]) {
                int cur = stack.peek();  // 栈顶元素
                stack.pop();
                int left = stack.peek() + 1;
                int right = i - 1;
                res = Math.max((right - left + 1) * heights_plus[cur], res);
            }
            stack.push(i);
        }

        return res;
    }
}
```



















 

 