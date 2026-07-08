- **Contains Duplicate**:
	- Given an integer array `nums`, return `true` if any value appears **more than once** in the array, otherwise return `false`.
	- To solve this, we would initialize an empty hash set. As we iterate through the array, we will store unseen numbers into the hash set and check whether it is in the hash set already. If we go through the whole array without finding a duplicate in the hash set, we would return false. Otherwise, return true.
	- ```python
	  def hasDuplicate(self, nums: List[int]) -> bool:
        seen = set()
        for num in nums:
            if num in seen:
                return True
            seen.add(num)
        return False
	  ```
- **Valid Anagram**:
	- Given two strings `s` and `t`, return `true` if the two strings are anagrams of each other, otherwise return `false`.
	- If the lengths of the string are different, they can not be anagrams. We would create a hash map for each word and track the occurrences of each letter. We would then compare the hash maps.
	- ```python
	  def isAnagram(self, s: str, t: str) -> bool:
		  if len(s) != len(t):
			  return False
		  countS, countT = {}, {}
		  for i in range(len(s)):
			  countS[s[i]] = 1 + countS.get(s[i], 0)
			  countT[t[i]] = 1 + countT.get(t[i], 0)
		  return countS == countT
	  ```
- **Two Sum**:
	- Given an array of integers `nums` and an integer `target`, return the indices `i` and `j` such that `nums[i] + nums[j] == target` and `i != j`. Return the smaller index first
	- We would create a previous map to store the value and indexes of each element. We would calculate the diff on each iteration and if it is in map, it would point to the index storing the diff for the current index value.
	- ```python
	  def twoSum(self, nums: List[int], target: int) -> List[int]:
        prev = {}
        for i, n in enumerate(nums):
            diff = target - n
            if diff in prev:
                return [prev[diff], i]
            prev[n] = i
	  ```
- **Group Anagrams**:
	- Given an array of strings `strs`, group all _anagrams_ together into sublists. You may return the output in **any order**.
	- For every string in strs, we would create a 26-length array to keep count of the letters. We would turn it into a tuple and append the string that has the same tuple together.
	- ```python
	  def groupAnagrams(self, strs: List[str]) -> List[List[str]]:
		  res = defaultdict(list)
		  for s in strs:
			  count = [0] * 26
			  for c in s:
				  count[ord(c) - ord('a')] += 1
			  res[tuple(count)].append(s)
		  return list(res.values())
	  ```
- **Top K Frequent Elements**:
	- Given an integer array `nums` and an integer `k`, return the `k` most frequent elements within the array.
	- We would use bucket sort (n + 1 buckets). We would then return the items in the right most bucket and go left until we reach k numbers in our results.
	- ```python
	  def topKFrequent(self, nums: List[int], k: int) -> List[int]:
		  count = {}
		  freq = [[] for in in range(len(nums) + 1)]
		  for num in nums:
			  count[num] = 1 + count.get(num, 0)
		  for num, count in count.items():
			  freq[count].append(num)
		  res = []
		  for i in range(len(freq) - 1, 0, -1):
			  for num in freq[i]:
				  res.append(num)
				  if len(res) == k:
					  return res
	  ```
- **Encode and Decode Strings**:
	- Design an algorithm to encode **a list of strings** to **a string**. The **encoded string** is then sent over the network and is **decoded** back to the **original list** of strings.
	- In encode, we would create a string that would keep track of the length of the individual strings, a hashtag, and then the actual string. In decode, we would use substring slicing to get the length, readjust i and j, and then substring slice the word into the list.
	- ```python
	  def encode(self, strs: List[str]) -> str:
        res = ""
        for s in strs:
            res += str(len(s)) + '#' + s
        return res
    def decode(self, s: str) -> List[str]:
        res = []
        i = 0
        while i < len(s):
            j = i
            while s[j] != '#':
                j += 1
            length = int(s[i:j])
            i = j + 1
            j = i + length
            res.append(s[i:j])
            i = j
        return res
	  ```
- **Product of Array Except Self**:
	- Given an integer array `nums`, return an array `output` where `output[i]` is the product of all the elements of `nums` except `nums[i]`.
	- The prefix handles everything before the index and postfix handles everything after the index. Result[i] = prefix[i] * postfix[i]
	- ```python
	  def productExceptSelf(self, nums: List[int]) -> List[int]:
		  res = [1] * len(nums)
		  prefix = 1
		  for i in range(len(nums)):
			  res[i] = prefix
			  prefix *= nums[i]
		  postfix = 1
		  for i in range(len(nums) - 1, -1, -1):
			  res[i] *= postfix
			  postfix *= nums[i]
		  return res
	  ```
- **Valid Sudoku**:
	- Return `true` if the Sudoku board is valid, otherwise return `false`
	- Hash Set (One Pass). Hash set for rows, cols, and squares.
	- ```python
	  def isValidSudoku(self, board: List[List[str]]) -> bool:
		  rows = defaultdict(set)
		  cols = defaultdict(set)
		  squares = defaultdict(set)
		  
		  for r in range(9):
			  for c in range(9):
				  if board[r][c] == ".":
					  continue
				  if (board[r][c] in rows[r] or board[r][c] in cols[c]
					  or board[r][c] in squares[(r // 3, c // 3)]):
						  return False
			      rows[r].add(board[r][c])
			      cols[c].add(board[r][c])
			      squares[(r // 3, c // 3)].add(board[r][c])
		  return True
	  ```
- **Longest Consecutive Sequence**:
	- Given an array of integers `nums`, return _the length_ of the longest consecutive sequence of elements that can be formed.
	- Create a set from nums. We only check points where there is no number directly behind to since these have to be the starts.
	- ```python
	  def longestConsecutive(self, nums: List[int]) -> int:
		  numSet = set(nums)
		  longest = 0
		  for num in numSet:
			  if (num - 1) not in numSet:
				  length = 1
				  while (num + length) in numSet:
					  length += 1
			  longest = max(length, longest)
		  return longest
	  ```