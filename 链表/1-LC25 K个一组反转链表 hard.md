<img src = 'https://github.com/leopardv10/DataStructure-and-ComputerAlgorithm/blob/master/%E9%93%BE%E8%A1%A8/images/LC25.png?raw=true' width = 40%>

### 方法一：使用栈临时存储每组nodes，顺序入栈，反序出栈，以此达到反转的目的，需额外空间为k  。

```python
class Solution:
    def reverseKGroup(self, head: ListNode, k: int) -> ListNode:
        p = dummy = ListNode(0)  # dummy用来指向反转后的链表的头节点，在链表题中极其常见
        stack = []
        
        while True:
            count, tmp = 1, head  
            while tmp and count <= k:  # count从1增至k+1
                stack.append(tmp)
                count += 1
                tmp = tmp.next  # eg：第一组nodes遍历完后tmp为第二组nodes的1st node
            if count != k + 1:  # 说明这一组nodes数量已经不够k个，因此不需要反转
                p.next = head
                break
            while stack:  # 弹出stack中的nodes以达到反转的目的
                p.next = stack.pop()
                p = p.next  # [1, 2, 5]，依次弹出5->2->1，p最后为1这个node
            head = tmp
        return dummy.next
```

>     此种解法使用三个指针:p,tmp,head;
>     head的作用是在于当最后一组不足K个nodes时，通过p.next = head将前面已反转的nodes和后面未反转的nodes连接起来；
>     tmp的作用是遍历原链表，将每组nodes放入stack中；
>     p的作用是连接stack中弹出的nodes，使其逆序。

### 方法二：递归  

