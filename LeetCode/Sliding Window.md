- **Best Time to Buy and Sell Stock**
	- You are given an integer array `prices` where `prices[i]` is the price of NeetCoin on the `ith` day. You may choose a **single day** to buy one NeetCoin and choose a **different day in the future** to sell it. Return the maximum profit you can achieve. You may choose to **not make any transactions**, in which case the profit would be `0`.
	- Keep track of the lowest price and compute the lowest price and max profit at each step.
	- ```python
	  def maxProfit(self, prices: List[int]) -> int:
		  minBuy = prices[0]
		  maxP = 0
		  for price in prices:
			  minBuy = min(minBuy, price)
			  maxP = max(maxP, price - minBuy)
		  return maxP
	  ```
- **Longest Substring Without Repeating Characters**
	- Given a string `s`, find the _length of the longest substring_ without duplicate characters.
	- We expand the window by moving the right pointer. Whenever we come across a duplicate, we will shrink the left pointer until there is no more.
	- ```python
	  def lengthOfLongestSubstring(self, s: str) -> int:
		  charSet = set()
		  maxL, l = 0
		  for r in range(len(s)):
			  while s[l] in charSet:
				  charSet.remove(s[l])
				  l += 1
			  charSet.add(s[r])
			  maxL = max(maxL, r - l + 1)
		  return maxL
	  ```
- **Longest Repeating Character Replacement**
	- You are given a string `s` consisting of only uppercase english characters and an integer `k`. You can choose up to `k` characters of the string and replace them with any other uppercase English character.
	-  For each unique character in s, we will go through and when we come across a string that that needs more than k replacement, we will shift the pointer left until it is less than <= k.
	- ```python
	  def characterReplacement(self, s: str, k: int) -> int:
		  charSet = set(s)
		  maxL = 0
		  for c in charSet:
			  l, count = 0, 0
			  for r in range(len(s)):
				  if s[r] == c:
					  count += 1
				  while (r - l + 1) - count > k:
					  if s[l] == c:
						  count -= 1
					  l += 1
				  maxL = max(maxL, r - l + 1)
		  return maxL
	  ```

After performing at most `k` replacements, return the length of the longest substring which contains only one distinct character.
- **Permutation in String**
	- You are given two strings `s1` and `s2`. Return `true` if `s2` contains a permutation of `s1`, or `false` otherwise. That means if a permutation of `s1` exists as a substring of `s2`, then return `true`.
	- Since a permutation of `s1` must have the **same character counts**, we can use a fixed-size sliding window over `s2` whose length is exactly `len(s1)`.  We maintain two frequency arrays, one for `s1` and one for the current window in `s2`.
	- ```python
	  def checkInclusion(self, s1: str, s2: str) -> bool:
		  if len(s1) > len(s2):
			  return False
		  countS1, countS2 = [0] * 26, [0] * 26
		  for i in range(len(s1)):
			  countS1[ord(s1[i]) - ord('a')] += 1
			  countS2[ord(s2[i]) - ord('a')] += 1
		  matches = 0
		  for i in range(26):
			  matches += (1 if countS1[i] == countS2[i] else 0)
		  l = 0
		  for r in range(len(s1), len(s2)):
			  if matches == 26:
				  return True
			  index = ord(s2[r]) - ord('a')
			  countS2[index] += 1
			  if countS2[index] == countS1[index]:
				  matches += 1
			  elif countS2[index] == countS1[index] + 1:
				  matches -= 1
			  index = ord(s1[l]) - ord('a')
			  if countS2[index] == countS1[index]:
				  matches += 1
			  elif countS2[index] == countS1 - 1:
				  matches -= 1
			  l += 1
		  return matches == 26
 	  ```
- **Minimum Window Substring**
- **Sliding Window Maximum**