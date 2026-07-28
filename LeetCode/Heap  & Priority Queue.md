- **Kth Largest Element in a Stream**
	- Design a class to find the kth largest integer in a stream of values, including duplicates. E.g. the 2nd largest from [1, 2, 3, 3] is 3. The stream is not necessarily sorted.
	- ```python
	  def __init__(self, k: int nums: List[int]):
		  self.minHeap = nums
		  self.k = k
		  heapq.heapify(self.minHeap)
		  while len(self.minHeap) > k:
			  heapq.heappop(self.minHeap)
	  def add(self, val: int) -> int:
		  heapq.heappush(self.minHeap, val)
		  if len(self.minHeap) > k:
			  heapq.heappop(self.minHeap)
		  return self.minHeap[0]
	  ```
- **Last Stone Weight**
	- You are given an array of integers stones where stones[i] represents the weight of the ith stone. At each step we choose the two heaviest stones, with weight x and y and smash them togethers. If x == y, both stones are destroyed. If x < y, the stone of weight x is destroyed, and the stone of weight y has new weight y - x. Continue the simulation until there is no more than one stone remaining. Return the weight of the last remaining stone or return 0 if none remain.
	- ```python
	  def lastStoneWeight(self, stones: List[int]) -> int:
		  stones = [-c for c in stones]
		  heapq.heapify(stones)
		  while len(stones) > 1:
			  first, second = heapq.heappop(stones), heapq.heappop(stones)
			  if second > first:
				  heapq.heappush(stones, second - first)
		  stones.append(0)
		  return abs(stones[0])
	  ```
- **K Closest Points to Origin**
	- You are given an 2-D array points where points[i] = [xi, yi] represents the coordinates of a point on an X-Y axis plane. You are also given an integer k. Return the k closest points to the origin (0, 0).
	- ```python
	  def kClosest(self, points: List[List[int]], k: int) -> List[List[int]]:
		  maxHeap = []
		  for x, y in points:
		  dist = -(x ** 2 + y ** 2)
		  heapq.heappush(maxHeap, [dist, x, y])
		  if len (maxHeap) > k:
			  heapq.heappop(maxHeap)
		  res = []
		  while maxHeap:
			  dist, x, y = heapq.heappop(maxHeap)
			  res.append([x, y])
		  return res
	  ```
- **Kth Largest Element in a Stream**
	- Given an unsorted array of integers `nums` and an integer `k`, return the `kth` largest element in the array.
	- heap
	- ```python
	  def findKthLargest(self, nums: List[int], k: int) -> int:
		  return heapq.nlargest(k, nums)[-1]
	  ```
	  - heap written out
	  - ```python
	    def findKthLargest(self, nums: List[int], k: int) -> int:
		    minHeap = [-n for n in nums]
		    heapq.heapify(minHeap)
		    while k > 0:
			    res = heapq.heappop(minHeap)
			    k -= 1
			return -res
	    ```
	    - quicksort
	    - ```python
	       def findKthLargest(self, nums: List[int], k: int) -> int:
	      ```
- **Task Scheduler**
- **Design Twitter**
- **Find Median From Data Stream**