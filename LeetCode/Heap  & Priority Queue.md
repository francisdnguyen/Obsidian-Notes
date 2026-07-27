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
- **Task Scheduler**
- **Design Twitter**
- **Find Median From Data Stream**