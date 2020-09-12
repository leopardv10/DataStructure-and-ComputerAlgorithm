<img src = 'https://github.com/leopardv10/DataStructure-and-ComputerAlgorithm/blob/master/%E4%BA%8C%E5%8F%89%E6%A0%91/images/116-1.png?raw=true' width=80%>

<img src = 'https://github.com/leopardv10/DataStructure-and-ComputerAlgorithm/blob/master/%E4%BA%8C%E5%8F%89%E6%A0%91/images/116-2.png?raw=true' width=80%>

### 解法一：BFS(队列，不符合题目常数级空间复杂度要求)

```java
class Solution {
    public Node connect(Node root) {
        if (root == null) return root;
        LinkedList<Node> queue = new LinkedList();
        queue.add(root);

        while (queue.size() > 0) {
            int size = queue.size();
            Node tmp = queue.get(0);
            
            for (int i=1; i<size; i++) {  // 先对当前队列中的元素进行next赋值
                tmp.next = queue.get(i);
                tmp = queue.get(i);
            }

            for (int i=0; i<size; i++) {  // 将当前层的node全部删除，再加入下一层node
                tmp = queue.remove(0);
                if (tmp.left != null) {
                    queue.add(tmp.left);
                    queue.add(tmp.right);
                }
            }
        }
        return root;
    }
}
```

### 解法二：迭代

```java
class Solution {
    public Node connect(Node root) {
        if (root == null) return root;
        Node pre = root;
        
        while (pre.left != null) {
            Node tmp = pre;
            while (tmp != null) {
                tmp.left.next = tmp.right;
                if (tmp.next != null) {
                    tmp.right.next = tmp.next.left;
                } 
                tmp = tmp.next;
            }
            pre = pre.left;
        }
        return root;
    }
}
```

**详细过程如下：**

<img src  ='https://github.com/leopardv10/DataStructure-and-ComputerAlgorithm/blob/master/%E4%BA%8C%E5%8F%89%E6%A0%91/images/lc116.gif?raw=true'>

### 解法三：递归

```java
class Solution {
    public Node connect(Node root) {
        return dfs(root);
    }

    private Node dfs(Node root) {
        if (root == null) return root;

        Node left = root.left;
        Node right = root.right;

        while (left != null) {
            left.next = right;
            left = left.right;
            right = right.left;
        }

        root.left = dfs(root.left);
        root.right = dfs(root.right);

        return root;
    }
}
```

**具体过程如下图：**

<img src = 'https://github.com/leopardv10/DataStructure-and-ComputerAlgorithm/blob/master/%E4%BA%8C%E5%8F%89%E6%A0%91/images/lcc116-3.gif?raw=true'>