- **Valid Parentheses**:
	- The input string `s` is valid if and only if:
		- Every open bracket is closed by the same type of close bracket.
		- Open brackets are closed in the correct order.
		- Every close bracket has a corresponding open bracket of the same type.
	- Return `true` if `s` is a valid string, and `false` otherwise.
	- We use a stack to track opening brackets since open brackets are closed in the correct order.
	- ```python
	  def isValid(self, s: str) -> bool:
		  stack = []
		  pair = {')' : '(', ']' : '[', '}' : '{'}
		  for c in s:
			  if c in pair:
				  if stack and stack[-1] == pair[c]:
					  stack.pop()
				  else:
					  return False
			  else:
				  stack.append(c)
		  return True if not stack else False
	  ```
- **Min Stack**:
	- One stack and instead of storing the actual, we store encoded ones. We record the difference between the pushed value and the minimum. Whenever a new minimum value is pushed, we store a negative encoded value. When we pop that value, we restore the previous minimum.
	- ![[MinStack Code.png]]
- **Evaluate Reverse Polish Notation**:
	- Return the integer that represents the evaluation of the expression.
	-  tokens = ["1","2","+","3","*","4","-"] -> ((1 + 2) * 3) - 4 = 5
	- ```python
	  def evalRPN(self, tokens: List[str]) -> int:
		  stack = []
		  for c in tokens:
			  if c == "+":
				  stack.append(stack.pop() + stack.pop())
			  elif c == "-":
				  a, b = stack.pop(), stack.pop()
				  stack.append(b - a)
			  elif c == "*":
				  stack.append(stack.pop() * stack.pop())
			  elif c == "/":
				  a, b = stack.pop(), stack.pop()
				  stack.append(int(float(b) / a))
			  else:
				  stack.append(int(c))
		   return stack[0]
	  ```
- **Daily Temperatures**:
	- Return an array `result` where `result[i]` is the number of days after the `ith` day before a warmer temperature appears on a future day. If there is no day in the future where a warmer temperature will appear for the `ith` day, set `result[i]` to `0` instead.
	- The stack helps keep track of days still waiting for a warmer temperature. Once it finds one, it will pop and compute the index to see how long it took.
	- ```python
	  def dailyTemperatures(self, temperatures: List[int]) -> List[int]:
		  stack = []
		  res = [0] * len(temperatures)
		  for t, i in enumerate(temperatures):
			  while stack and t > stack[-1][0]:
				  stackT, stackI = stack.pop()
				  res[stackI] = i - stackI
			  stack.append((t, i))
		  return res
	  ```
- **Car Fleet**:
	- A car can **not** pass another car ahead of it. It can only catch up to another car and then drive at the same speed as the car ahead of it. A **car fleet** is a non-empty set of cars driving at the same position and same speed. A single car is also considered a car fleet. If a car catches up to a car fleet the moment the fleet reaches the destination, then the car is considered to be part of the fleet. Return the number of **different car fleets** that will arrive at the destination.
	-  We reverse sort the list so that cars closer to the target are processed first. If  a car time is faster than the most recent car on the stack, it will combine so it will pop off.
	- ```python
	  def carFleet(self, target: int, position: List[int], speed: List[int]) -> int:
		  pair = [(p, s) for p, s in zip(position, speed)]
		  pair.sort(reverse=True)
		  stack = []
		  for p, s in pair:
			  stack.append((target - p) / s)
			  if len(stack) > 1 and stack[-1] <= stack[-2]:
				  stack.pop()
		  return len(stack)
	  ```
- **Largest Rectangle In Histogram**:
	- You are given an array of integers `heights` where `heights[i]` represents the height of a bar. The width of each bar is `1`. Return the area of the largest rectangle that can be formed among the bars.
	- ```python
	  def largestRectangleArea(self, heights: List[int]) -> int:
		  stack = []
		  maxArea = 0
		  n = len(heights)
		  for i in range(n + 1):
			  while stack and (i == n or heights[stack[-1]] >= heights[i]):
				  height = heights[stack.pop()]
	              width = i if not stack else i - stack[-1] - 1
                  maxArea = max(maxArea, height * width)
              stack.append(i)
          return maxArea
	  ```