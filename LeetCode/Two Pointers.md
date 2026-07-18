- **Valid Palindrome**:
	- Given a string `s`, return `true` if it is a **palindrome**, otherwise return `false`.
	-  We have a left pointer and a right pointer that will traverse the string from both endpoints and compare the characters. It will ignore any characters that are not letters or digits.
	- ```python
	  def isPalindrome(self, s: str) -> bool:
		  l, r = 0, len(s) - 1
		  while l < r:
			  while l < r and not self.alphaNum(s[l]):
				  l += 1
			  while r > l and not self.alphaNum(s[r]):
				  r -= 1
			  if s[l].lower() != s[r].lower():
				  return False
			  l, r = l + 1, r - 1
		  return True
	```
	- ```python
	  def alphaNum(self, c):
		return ord('A') <= ord(c) <= ord('Z') or ord('a') <= ord(c) <= ord('z')
				or ord('0') <= ord(c) <= ord('9')
	  ```
- **Two Sum Sorted**:
	- Return the indices (**1-indexed**) of two numbers, `[index1, index2]`, such that they add up to a given target number `target` and `index1 < index2`. Note that `index1` and `index2` cannot be equal, therefore you may not use the same element twice.
	- Because the array is sorted, if we add numbers from opposite ends, we can just move our pointers left or right to increase or decrease our sum until we get our target since there is exactly one valid solution.
	- ```python
	  def twoSum(self, numbers: List[int], target: int) -> List[int]:
		  l, r = 0, len(numbers) - 1
		  while l < r:
			  sum = numbers[l] + numbers[r]
			  if sum < target:
				  l += 1
			  elif sum > target:
				  r -= 1
			  else:
				  return [l + 1, r + 1]
	  ```
- **3Sum**
	- Given an integer array `nums`, return all the triplets `[nums[i], nums[j], nums[k]]` where `nums[i] + nums[j] + nums[k] == 0`, and the indices `i`, `j` and `k` are all distinct. No duplicate triplets.
	- We sort the list and then at each value from the left, we make sure to skip past duplicates and then use 2 pointers to find the sum with the current value and add it to the list. Once we append it, we have to make sure to skip duplicates at the left pointer again.
	- ```python
	  def threeSum(self, nums: List[int]) -> List[List[int]]:
		  res = []
		  nums.sort()
		  for i, a in enumerate(nums):
			  if a > 0:
				  continue
			  if i > 0 and a == nums[i - 1]:
				  continue
			  l, r = i + 1, len(nums) - 1
			  while l < r:
				  sum = a + nums[l] + nums[r]
				  if sum < 0:
					  l += 1
				  elif sum > 0:
					  r += 1
				  else:
					  res.append([a, nums[l], nums[r]])
					  l += 1
					  r -= 1
					  while nums[l] == nums[l - 1] and l < r:
						  l += 1
		 return res  
	  ```
- **Container with Most Water**
	- You are given an integer array `heights` where `heights[i]` represents the height of the ith bar. You may choose any two bars to form a container. Return the _maximum_ amount of water a container can store.
	- With 2 pointers, we can calculate the area of the graph with width * height at each point and store a maximum. We then move the pointer to whatever height is higher.
	- ```python
	  def maxArea(self, heights: List[int]) -> int:
		  l, r = 0, len(heights) - 1
		  maxArea = 0
		  while l < r:
			  area = min(heights[l], heights[r]) * (r - l)
			  maxArea = max(area, maxArea)
			  if heights[l] <= heights[r]:
				  l += 1
			  else:
				  r -= 1
		  return maxArea
	  ```
- **Trapping Rainwater**
	- You are given an array of non-negative integers `height` which represent an elevation map. Each value `height[i]` represents the height of a bar, which has a width of `1`. Return the maximum area of water that can be trapped between the bars.
	- Water depends on the shorter wall between the left and right sides. If the leftMax is shorter than the rightMax, we can move the pointer inwards and calculate the water trapped. Same goes for the right pointer. water = max wall on that side – height at that position
	- ```python
	  def trap(self, height: List[int]) -> int:
		  l, r = 0, len(height) - 1
		  res = 0
		  leftMax, rigthMax = height[l], height[r]
		  
		  while l < r:
			  if leftMax < rightMax
				  l += 1
				  leftMax = max(leftMax, height[l])
				  res += leftMax - height[l]
			  else:
				  r -= 1
				  rightMax = max(rightMax, height[r])
				  res += rightMax - height[r]
		  return res
	  ```