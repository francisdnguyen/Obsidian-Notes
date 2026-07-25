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
	- DFS recursion
	- ```python
	  def isSubtree(self, root: Optional[TreeNode], subRoot: Optional[TreeNode]) -> bool:
		  def sameTree(root, subRoot):
			  if not root and not subRoot:
				  return True
			  if root and subRoot and root.val == subRoot.val:
				  return (sameTree(root.left, subRoot.left) 
					  and sameTree(root.right, subRoot.right))
			  return False
		  if not subRoot:
			  return True
		  if not root:
			  return False
		  if sameTree(root, subRoot):
			  return True
		  return (self.isSubtree(root.left, subRoot) 
			  or self.isSubtree(root.right, subRoot))
	  ```
  - **Lowest Common Ancestor in BST**
	  - Given a binary search tree (BST) where all node values are unique, and two nodes from the tree p and q, return the lowest common ancestor (LCA) of the two nodes.
	  - Iteration
	  - ```python
	    def lowestCommonAncestor(self, root: TreeNode, p: TreeNode, q: TreeNode) -> TreeNode:
		    curr = rot
		    while curr:
				    if p.val > curr.val and q.val > curr.val:
					    curr = curr.right
					elif p.val < curr.val and q.val < curr.val:
						curr = curr.left
					else:
						return curr
	    ```
	- **Binary Tree Level Order Traversal**
		- Given a binary tree root, return the level order traversal of it as a nested list, where each sublist contains the values of nodes at a particular level in the tree, from left to right.
		- bfs
		- ```python
		  def levelOrder(self, root: Optional[TreeNode]) -> List[List[int]]:
			  res = []
			  q = deque([root])
			  while q:
				  level = []
				  for i in range(len(q)):
					  node = q.popleft()
					  if node:
						  level.append(node.val)
						  q.append(node.left)
						  q.append(node.right)
				  if level:
					  res.append(level)
			  return res  
		  ```
		  - dfs
		  - ```python
		    def levelOrder(self, root: Optional[TreeNode]) -> List[List[int]]:
			    res = []
			    def dfs(node, depth):
				    if not node:
					    return None
					if len(res) == depth:
						res.append([])
					res[depth].append(node.val)
					dfs(node.left, depth + 1)
					dfs(node.right, depth + 1)
				dfs(root, 0)
				return res
		    ```
	- **Binary Tree Right Side View**
		- You are given the `root` of a binary tree. Return only the values of the nodes that are visible from the right side of the tree, ordered from top to bottom.
		- dfs
		- ```python
		  def rightSideView(self, root: Optional[TreeNode]) -> List[int]:
			  res = []
			  def dfs(node, depth):
				  if not node:
					  return None
				  if depth == len(res):
					  res.append(node.val)
				  dfs(node.right, depth + 1)
				  dfs(node.left, depth + 1)
			  dfs(root, 0)
		  ```
		  - bfs
		  - ```python
		    def rightSideView(self, root: Optional[TreeNode]) -> List[int]:
			    res = []
			    q = deque([root])
			    while q:
				    rightSide = None
				    for i in range(len(q)):
					    node = q.popleft()
					    if node:
						    rightSide = node
						    q.append(node.left)
						    q.append(node.right)
					if rightSide:
						res.append(rightSide.val)
				return res
		    ```
	- **Count Good Nodes in Binary Tree**
		- Within a binary tree, a node `x` is considered **good** if the path from the root of the tree to the node `x` contains no nodes with a value greater than the value of node `x` Given the root of a binary tree `root`, return the number of **good** nodes within the tree.
		- dfs
		- ```python
		  def goodNodes(self, root: TreeNode) -> int:
			  def dfs(node, maxVal):
				  if not node:
					  return 0
				  res = 1 if node.val >= maxVal else 0
				  maxVal = max(maxVal, node.val)
				  res += dfs(node.left, maxVal)
				  res += dfs(node.right, maxVal)
				  return res
			  dfs(root, root.val)
		  ```
		  - bfs
		  - ```python
		    def goodNodes(self, root: TreeNode) -> int:
			    res = 0
			    q = deque([root, float('-infinity')])'
			    while q:
				    node, maxval = q.popleft()
				    if node.val >= maxval:
					    res += 1
					if node.left:
						q.append((node.left, max(maxval, node.val)))
					if node.right:
						q.append((node.right, max(maxval, node.val)))
				return res
		    ```
	- **Validate BST**
		- Given the `root` of a binary tree, return `true` if it is a **valid binary search tree**, otherwise return `false`.
		- dfs
		- ```python
		  def isValidBST(self, root: Optional[TreeNode]) -> bool:
			  def dfs(node, left, right):
				  if not node:
					  return True
				  if not (left < node.val < right):
					  return False
				  return dfs(node.left, left, node.val)
					  and dfs(node.right, node.val, right)
			  return dfs(root, float("-infinity"), float("infinity"))
		  ```
		  - bfs
		  - ```python
		    def isValidBST(self, root: Optional[TreeNode]) -> bool:
			    if not root:
				    return True
				q = deque([(root, float("-infinity"), float("infinity"))])
				while q:
					node, left, right = q.popleft()
					if not (left < node.val < right):
						return False
					if node.left:
						q.append((node.left, left, node.val))
					if node.right:
						q.append((node.right, node.val, right))
				return True
		    ```
	- **Kth Smallest Element in a BST**
		- Given the `root` of a binary search tree, and an integer `k`, return the `kth` smallest value (**1-indexed**) in the tree.
		- Iterative dfs
		- ```python
		  def kthSmallest(self, root: Optional[TreeNode], k: int) -> int:
			  stack = []
			  curr = root
			  while stack or curr:
				  while curr:
					  stack.append(curr)
					  curr = curr.left
				  curr = stack.pop()
				  k -= 1
				  if k == 0:
					  return curr.val
				  curr = curr.right
		  ```
		  - recursive dfs
		  - ```python
		    def kthSmallest(self, root: Optional[TreeNode], k: int) -> int:
			    count = k
			    res = root.val
			    def dfs(node):
				    nonlocal count, res
				    if not node:
					    return
					dfs(node.left)
					if cnt == 0:
						return
					cnt -= 1
					if cnt == 0:
						res = node.val
						return
					dfs(node.right)
				dfs(root)
				return res
		    ```
	- **Construct Binary Tree from Preorder and Inorder Traversal**
		- You are given two integer arrays `preorder` and `inorder`. `preorder` is the preorder traversal of a binary tree `inorder` is the inorder traversal of the same tree. Both arrays are of the same size and consist of unique values. Rebuild the binary tree from the preorder and inorder traversals and return its root.
		- dfs
		- ```python
		  def buildTree(self, preorder: List[int], inorder: List[int]) -> Optional[TreeNode]:
			  preIdx, inIdx = 0, 0
			  def dfs(limit):
				  nonlocal preIdx, inIdx
				  if preIdx >= (preorder):
					  return None
				  if inorder[inIdx] == limit:
					  inIdx += 1
					  return None
				  root = TreeNode(preorder[preIdx])
				  preIdx += 1
				  root.left = dfs(root.val)
				  root.right = dfs(limit)
				  return root
			  return dfs(float('infinity'))
		  ```
	- **Binary Tree Maximum Path Sum**
		- Given the `root` of a _non-empty_ binary tree, return the maximum **path sum** of any _non-empty_ path.
		- dfs
		- ```python
		  def maxPathSum(self, root: Optional[TreeNode]) -> int:
			  res = [root.val]
			  def dfs(root):
				  if not root:
					  return 0
				  leftMax = dfs(root.left)
				  rightMax = dfs(root.right)
				  leftMax = max(leftMax, 0)
				  rightMax = max(rightMax, 0)
				  res[0] = max(res[0], root.val + leftMax + rightMax)
				  return root.val + max(leftMax, rightMax)
			  dfs(root)
			  return res[0]
		  ```
	- **Serialize and Deserialize Binary Tree**
		- Implement an algorithm to serialize and deserialize a binary tree.
		- dfs preorder
		- ```python
		  def serialize(self, root: Optional[TreeNode]) -> str:
			  res = []
			  def dfs(node):
				  if not node:
					  res.append("N")
					  return
				  res.append(str(node.val))
				  dfs(node.left)
				  dfs(node.right)
			  dfs(root)
			  return ",".join(res)
		  def deserialize(self, data: str) -> Optional[TreeNode]:
			  vals = data.split(",")
			  self.i = 0
			  def dfs():
				  if vals[self.i] == "N":
					  self.i += 1
					  return None
				  node = TreeNode(int(vals[self.i]))
				  self.i += 1
				  node.left = dfs()
				  node.right = dfs()
				  return node
			  return dfs()
		  ```