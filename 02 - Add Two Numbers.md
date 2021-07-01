[leetcode 02 Add Two Numbers](https://leetcode.com/problems/add-two-numbers/)

解析：在两个链表相加达到末尾时，还需要判断末尾的数是否会产生进位， 所以最后需要判断carry是否大于0。

```java
public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        if (l1 == null || l2 == null) {
            return l1 != null ? l1 : l2;
        }
        ListNode head = null;
        ListNode next = head;
        ListNode firstList = l1;
        ListNode secondList = l2;
        int carry = 0; //进位
        while (firstList != null && secondList != null) {
            int number = firstList.val + secondList.val + carry;
            ListNode node = new ListNode();
            node.val = number % 10;
            carry = number / 10;
            if (head == null) {
                head = node;
            } else {
                next.next = node;
            }
            next = node;
            firstList = firstList.next;
            secondList = secondList.next;
        }

        ListNode remainingList = firstList != null ? firstList : secondList;
        while (remainingList != null) {
            int number = remainingList.val + carry;
            ListNode node = new ListNode();
            node.val = number % 10;
            carry = number / 10;
            next.next = node;
            next = node;
            remainingList = remainingList.next;
        }
  			//判断末尾的数是否产生进位
        if (carry > 0) {
           next.next = new ListNode(carry);
        }
        return head;
    }
```

