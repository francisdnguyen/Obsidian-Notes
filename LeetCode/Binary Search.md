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
	- You are given an integer array `piles` where `piles[i]` is the number of bananas in the `ith` pile. You are also given an integer `h`, which represents the number of hours you have to eat all the bananas. You may decide your bananas-per-hour eating rate of `k`. Each hour, you may choose a pile of bananas and eats `k` bananas from that pile. If the pile has less than `k` bananas, you may finish eating the pile but you can not eat from another pile in the same hour. Return the minimum integer `k` such that you can eat all the bananas within `h` hours.
	- It has to be a number from 1 to max in piles. We used binary search from this range and we record the smallest speed.
	- ```python
	  def minEatingSpeed(self, piles: List[int], h: int) -> int:
		  l, r = 1, max(piles)
		  res = r
		  while l <= r:
			  m = (r + l) // 2
			  totalTime = 0
			  for p in piles:
				  totalTime += math.ceil(float(p) / m)
			  if totalTime <= h:
				  res = m
				  r = m - 1
			  else
				  l = m + 1
		  return res
	  ```
- **Find Minimum in Rotated Sorted Array**
	- You are given an array of length `n` which was originally sorted in ascending order. It has now been **rotated** between `1` and `n` times. Assuming all elements in the rotated sorted array `nums` are **unique**, return the minimum element of this array.
	- Binary Search Lower Bound: if nums[mid] < nums[r], the minimum has to be in the left half including mid. Otherwise, the minimum has to be in the right half excluding mid.
	- ```python
	  def findMin(self, nums: List[int]) -> int:
		  l, r = 0, len(nums) - 1
		  while l < r:
			  m = l + ((r - l) // 2)
			  if nums[m] < nums[r]
				  r = m
			  else:
				  l = m + 1
		  return nums[l]
	  ```
- **Search in Rotated Sorted Array**
	- Given the rotated sorted array `nums` and an integer `target`, return the index of `target` within `nums`, or `-1` if it is not present.
	- 1. **First binary search**: Find the pivot — the index of the smallest element. This tells us where the array was rotated. **Second binary search**: Decide which sorted half may contain the target, then run a standard binary search only on that half.
	- ```python
	  def search(self, nums: List[int], target: int) -> int:
		  l, r = 0, len(nums) - 1
		  while l < r:
			  m = l + ((r - l) // 2)
			  if nums[m] > nums[r]:
				  l = m + 1
			  else:
				  r = m
		  pivot = l
		  l, r = 0, len(nums) - 1
		  if target >= nums[pivot] and target <= nums[r]:
			  l = pivot
		  else:
			  r = pivot - 1
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
- **Time Based Key Value Store**
- **Median of Two Sorted Arrays**