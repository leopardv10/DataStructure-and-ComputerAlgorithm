<img src='https://github.com/leopardv10/DataStructure-and-ComputerAlgorithm/blob/master/%E4%BA%8C%E5%8F%89%E6%A0%91/images/117-1.png?raw=true' width=50%> 

<img src = 'https://github.com/leopardv10/DataStructure-and-ComputerAlgorithm/blob/master/%E4%BA%8C%E5%8F%89%E6%A0%91/images/117-2.png?raw=true' width=50%>

### 思路与116类似，只不过从完全二叉树变成普通二叉树，因此要考虑son node为空的情况；

### 解法一 BFS（队列，和116几乎一样）：

```java
class Solution {
    public Node connect(Node root) {
        if (root == null) return root;
        LinkedList<Node> queue = new LinkedList();
        queue.add(root);

        while (queue.size() > 0) {
            int size = queue.size();
            Node tmp = queue.get(0);  // 先取queue[0]
            
            for (int i=1; i < size; i++) {  // 此处从i=1开始
                tmp.next = queue.get(i);
                tmp = tmp.next;
            }

            for (int i=0; i < size; i++) {
                tmp = queue.remove(0);  // 这里每次都删除队列首位元素
                if (tmp.left != null) {
                    queue.add(tmp.left);
                }
                if (tmp.right != null) {
                    queue.add(tmp.right);
                }
            }
        }
        return root;
    }
}
```

### 解法二  迭代：

cur代表当前层的node，我们通过遍历当前层来将下一层的节点连接起来；

这里要使用dummy结点，因为我们不知道下一层会从哪个node开始，所以dummy.next指向下一层的开始结点；

```java
class Solution {
    public Node connect(Node root) {
        Node cur = root;
        //这个while循环用来遍历树的深度
        while (cur != null) {
            Node dummy = new Node();
            Node tail = dummy;
            // 这个while循环用来遍历当前层
            while (cur != null) {
                if (cur.left != null) {
                    tail.next = cur.left;
                    tail = tail.next;
                }
                if (cur.right != null) {
                    tail.next = cur.right;
                    tail = tail.next;
                }
                cur = cur.next;
            }
            cur = dummy.next;
        }
        return root;
    }
}
```

### 解法三  递归：

有两个要点：

1. assist函数用来寻找 .next应该指向的**非空**结点
2. 先递归遍历root.right后遍历root.left，因为对当前层的.next赋值时，总是去遍历上一层的右侧结点，而不是左侧，所以要先构建右子树

```java
class Solution {
    public Node connect(Node root) {
        if (root == null || (root.left == null && root.right == null)) return root;
        if (root.left != null && root.right != null) {
            root.left.next = root.right;
            root.right.next = assist(root);
        }
        if (root.left == null) {
            root.right.next = assist(root);
        }
        if (root.right == null) {
            root.left.next = assist(root);
        }
        
        root.right = connect(root.right);
        root.left = connect(root.left);

        return root;
    }

    public Node assist(Node root) {
        while (root.next != null) {
            if (root.next.left != null) return root.next.left;
            if (root.next.right != null) return root.next.right;
            root = root.next;
        }
        return null;
    }
}
```



