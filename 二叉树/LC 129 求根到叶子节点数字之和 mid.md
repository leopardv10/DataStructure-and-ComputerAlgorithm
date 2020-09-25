<img src = 'https://github.com/leopardv10/DataStructure-and-ComputerAlgorithm/blob/master/%E4%BA%8C%E5%8F%89%E6%A0%91/images/129-1.png?raw=true' width = 50%>

<img src = 'https://github.com/leopardv10/DataStructure-and-ComputerAlgorithm/blob/master/%E4%BA%8C%E5%8F%89%E6%A0%91/images/129-2.png?raw=true' width = 50%>

### 解法一：递归（先序遍历）

```java
class Solution {
    private int sum = 0;
    
    public int sumNumbers(TreeNode root) {
        if (root == null) return 0;
        helper(root, 0);
        return sum;
    }
    private void helper(TreeNode node, int current) {
        if (node == null) return;  // 递归终止条件1
        current = current * 10 + node.val;
        if (node.left == null && node.right == null) {  // 递归终止条件2：遍历到叶子节点
            sum += current;
            return;
        }
        helper(node.left, current);  //遍历左子树
        helper(node.right, current);  // 遍历右子树
    } 
}
```

### 解法二：DFS（栈），唯一需要在意的是numStack如何push和pop

```java
class Solution {
    public int sumNumbers(TreeNode root) {
        if (root == null) return 0;
        int sum == 0;
        Stack<TreeNode> nodeStack = new Stack<>();
        Stack<Integer> numStack = new Stack<>();
        nodeStack.add(root);
        numStack.add(0);
        
        while (!nodeStack.isEmpty()) {
            TreeNode node = nodeStack.pop();  // 弹出当前node
            int currentVal = 10 * numStack.pop() + node.val;  // 遍历到当前node，当前路径的数值大小
            
            if (node.left != null) {
                nodeStack.add(node.left);
                numStack.add(currenVal);  // 这一步很关键
            }
            if (node.right != null) {
                nodeStack.add(node.right);
                numStack.add(currentVal);  // 这一步很关键
                // 如果当前节点有左右子节点，则需要需要将currenVal向numStack中添加两次
            }
            if (node.left == null && node.right == null) {  // 达到了叶子节点
                sum += currentVal;
            }
        }
        return sum;
    }
```

