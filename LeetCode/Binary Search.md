- **Binary Search**
	- You are given an array of **distinct** integers `nums`, sorted in ascending order, and an integer `target`. Implement a function to search for `target` within `nums`. If it exists, then return its index, otherwise, return `-1`.
	- Core binary search. Checks the middle element of a sorted array and decides which half to discard. We adjust the left and right pointers until we either find the target or the pointers cross, meaning the target isn’t present.
	- ```python
	  def search(self, nums: List[int], target: int) -> int:
		  l, r = 0, len(nums) - 1
		  while l <= r:
			  m = l + ((r - l) // 2)
			  if nums[m] < target:
				  l = m + 1
			  elif nums[m] > target:
				  r = m - 1
			  else:
				  return m
		  return -1
	  ```
- **Search a 2D Matrix**
	- You are given an `m x n` 2-D integer array `matrix` and an integer `target`. Each row in `matrix` is sorted in _non-decreasing_ order. The first integer of every row is greater than the last integer of the previous row. Return `true` if `target` exists within `matrix` or `false` otherwise.
	- If we imagine flattening the matrix into a single list, the order of elements doesn't change. This means we can run **one binary search** from index `0` to `ROWS * COLS - 1`
	- ```python
	  def searchMatrix(self, matrix: List[List[int]], target: int) -> bool:
		  rows, cols = len(matrix), len(matrix[0])
		  l, r = 0, rows * cols - 1
		  while l <= r:
			  m = l + ((r - l) // 2)
			  row, col = m // cols, m % cols
			  if target > matrix[row][col]:
				  l = m + 1
			  elif target < matrix[row][col]:
				  r = m - 1
			  else:
				  return True
		  return False
	  ```
- **Koko Eating Bananas**
- **Find Minimum in Rotated Sorted Array**
- **Search in Rotated Sorted Array**
- **Time Based Key Value Store**
- **Median of Two Sorted Arrays**