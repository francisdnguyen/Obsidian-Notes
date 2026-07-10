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
- **Permutation in String**
- **Minimum Window Substring**
- **Sliding Window Maximum**