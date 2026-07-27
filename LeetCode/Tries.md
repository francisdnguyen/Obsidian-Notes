- **Implement Trie (Prefix Tree)**
	- A **prefix tree** (also known as a trie) is a tree data structure used to efficiently store and retrieve keys in a set of strings. Some applications of this data structure include auto-complete and spell checker systems.
	- `PrefixTree()` Initializes the prefix tree object.
	- `void insert(String word)` Inserts the string `word` into the prefix tree.
	- `boolean search(String word)` Returns `true` if the string `word` is in the prefix tree (i.e., was inserted before), and `false` otherwise.
	- `boolean startsWith(String prefix)` Returns `true` if there is a previously inserted string `word` that has the prefix `prefix`, and `false` otherwise.
	- ```python
	  class TrieNode:
		  def __init__(self):
			  self.children = [None] * 26
			  self.endOfWord = False
	  class PrefixTree:
		  def __init__(self):
			  self.root = TrieNode()
		  def insert(self, word: str) -> None:
			  curr = self.root
			  for c in word:
				  i = ord(c) - ord('a')
				  if curr.children[i] == None:
					  curr.children[i] = TrieNode()
				  curr = curr.children[i]
			  cur.endOfWord = True
		  def search(self, word: str) -> bool:
			  curr = self.root
			  for c in word:
				  i = ord(c) - ord('a')
				  if curr.children[i] == None:
					  return False
				  curr = curr.children[i]
			  return curr.endOfWord
		  def startsWith(self, prefix: str) -> bool:
			  curr = self.root
			  for c in word:
				  i = ord(c) - ord('a')
				  if curr.children[i] == None:
					  return False
				  curr = curr.children[i]
			  return True
	  ```
  - **Design Add and Search Word Data Structure**
	  - Design a data structure that supports adding new words and searching for existing words.
	- `void addWord(word)` Adds `word` to the data structure.
	- `bool search(word)` Returns `true` if there is any string in the data structure that matches `word` or `false` otherwise. `word` may contain dots `'.'` where dots can be matched with any letter.
	- ```python
	  class TrieNode:
		  def __init__(self):
			  self.children = {}
			  self.word = False
	  class WordDictionary
		  def __init__(self):
			  self.root = TrieNode()
		  def addWord(self, word: str) -> None:
			  curr = self.root
			  for c in word:
				  if c not in curr.children:
					  curr.children[c] = TrieNode()
				  curr = curr.children[c]
			  curr.word = True
		  def search(self, word: str) -> bool:
			  def dfs(j, root):
				  curr = root
				  for i in range(j, len(word)):
					  c = word[i]
					  if c == ".":
						  for child in curr.children.values():
							  if dfs(i + 1, child):
								  return True
						  return False
					  else:
						  if c not in curr.children:
							  return False
						  curr = curr.children[c]
				  return curr.word
			  return dfs(0, self.root)
	  ```