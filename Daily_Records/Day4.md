# Day 4: 链表

- **题目 1**：[206. 反转链表](https://leetcode.com/problems/reverse-linked-list/description/)
  - **知识点**：链表，递归
  - **解题思路**：
    1.  如果链表为空或只有一个节点，直接返回
    2.   假设我们已经成功反转了从第二个节点开始的子链表
         -  head.next 是原链表的第二个节点
         -  newnode 是反转后子链表的头节点（原链表的尾节点）
    3.   重新连接节点
    4.   返回值
  - **代码**：
  ```python
  # Definition for singly-linked list.
  # class ListNode:
  #     def __init__(self, val=0, next=None):
  #         self.val = val
  #         self.next = next
  class Solution:
      def reverseList(self, head: Optional[ListNode]) -> Optional[ListNode]:
          if head == None or head.next == None:
              return head
          
          newnode = self.reverseList(head.next)
  
          head.next.next = head # 让第二个节点指向第一个节点
          head.next = None # 断开第一个节点与第二个节点的连接
  
          return newnode
  ```

  - **题目 2**：[24. 交换相邻节点](https://leetcode.com/problems/swap-nodes-in-pairs/description/)
  - **知识点**：链表，递归
  - **解题思路**：
    1.  如果链表为空或只有一个节点，直接返回
    2.  保存第二个节点（新的头节点）
    3.  递归剩余部分
    4.  交换当前两个节点
  - **代码**：
  ```python
  # Definition for singly-linked list.
  # class ListNode:
  #     def __init__(self, val=0, next=None):
  #         self.val = val
  #         self.next = next
  class Solution:
      def swapPairs(self, head: Optional[ListNode]) -> Optional[ListNode]:
          if not head or not head.next:
              return head
          new_head = head.next
          head.next = self.swapPairs(head.next.next)
          new_head.next = head
          return new_head
  ```

  - **题目 3**：[19. 从列表末尾删除第 N 个节点](https://leetcode.com/problems/remove-nth-node-from-end-of-list/description/)
  - **知识点**：链表，双指针
  - **解题思路**：
    1.  创建虚拟头节点，空双指针
    2.  fast比slow先走n+1步，再同步移动
    3.  跳过要删除的节点
  - **代码**：
  ```python
  # Definition for singly-linked list.
  # class ListNode:
  #     def __init__(self, val=0, next=None):
  #         self.val = val
  #         self.next = next
  class Solution:
      def removeNthFromEnd(self, head: Optional[ListNode], n: int) -> Optional[ListNode]:
          dummy_head = ListNode(0, head)
          slow, fast = dummy_head, dummy_head
  
          for i in range(n+1):
              fast = fast.next
          
          while fast:
              fast = fast.next
              slow = slow.next
          
          slow.next = slow.next.next
  
          return dummy_head.next
  ```

  - **题目 4**：[160. 两个链表的交点](https://leetcode.com/problems/intersection-of-two-linked-lists/description/)
  - **知识点**：哈希表，链表，双指针
  - **解题思路**：
    1.  两个指针分别从两个链表头开始
    2.  切换链表：当指针到达末尾时，切换到另一个链表
    3.  相遇即相交：如果两链表相交，指针必定会相遇
    4.  如果两链表不相交，指针也会同时指向None
  - **代码**：
  ```python
  # Definition for singly-linked list.
  # class ListNode:
  #     def __init__(self, x):
  #         self.val = x
  #         self.next = None
  
  class Solution:
      def getIntersectionNode(self, headA: ListNode, headB: ListNode) -> Optional[ListNode]:
          if not headA or not headB:
              return None
          pA, pB = headA, headB
          # 当两个指针相遇时停止
          while pA != pB:
              # 如果到达末尾，切换到另一个链表
              pA = headB if pA is None else pA.next
              pB = headA if pB is None else pB.next
          return pA
  ```

  - **题目 n**：[142. 链表循环](https://leetcode.com/problems/linked-list-cycle-ii/description/)
  - **知识点**：哈希表，链表，双指针
  - **解题思路**：
    1.  检测是否有环
    2.  慢指针每次移动1步，快指针每次移动2步，如果有环，快慢指针必定会相遇
    3.  第二步：找到环的起始位置
    4.  当快慢指针相遇后：将其中一个指针重置到链表头，两个指针都改为每次移动1步
    5.  相遇位置距离链表入口距离 = 起始位置到入口距离，再次相遇的位置就是环的起始位置
  - **代码**：
  ```python
  # Definition for singly-linked list.
  # class ListNode:
  #     def __init__(self, x):
  #         self.val = x
  #         self.next = None
  
  class Solution:
      def detectCycle(self, head: Optional[ListNode]) -> Optional[ListNode]:
          slow = fast = head
          while fast and fast.next:
              slow = slow.next
              fast = fast.next.next
              if slow == fast:
                  slow = head
                  while slow != fast:
                      slow = slow.next
                      fast = fast.next
                  return slow
          return None
  ```

  
