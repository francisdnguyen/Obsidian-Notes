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
	- Given the beginning of a linked list `head`, return `true` if there is a cycle in the linked list. Otherwise, return `false`.
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
		  oldToCopy = collections.defaultdict(lambda: Node(0))
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
	- You are given two **non-empty** linked lists, `l1` and `l2`, where each represents a non-negative integer. The digits are stored in **reverse order**, e.g. the number 321 is represented as `1 -> 2 -> 3 ->` in the linked list. Return the sum of the two numbers as a linked list.
	- Recursion since lists are stored in reverse order. Keep a carry for addition.
	- ```python
	  def addTwoNumbers(self, l1: Optional[ListNode], l2: Optional[ListNode]) -> Optional[ListNode]:
		  def add(l1, l2, carry)
			  if l1 is None and l2 is None and carry == 0:
				  return None
			  val1 = l1.val if l1 else 0
			  val2 = l2.val if l2 else 0
			  total = val1 + val2 + carry
			  carry, val = divmod(total, 10)
			  next_node = add(l1.next if l1 else None, 
							  l2.next if l2 else None, carry)
			  return ListNode(val, next_node)
	  return add(l1, l2, 0)
	  ```
	  - Iteration
	  - ```python
	    def addTwoNumbers(self, l1: Optional[ListNode], l2: Optional[ListNode]) -> Optional[ListNode]:
		    dummy = cur = ListNode()
		    while l1 or l2 or carry:
			    v1 = l1.val if l1 else 0
			    v2 = l2.val if l2 else 0
			    total = v1 + v2 + carry
			    carry = total // 10
			    val = total % 10
			    cur.next = ListNode(val)
			    cur = cur.next
			    l1 = l1.next if l1 else None
			    l2 = l2.next if l2 else None
			return dummy.next
	    ```
- **Find the Duplicate Number**
	- You are given an array of integers `nums` containing `n + 1` integers. Each integer in `nums` is in the range `[1, n]` inclusive. There is exactly **one repeated integer** in `nums`, and every other integer appears at most once. Return the repeated integer.
	- Because one number is duplicated, two indices will point into the **same chain**, creating a **cycle** — exactly like a linked list with a loop.
	- ```python
	  def findDuplicate(self, nums: List[int]) -> int:
		  slow, slow2, fast = 0, 0, 0
		  while True:
			  slow = nums[slow]
			  fast = nums[nums[fast]]
			  if slow == fast:
				  break
		  while True:
			  slow = nums[slow]
			  slow2 = nums[slow2]
			  if slow == slow2:
				  return slow
	  ```
- **Merge K Sorted Lists**
	- You are given an array of `k` linked lists `lists`, where each list is sorted in ascending order. Return the **sorted** linked list that is the result of merging all of the individual linked lists.
	- We divide and conquer. We iterate through the lists and merge two lists at a time and we keep going until the length is 1.
	- ```python
	  def mergeKLists(self, lists: List[Optional[ListNode]]) -> Optional[ListNode]:
		  def mergeList(self, l1, l2):
			  dummy = node = ListNode()
			  while l1 and l2:
				  if l1.val < l2.val:
					  node.next = l1
					  l1 = l1.next
				  else:
					  node.next = l2
					  l2 = l2.next
				  node = node.next
			  node.next = l1 or l2
			  return dummy.next
		  
		  if not lists or len(lists) == 0:
			  return None
		  while len(lists) > 1:
			  mergedLists = []
			  for i in range(0, len(lists), 2):
				  l1 = lists[i]
				  l2 = lists[i + 1] if (i + 1) < len(lists) else None
				  mergedLists.append(mergeList(l1, l2))
			  lists = mergedLists
		  return lists[0]	  
	  ```
	- **Reverse Nodes in K-Group**
		- You are given the head of a singly linked list `head` and a positive integer `k`. You must reverse the first `k` nodes in the linked list, and then reverse the next `k` nodes, and so on. If there are fewer than `k` nodes left, leave the nodes as they are. Return the modified list after reversing the nodes in each group of `k`.
		- Recursion
		- ```python
			  def reverseKGroup(self, head: Optional[ListNode], k: int) -> Optional[ListNode]:
			  curr = head
			  group = 0
			  while curr and group < k:
				  curr = curr.next
				  group += 1
			  if group == k:
				  curr = reverseKGroup(curr, k)
				  while group > 0:
					  temp = head.next
					  head.next = curr
					  curr = head
					  head = temp
					  group -= 1
				  head = curr
			  return head
		  ```