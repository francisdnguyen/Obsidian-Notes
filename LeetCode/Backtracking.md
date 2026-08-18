- **Subsets**
	- Given an array nums of unique integers, return all possible subsets of nums. The solution set must not contain duplicate subsets. You may return the solution in any order.
	- Backtracking
	- ```python
	  def subsets(self, nums: List[int]) -> List[List[int]]:
		  res, subset = [], []
		  def dfs(i):
			  if i >= len(nums):
				  res.append(subset.copy())
				  return
			  subset.append(nums[i])
			  dfs(i + 1)
			  subset.pop()
			  dfs(i + 1)
		  dfs(0)
		  return res
	  ```
	  - Iteration
	  - ```python
	    def subsets(self, nums: List[int]) -> List[List[int]]:
		    res = [[]]
		    for num in nums:
			    res += [subset + [num] for subset in res]
			return res
	    ```
  - **Combination Sum**
	  - You are given an array of distinct integers nums and a target integer target. Your task is to return a list of all unique combinations of nums where the chosen numbers sum to target. The same number may be chosen from nums an unlimited number of times. Two combinations are the same if the frequency of each of the chosen numbers is the same, otherwise they are different. You may return the combinations in any order and the order of the numbers in each combination can be in any order
	  - backtracking
	  - ```python
	    def combinationSum(self, nums: List[int], target: int) -> List[List[int]]:
		    res = []
		    def dfs(i, curr, total):
			    if total == target:
				    res.append(cur.copy())
				    return
				if i >= len(nums) or total > target:
					return
				cur.append(nums[i])
				dfs(i, cur, total + nums[i])
				cur.pop()
				dfs(i + 1, cur, total)
			dfs(0, [], 0)
			return res
	    ```
  - **Combination Sum II**
	  - You are given an array of integers `candidates`, which may contain duplicates, and a target integer `target`. Your task is to return a list of all **unique combinations** of `candidates` where the chosen numbers sum to `target`. Each element from `candidates` may be chosen **at most once** within a combination. The solution set must not contain duplicate combinations. You may return the combinations in **any order** and the order of the numbers in each combination can be in **any order**.
	  - sort, backtracking, avoid duplicate combinations, stop early since list is sorted
	  - ```python
	    def combinationSum2(self, candidates: List[int], target: int) -> List[List[int]]:
		    res = []
		    candidates.sort()
		    def dfs(idx, path, cur):
			    if cur == target:
				    res.append(path.copy())
				    return
				for i in range(idx, len(candidates)):
					if i > idx and candidates[i] == candidates[i - 1]:
						continue
					if cur + candidates[i] > target:
						break
					path.append(candidates[i])
					dfs(i + 1, path, cur + candidates[i])
					path.pop()
		    dfs(0, [], 0)
		    return res
	    ```
  - **Permutations**
	  - Given an array `nums` of **unique** integers, return all the possible permutations. You may return the answer in **any order**.
	  - backtracking
	  - ```python
	    def permute(self, nums: List[int]) -> List[List[int]]:
		    res = []
		    def backtrack(perm, nums, pick):
			    if len(perm) == len(nums):
				    res.append(perm[:])
				    return
				for i in range(len(nums)):
					if not pick[i]:
						perm.append(nums[i])
						pick[i] = True
						backtrack(perm, nums, pick)
						perm.pop()
						pick[i] = False
		    backtrack([], nums, [False] * len(nums))
		    return res
	    ```
  - **Subsets II**
  - **Generate Parentheses**
  - **Word Search**
  - **Palindrome Partitioning**
  - **Letter Combinations of a Phone Number**
  - **N Queens**
  - 