<img src='https://github.com/leopardv10/DataStructure-and-ComputerAlgorithm/blob/master/%E5%8F%8C%E6%8C%87%E9%92%88/images/142-1.png?raw=true' width = 50%>

<img src='https://github.com/leopardv10/DataStructure-and-ComputerAlgorithm/blob/master/%E5%8F%8C%E6%8C%87%E9%92%88/images/142-2.png?raw=true' width=50%>

### 双指针法：

1. 设非环部分长度为a，环状部分长度为b
2. 设快指针fast，慢指针slow，快指针走两步，慢指针走一步，当快慢指针在环状部分第一次相遇时，fast比slow多走n * b步（n是常数）；
3. 假设slow指针走了a + x步，则fast指针走了2a + 2x = a + x + n * b----->得a + x = n * b, 2 * (a + x) = 2n * b；
4. 此时slow指针若想走到链表环的开始还需走a步，**将fast指针重新放在链表开头**，让其也走a步则会和slow相遇。此时相遇的节点为环的开始节点。

```java
public class Solution {
    public ListNode detectCycle(ListNode head) {
        ListNode fast = head, slow = head;
        while (true) {
            if (fast == null || fast.next == null) return null;
            fast = fast.next.next;
            slow = slow.next;
            if (fast == slow) break;
        }
        fast = head;
        while (slow != fast) {
            slow = slow.next;
            fast = fast.next;
        }
        return fast;
    }
}
```





