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
	- You are given an array of CPU tasks tasks, where tasks[i] is an uppercase english character from A to Z. You are also given an integer n. Each CPU cycle allows the completion of a single task, and tasks may be completed in any order. The only constraint is that identical tasks must be separated by at least n CPU cycles, to cooldown the CPU. Return the minimum number of CPU cycles required to complete all tasks.
	- Max-Heap
	- ```python
	  def leastInterval(self, tasks: List[str], n: int) -> int:
		  count = Counter(tasks)
		  maxHeap = [-c for c in count.values()]
		  heapq.heapify(maxHeap)
		  time = 0
		  q = deque()
		  while maxHeap or q:
			  time += 1
			  if not maxHeap:
				  time = q[0][1]
			  else:
				  cnt = 1 + heapq.heappop(maxHeap)
				  if cnt:
					  q.append([cnt, time + n])
			  if q and q[0][1] == time:
				  heapq.heappush(maxHeap, q.popleft()[0])
		  return time		  
	  ```
- **Design Twitter**
	- Implement a simplified version of Twitter which allows users to post tweets, follow/unfollow each other, and view the `10` most recent tweets within their own news feed. Users and tweets are uniquely identified by their IDs (integers).
	- `Twitter()` Initializes the twitter object.
	- `void postTweet(int userId, int tweetId)` Publish a new tweet with ID `tweetId` by the user `userId`. You may assume that each `tweetId` is unique.
	- `List<Integer> getNewsFeed(int userId)` Fetches at most the `10` most recent tweet IDs in the user's news feed. Each item must be posted by users who the user is following or by the user themself. Tweets IDs should be **ordered from most recent to least recent**.
	- `void follow(int followerId, int followeeId)` The user with ID `followerId` follows the user with ID `followeeId`.
	- `void unfollow(int followerId, int followeeId)` The user with ID `followerId` unfollows the user with ID `followeeId`.
	- ```python
	  def __init__(self):
	  def postTweet(self, userId: int, tweetId: int) -> None:
	  def getNewsFeed(self, userId: int) -> List[int]:
	  def follow(self, followerId: int, followeeId: int) -> None:
	  def unfollow(self, followerId: int, followeeId: int) -> None:
	  ```
- **Find Median From Data Stream**
	- The median is the middle value in a sorted list of integers. For lists of even length, there is no middle value, so the median is the mean of the two middle values.
	- ```python
	  def __init__(self):
		  self.small, self.large = [], []
	  def addNum(self, num: int) -> None:
		  if self.large and num > self.large[0]:
			  heapq.heappush(self.large, num)
		  else:
			  heapq.heappush(self.small, -1 * num)
		  if len(self.small) > len(self.large) + 1:
			  val = -1 * heapq.heappop(self.small)
			  heapq.heappush(self.large, val)
		  if len(self.large) > len(self.small) + 1:
			  val = heapq.heappop(self.large)
			  heapq.heappush(self.small, -1 * val)
	  def findMedian(self) -> float:
		  if len(self.small) > len(self.large):
			  return -1 * self.small[0]
		  elif len(self.large) > len(self.small):
			  return self.large[0]
		  else:
			  return (-1 * self.small[0] + self.large[0]) / 2.0
	  ```