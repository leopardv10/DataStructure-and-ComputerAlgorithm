<img src = 'https://github.com/leopardv10/DataStructure-and-ComputerAlgorithm/blob/master/%E6%A0%88/images/lc85.png?raw=true' width = 50%>

### 解法与84题非常相似：

如下图所示，对每一行分别求柱状图中的最大矩形即可

<img src='https://github.com/leopardv10/DataStructure-and-ComputerAlgorithm/blob/master/%E6%A0%88/images/lc85-1.png?raw=true' width=50%>

```java
class Solution {
    public int maximalRectangle(char[][] matrix) {
        if (matrix.length == 0) return 0;

        int[] heights = new int[matrix[0].length];
        int maxArea = 0;
        for (int row = 0; row < matrix.length; row++) {
            for (int col = 0; col < matrix[0].length; col++) {
                if (matrix[row][col] == '1') heights[col] += 1;
                else heights[col] = 0;
            }
            maxArea = Math.max(maxArea, helper(heights));
        }
        return maxArea;
    }

    public int helper(int[] heights) {
        int [] heights_plus = new int[heights.length + 2];
        System.arraycopy(heights, 0, heights_plus, 1, heights.length);
        Stack<Integer> stack = new Stack<>();

        int res = 0;

        for (int i=0; i < heights_plus.length; i++) {
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

