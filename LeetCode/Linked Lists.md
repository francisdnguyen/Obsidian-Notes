- ```python
  # Definition for singly-linked list.
  # class ListNode:
  #     def __init__(self, val=0, next=None):
  #         self.val = val
  #         self.next = next
  ```
- **Reverse Linked List**
	- Given the beginning of a singly linked list `head`, reverse the list, and return the new beginning of the list.
	- Save the next node. Reverse the pointer of the current node to prev. Move current node to prev node. Move temp node to current node. (Iteration)
	- ```python
	  def reverseList(self, head: Optional[ListNode]) -> Optional[ListNode]:
		  prev, curr = None, head
		  while curr:
			  temp = curr.next #store next
			  curr.next = prev #reverse current node's next pointer
			  prev = curr #move pointers one up
			  curr = temp #move pointers one up
		  return prev
	  ```
	- Uses the call stack to naturally reverse the direction of the pointers. (Recursion)
	- ```python
	  def reverseList(self, head: Optional[ListNode]) -> Optional[ListNode]:
		  if not head:
			  return None
		  newHead = head
		  if head.next:
			  newHead = self.reverseList(head.next)
			  head.next.next = head
		  head.next = None
		  return newHead
	  ```
- **Merge Two Sorted Lists**
	- You are given the heads of two sorted linked lists `list1` and `list2`. Merge the two lists into one **sorted** linked list and return the head of the new sorted linked list. The new list should be made up of nodes from `list1` and `list2`.
	- Pick the smaller node, recursively merge the rest of the lists, then attach result to the chosen node. (Recursion)
	- ```python
	  def mergeTwoLists(self, list1: Optional[ListNode], list2: Optional[ListNode]) -> Optional[ListNode]:
		  if list1 is None:
			  return list2
		  if list2 is None:
			  return list1
		  if list1.val <= list2.val:
			  list1.next = self.mergeTwoLists(list1.next, list2)
			  return list1
		  else:
			  list2.next = self.mergeTwoLists(list1, list2.next)
			  return list2
	  ```
	- Iteration
	- ```python
	  def mergeTwoLists(self, list1: Optional[ListNode], list2: Optional[ListNode]) -> Optional[ListNode]:
		  dummy = node = ListNode()
		  while list1 and list2:
			  if list1.val <= list2.val:
				  node.next = list1
				  list1 = list1.next
			  else:
				  node.next = list2
				  list2 = list2.next
			  node = node.next
	     node.next = list1 or list2
	     return dummy.next
	  ```
- **Linked List Cycle**
	- e
	- slow moves one step at a time, fast moves two steps at a time
	- ```python
	  def hasCycle(self, head: Optional[ListNode]) -> bool:
		  slow, fast = head, head
		  while fast and fast.next:
			  slow = slow.next
			  fast = fast.next.next
			  if slow == fast:
				  return True
		  return False
	  ```
- **Reorder List**
	-  In the general case for a list of `length = n` the nodes are reordered to be in the following order: `[0, n-1, 1, n-2, 2, n-3, ...]`
	- Find middle using slow and fast pointers. Reverse second half of the list. Merge two halves one by one.
	- ```python
	  def reorderList(self, head: Optional[ListNode]) -> None:
		  slow, fast = head, head
		  while fast and fast.next:
			  slow = slow.next
			  fast = fast.next.next
		  second = slow.next
		  prev = slow.next = None
		  while second:
			  temp = second.next
			  second.next = prev
			  prev = second
			  second = temp
		  first, second = head, prev
		  while second:
			  temp1, temp2 = first.next, second.next
			  first.next = second
			  second.next = temp1
			  first, second = temp1, temp2
	  ```
- **Remove Nth Node from End of List**
	- Given the `head` of a linked list and an integer `n`, remove the `nth` node from the end of the list and return its head.
	- Two pointers where the second pointer is n away from the first. We traverse to the end of the list and the first pointer will be at the nth node
	- ```python
	  def removeNthFromEnd(self, head: Optional[ListNode], n: int) -> Optional[ListNode]:
	  dummy = ListNode(0, head)
	  left = dummy
	  right = head
	  while n > 0
		  right = right.next
		  n -= 1
	  while right:
		  left = left.next
		  right = right.next
	  left.next = left.next.next
	  return dummy.next
	  ```
	- Recursion (Put n inside a list since it is mutable, integers are not)
	- ```python
	  def removeNthFromEnd(self, head: Optional[ListNode], n: int) -> Optional[ListNode]:
		  def rec(head, n)
			  if not head:
				  return None
			  head.next = rec(head.next, n)
			  n[0] -= 1
			  if n[0] == 0:
				  return head.next
			  return head
		  return rec(head, [n])
	  ```
- **Copy List With Random Pointer**
	- You are given the head of a linked list of length `n`. Unlike a singly linked list, each node contains an additional pointer `random`, which may point to any node in the list, or `null` Create a **deep copy** of the list.
	- Creates a hash map and we traverse the list copying each item as we go.
	- ```python
	  def copyRandomList(self, head: 'Optional[Node]') -> 'Optional[Node]':
		  oldToCopy = collections.defaultdict(lambda: None(0))
		  oldToCopy[None] = None
		  cur = head
		  while cur:
			  oldToCopy[cur].val = cur.val
			  oldToCopy[cur].next = oldToCopy[cur.next]
			  oldToCopy[cur].random = oldToCopy[cur.random]
			  cur = cur.next
		  return oldToCopy[head]
	  ```
- **Add 2 Numbers**
	- w
	- w
	- ```python
	  def addTwoNumbers(self, l1: Optional[ListNode], l2: Optional[ListNode]) -> Optional[ListNode]:
		  
	  ```
- **Find the Duplicate Number**
- **LRU Cache**