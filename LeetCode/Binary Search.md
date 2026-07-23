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
	- Binary Search One Pass. A rotated sorted array are basically two sorted arrays stuck together.
	- ```python
	  def search(self, nums: List[int], target: int) -> int:
		  l, r = 0, len(nums) - 1
		  while l <= r:
			  m = l + ((r - l) // 2)
			  if nums[m] == target:
				  return m
			  if nums[l] <= nums[m]:
				  if target < nums[l] or target > nums[m]:
					  l = m + 1
				  else:
					  r = m - 1
			  else:
				  if target > nums[r] or target < nums[m]:
					  r = m - 1
				  else:
					  l = m + 1
		  return -1
	  ```
- **Time Based Key-Value Store**
	- Design a time-based key-value data structure that can store multiple values for the same key at different time stamps and retrieve the key's value at a certain timestamp.
	- `TimeMap()` Initializes the object of the data structure.
	- `void set(String key, String value, int timestamp)` Stores the key `key` with the value `value` at the given time `timestamp`.
	- `String get(String key, int timestamp)` Returns a value such that `set` was called previously, with `timestamp_prev <= timestamp`. If there are multiple such values, it returns the value associated with the largest `timestamp_prev`. If there are no values, it returns `""`.
	- ```python
	  class TimeMap:
		  def __init__(self):
			  self.keyStore = {}
		  
		  def set(self, key: str, value: str, timestamp: int) -> None:
			  if key not in self.keyStore:
				  self.keyStore[key] = []
			  self.keyStore[key].append([value, timestamp])
		  
		  def get(self, key: str, timestamp: int) -> str:
			  res, values = "", self.keyStore.get(key, [])
			  l, r = 0, len(values) - 1
			  while l <= r:
				  m = l + ((r - l) // 2)
				  if values[m][1] <= timestamp:
					  res = values[m][0]
					  l = m + 1
				  else:
					  r = m - 1
			  return res
	  ```
- **Median of Two Sorted Arrays**
	- You are given two integer arrays `nums1` and `nums2` of size `m` and `n` respectively, where each is sorted in ascending order. Return the [median](https://en.wikipedia.org/wiki/Median) value among all elements of the two arrays.
	- First makes sure `A` is the smaller array so that the binary search is as fast as possible. Then it uses binary search to choose a partition (cut) in `A`, and calculates where the partition in `B` must be so that the left side contains half of all the elements. At each step, it checks whether every value on the left side is less than or equal to every value on the right side (`Aleft <= Bright` and `Bleft <= Aright`). If this condition is true, it has found the correct split: for an odd total number of elements, the median is the smallest value on the right side, and for an even total, it is the average of the largest value on the left side and the smallest value on the right side. If the partition is incorrect, it moves the binary search left or right until the correct partition is found.
	- ```python
	  def findMedianSortedArrays(self, nums1: List[int], nums2: List[int]) -> float:
		  A, B = nums1, nums2
		  total = len(nums1) + len(nums2)
		  half = total // 2
		  if len(A) > len(B):
			  A, B = B, A
		  l, r = 0, len(A) - 1
		  while True:
			  i = l + ((r - l) // 2)
			  j = half - i - 2
			  Aleft = A[i] if i >= 0 else float("-infinity")
			  Aright = A[i + 1] if (i + 1) < len(A) else float("infinity")
			  Bleft = B[j] if j >= 0 else float("-infinity")
			  Bright = B[j + 1] if (j + 1) < len(B) else float("infinity")
			  
			  if Aleft <= Bright and Aright >= Bleft:
				  if total % 2:
					  return min(Aright, Bright)
				  else:
					  return ((min(Aright, Bright) + max(Aleft, Bleft)) / 2)
			  elif Aleft > Bright:
				  r = i - 1
			  else:
				  l = i + 1
	  ```