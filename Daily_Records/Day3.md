# Day 3: 链表
- **题目 1**：[203. 删除链表元素](https://leetcode.com/problems/remove-linked-list-elements/description/)
  - **知识点**：链表，递归
  - **解题思路**：
    1.  创立虚拟头节点，将current设置为头节点的下一个
    2.  遍历列表，检查下一个节点，而不是当前节点
    3.  删除逻辑：删除时，只修改指针，不移动current（因为要重新检查新的下一个节点）；不删除时，才移动current到下一个节点
    4.  返回结果
  - **代码**：
  ```python
  # Definition for singly-linked list.
  # class ListNode:
  #     def __init__(self, val=0, next=None):
  #         self.val = val
  #         self.next = next
  class Solution:
      def removeElements(self, head: Optional[ListNode], val: int) -> Optional[ListNode]:
          dummy_head = ListNode(next = head) # # 创建虚拟头节点，让所有节点都有"前驱"
  
          current = dummy_head
          while current.next: 
              if current.next.val == val:
                  current.next = current.next.next
              else:
                  current = current.next
          return dummy_head.next
  ```

- **题目 2**：[707. 设计链表](https://leetcode.com/problems/design-linked-list/description/)
  - **知识点**：链表，设计
  - **解题思路**：
    1.  分离链表类和节点类：链表类管理整个链表，节点类存储数据
    2.  使用虚拟头节点：简化头节点操作
    3.  维护链表大小：方便边界检查
  - **代码**：
  ```python
  class ListNode:
      def __init__(self, val=0, next=None):
          self.val = val
          self.next = next
  
  class MyLinkedList:
  
      def __init__(self):
          self.dummy_head = ListNode()
          self.size = 0
  
      def get(self, index: int) -> int:
          if index < 0 or index >= self.size:
              return -1
          current = self.dummy_head.next
          for i in range(index):
              current = current.next
          return current.val
  
      def addAtHead(self, val: int) -> None:
          new_node = ListNode(val)
          new_node.next = self.dummy_head.next
          self.dummy_head.next = new_node
          self.size += 1
  
      def addAtTail(self, val: int) -> None:
          current = self.dummy_head
          while current.next:
              current = current.next
          current.next = ListNode(val)
          self.size += 1
  
      def addAtIndex(self, index: int, val: int) -> None:
          if index < 0 or index > self.size:
              return
          current = self.dummy_head
          for i in range(index):
              current = current.next
          current.next = ListNode(val, current.next)
          self.size += 1
  
      def deleteAtIndex(self, index: int) -> None:
          if index < 0 or index >= self.size:
              return
          
          current = self.dummy_head
          for i in range(index):
              current = current.next
          current.next = current.next.next
          self.size -= 1
  ```
