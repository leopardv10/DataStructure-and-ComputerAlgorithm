<img src = 'https://github.com/leopardv10/DataStructure-and-ComputerAlgorithm/blob/master/%E9%93%BE%E8%A1%A8/images/LC147-1.png?raw=true' width = 50%>

<img src = 'https://github.com/leopardv10/DataStructure-and-ComputerAlgorithm/blob/master/%E9%93%BE%E8%A1%A8/images/LC147-2.png?raw=true' width = 50%>

### 本题使用插入排序，方法很简单，关键在于指针的指向不要出错。

1. 使用双指针，pSlow & pFast 来遍历链表，pSlow指向前一个元素，pFast指向后一个元素；

   若pFast < pSlow则存在逆序，eg：4->3；3需要放到4前面。

2. 存在逆序时需要将pFast插入到pSlow前面某处，pre指针的作用便是用来确定插入位置。

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def insertionSortList(self, head: ListNode) -> ListNode:
        pre = pSlow = dummy = ListNode(float('-inf'))
        dummy.next = head
        pFast = head

        while pFast:
            if pSlow.val < pFast.val:  # 不存在逆序时，pSlow和pFast都向后移动一位
                pSlow, pFast = pSlow.next, pFast.next
            else:  # 存在逆序
                tmp = pFast.next  # eg: 3->2->4，此时PSlow = 3，pFast=2，tmp = 4
                pSlow.next = tmp  # 将3与4连接起来，即3->4，然后将2移到3前面
                # 使用pre指针寻找插入位置，eg:1->2->4->3，则3要插入到2后面
                while pre.next.val < pFast.val:  # 一开始p为dummy，p.next为头节点
                    pre = pre.next
                # 此时pre.val < pFast.val，而pre.next.val > pFast.val
                pre.next, pFast.next = pFast, pre.next
                pre = dummy
                pFast = tmp
        return dummy.next
```





