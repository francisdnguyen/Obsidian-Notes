- # class TreeNode:

#     def __init__(self, val=0, left=None, right=None):

#         self.val = val

#         self.left = left

#         self.right = right
- **Invert Binary Tree**
	- You are given the root of a binary tree `root`. Invert the binary tree and return its root.
	- Recursion, switching every left and right node DFS
	- ```python
	  def invertTree(self, root: Optional[TreeNode]) -> Optional[TreeNode]:
		  if not root:
			  return None
		  root.left, root.right = root.right, root.left
		  self.invertTree(root.left)
		  self.invertTree(root.right)
		  return root
	  ```
	  - BFS with a deque
	  - ```python
	    def invertTree(self, root: Optional[TreeNode]) -> Optional[TreeNode]:
		    if not root:
			    return None
			queue = deque([root])
			while queue:
				node = queue.popleft()
				node.left, node.right = node.right, node.left
				if node.left:
					queue.append(node.left)
				if node.right:
					queue.append(node.right)
			return root
	    ```
- **Maximum Depth of Binary Tree
	- Given the `root` of a binary tree, return its **depth**. The **depth** of a binary tree is defined as the number of nodes along the longest path from the root node down to the farthest leaf node.
	- DFS using recursion
	- ```python
	  def maxDepth(self, root: Optional[TreeNode]) -> int:
		  if not root:
			  return 0
		  return 1 + max(self.maxDepth(root.left), self.maxDepth(root.right))
	  ```
	- DFS iterative
	- ```python
	  def maxDepth(self, root: Optional[TreeNode]) -> int:
		  stack = [(root, 1)]
		  maxDepth = 0
		  while stack:
			  node, depth = stack.pop()
			  if node:
				  maxDepth = max(maxDepth, depth)
				  stack.append([root.left, depth + 1])
				  stack.append([root.right, depth + 1])
		  return maxDepth
	  ```
	  - BFS with a queue
	  - ```python
	    def maxDepth(self, root: Optional[TreeNode]) -> int:
		    if not root:
			    return 0
			q = deque([root])
			level = 0
			while q:
				for i in range(len(q)):
					node = q.popleft()
					if node.left:
						q.append(node.left)
					if node.right:
						q.append(node.right)
				level += 1
			return level
	    ```
- **Diameter of Binary Tree**
	- Given the root of a binary tree `root`, return the **diameter** of the tree.
	- DFS Recursion
	- ```python
	  def diameterOfBinaryTree(self, root: Optional[TreeNode]) -> int:
		  res = 0
		  def dfs(root):
			  nonlocal res
			  if not root:
				  return None
			  left = dfs(root.left)
			  right = dfs(root.right)
			  res = max(res, left + right)
			  return 1 + max(left, right)
		  dfs(root)
		  return res
	  ```
- **Balanced Binary Tree**
	- Given a binary tree, return `true` if it is **height-balanced** and `false` otherwise.
	- DFS recursion
	- ```python
	  def isBalanced(self, root: Optional[TreeNode]) -> bool:
		  def dfs(root):
			  if not root:
				  return [True, 0]
			  left, right = dfs(root.left), dfs(root.right)
			  balanced = left[0] and right[0] and abs(left[1] - right[1]) <= 1
			  return [balanced, 1 + max(left[1], right[1])]
		  return dfs(root)[0]
	  ```
	  - DFS Iterative postorder traversal
	  - ```python
	    def isBalanced(self, root: Optional[TreeNode]) -> bool:
		    stack = []
		    node = root
			last = None
			depths = {}
			while stack or node:
				if node:
					stack.append(node)
					node = node.left
				else:
					node = stack[-1]
					if not node.right or last == node.right:
						stack.pop()
						left = depths.get(node.left, 0)
						right = depths.get(node.right, 0)
						if abs(left - right) > 1:
							return False
						depths[node] = 1 + max(left, right)
						last = node
						node = None
					else:
						node = node.right
				return True
	    ```
- **Same Tree**
	- Given the roots of two binary trees `p` and `q`, return `true` if the trees are **equivalent**, otherwise return `false`.
	- dfs (recursion)
	- ```python
	  def isSameTree(self, p: Optional[TreeNode], q: Optional[TreeNode]) -> bool:
		  if not p and not q:
			  return True
		  if p and q and p.val == q.val:
			  return self.isSameTree(p.left, q.left) and self.isSameTree(p.right, q.right)
		  else:
			  return False
	  ```
	  - dfs (iteration)
	  - ```python
	    def isSameTree(self, p: Optional[TreeNode], q: Optional[TreeNode]) -> bool:
	    stack = [(p, q)]
	    while stack:
		    node1, node2 = stack.pop()
		    if not node1 and node2:
			    continue
			if not node1 or not node2 or node1.val != node2.val:
				return False
			stack.append((node1.left, node2.left))
			stack.append((node1.right, node2.right))
		return True
	    ```
	    - bfs (queue)
	    - ```python
	      def isSameTree(self, p: Optional[TreeNode], q: Optional[TreeNode]) -> bool:
		      q1 = deque([p])
		      q2 = deque([q])
		      while q1 and q2:
			      for _ in range(len(q1)):
				      nodeP = q1.popleft()
				      nodeQ = q2.popleft()
				      if nodeP is None and nodeQ is None:
					      continue
					  if nodeP is None or nodeQ is None or nodeP.val != nodeQ.val:
						  return False
					  q1.append(nodeP.left)
					  q1.append(nodep.right)
					  q2.append(nodeQ.left)
					  q2.append(nodeQ.right)
			  return True
	      ```
- **Subtree of Another Tree**
	- Given the roots of two binary trees `root` and `subRoot`, return `true` if there is a subtree of `root` with the same structure and node values of `subRoot` and `false` otherwise.
	- w
	- ```python
	  def isSubtree(self, root: Optional[TreeNode], subRoot: Optional[TreeNode]) -> bool:
	  
	  ```