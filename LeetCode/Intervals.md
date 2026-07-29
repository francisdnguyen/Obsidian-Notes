- **Insert Intervals**
	- You are given an array of non-overlapping intervals `intervals` where `intervals[i] = [start_i, end_i]` represents the start and the end time of the `ith` interval. `intervals` is initially sorted in ascending order by `start_i`. You are given another interval `newInterval = [start, end]`. Insert `newInterval` into `intervals` such that `intervals` is still sorted in ascending order by `start_i` and also `intervals` still does not have any overlapping intervals. You may merge the overlapping intervals if needed.
	- Greedy
	- ```python
	  def insert(self, intervals: List[List[int]], newInterval: List[int]) -> List[List[int]]:
		  res = []
		  for i in range(len(intervals)):
			  if newInterval[1] < intervals[i][0]:
				  res.append(newInterval)
				  return res + intervals[i:]
			  elif newInterval[0] > intervals[i][1]:
				  res.append(intervals[i])
			  else:
				  newInterval = [
					  min(newInterval[0], intervals[i][0]),
					  max(newInterval[1], intervals[i][1])]
		  res.append(newInterval)
		  return res
	  ```
- **Merge Intervals**
	- Given an array of `intervals` where `intervals[i] = [start_i, end_i]`, merge all overlapping intervals, and return an array of the non-overlapping intervals that cover all the intervals in the input.
	- Sweeping Line
	- ```python
	  def merge(self, intervals: List[List[int]]) -> List[List[int]]:
		  mp = defaultdict(int)
		  for start, end in intervals:
			  mp[start] += 1
			  mp[end] -= 1
		  res = []
		  interval = []
		  have = 0
		  for i in sorted(mp):
			  if not interval:
				  interval.append[i]
			  have += mp[i]
			  if have == 0:
				  interval.append[i]
				  res.append(interval)
				  interval = []
		  return res
		  
	  ```
- **Non Overlapping Intervals**
	- Given an array of intervals `intervals` where `intervals[i] = [start_i, end_i]`, return the minimum number of intervals you need to remove to make the rest of the intervals non-overlapping.
	- Greedy (Sort by Start)
	- ```python
	  def eraseOverlapIntervals(self, intervals: List[List[int]]) -> int:
		  intervals.sort()
		  res = 0
		  prevEnd = intervals[0][1]
		  for start, end in intervals[1:]:
			  if start >= prevEnd:
				  prevEnd = end
			  else:
				  res += 1
				  prevEnd = min(end, prevEnd)
		  return res
		  
	  ```
- **Meeting Rooms**
	- Given an array of meeting time interval objects consisting of start and end times `[[start_1,end_1],[start_2,end_2],...] (start_i < end_i)`, determine if a person could add all meetings to their schedule without any conflicts. The intervals may be provided in any order.
	- sorting
	- ```python
	  def canAttendMeetings(self, intervals: List[Interval]) -> bool:
		  intervals.sort(key=lambda i: i.start)
		  for i in range(1, len(intervals)):
			  i1 = intervals[i - 1]
			  i2 = intervals[i]
			  if i1.end > i2.start:
				  return False
		  return True
	  ```
- **Meeting Rooms II**
	- Given an array of meeting time interval objects consisting of start and end times `[[start_1,end_1],[start_2,end_2],...] (start_i < end_i)`, find the minimum number of rooms required to schedule all meetings without any conflicts.
	- Sweep Line
	- ```python
	  def minMeetingRooms(self, intervals: List[Interval]) -> int:
		  mp = defaultdict(int)
		  for i in intervals:
			  mp[i.start] += 1
			  mp[i.end] -= 1
		  prev, res = 0, 0
		  for i in sorted(mp):
			  prev += mp[i]
			  res = max(res, prev)
		  return res
	  ```
- **Minimum Interval to Include Each Query**