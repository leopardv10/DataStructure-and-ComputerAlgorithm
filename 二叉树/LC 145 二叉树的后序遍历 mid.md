<img src = 'https://github.com/leopardv10/DataStructure-and-ComputerAlgorithm/blob/master/%E4%BA%8C%E5%8F%89%E6%A0%91/images/145.png?raw=true' width = 50%>

### 解法一： 递归

### 后序遍历，顾名思义，先遍历左子树，再遍历右子树，最后添加root节点。所以先递归左子树，再递归右子树，最后添加root节点。递归终止条件是当前节点为空。

```java
class Solution {
    private List<Integer> res = new ArrayList<>();

    public List<Integer> postorderTraversal(TreeNode root) {
        recur(root);
        return res;
    }

    private void recur(TreeNode root) {
        if (root == null) return;
        recur(root.left);
        recur(root.right);
        res.add(root.val);
    }
}
```



