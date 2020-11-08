<img src='https://github.com/leopardv10/DataStructure-and-ComputerAlgorithm/blob/master/%E4%BA%8C%E5%8F%89%E6%A0%91/images/%E5%89%91%E6%8C%8707.png?raw=true' width=50%>

### 解题思路：

前序遍历：[根节点，左子树，右子树]

中序遍历：[左子树，根节点，右子树]

1. so, 在前序遍历中可直接得到root.value，根据root.value找到root在中序遍历中的位置；
2. 有了root在中序遍历中的位置，可得左子树&右子树长度；
3. 据此，在前序遍历中可对应出左子树和右子树的位置；
4. root.left = 前序左子树第一个节点，root.right = 前序右子树第一个节点，依次递归；

```java
class Solution {
    int[] preorder;
    // hashmap的作用是保存inorder中node.val与index的对应关系；
    HashMap<TreeNode> hash = new HashMap<>();
    
    public TreeNode buildTree(int[] preorder, int[] inorder) {
        this.preorder = preorder;
    	for(int i = 0; i < inorder.length; i++) {
            hash.put(inorder[i], i);  // node.val: index
        }
        return recur(0, 0, preorder.length - 1);
    }
    
    // root->前序中根节点的index，(l, r)中序中当前子树的起始和结束index
    public TreeNode recur(int root, int l, int r) {
        if(l > r) return null;
        TreeNode node = new TreeNode(preorder[root]);
        int i = hash.get(preorder[root]);  // 找到inorder中root的位置
        node.left = recur(root + 1, l, i - 1);
        node.right = recur(root + i - l + 1, i + 1, r);
        return node;
    }
}
```

