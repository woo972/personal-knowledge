---
tags:
  - algorithm
  - data_structure
  - coding_test
  - dev
dg-publish: true
---
	 ## 접근 방법
---
- Brute Force: enumerate all possible solutions
- Greedy: keep track of the best answer so far
- Use a Hash Table
	- Tip: 문제에서는 주로 Input array에서 item이 얼마나 많이 등장했는지 체크해야할 때 사용
- 
### 팁
- `O(n^2)` : 이중 루프
- `O(nlogn)` : 정렬, 힙
- `O(n)` : 루프 
- `O(logn)` : 바이너리 서치
- `O(1)` : 해쉬
- 이중~삼중루프가 필요한 문제는 정렬로 풀 수 있는지 고민
- 정렬이 필요한 문제는 정렬 후 이중 포인터, 혹은 바이너리서치가 가능한지 확인
- 정렬이 필요한 문제는 한번의 루프와 해쉬를 조합하여 풀 수 있는 지 고민
## 문제 목록
---
### LeetCode TOP 75: 
### Array

- [Two Sum](https://leetcode.com/problems/two-sum/)
- [Best Time to Buy and Sell Stock](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/)
- [Contains Duplicate](https://leetcode.com/problems/contains-duplicate/)
- [Product of Array Except Self](https://leetcode.com/problems/product-of-array-except-self/)
- [Maximum Subarray](https://leetcode.com/problems/maximum-subarray/)
- [Maximum Product Subarray](https://leetcode.com/problems/maximum-product-subarray/)
- [Find Minimum in Rotated Sorted Array](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/)
- [Search in Rotated Sorted Array](https://leetcode.com/problems/search-in-rotated-sorted-array/)
- [3 Sum](https://leetcode.com/problems/3sum/)
- [Container With Most Water](https://leetcode.com/problems/container-with-most-water/)

---

### Binary

- [Sum of Two Integers](https://leetcode.com/problems/sum-of-two-integers/)
- [Number of 1 Bits](https://leetcode.com/problems/number-of-1-bits/)
- [Counting Bits](https://leetcode.com/problems/counting-bits/)
- [Missing Number](https://leetcode.com/problems/missing-number/)
- [Reverse Bits](https://leetcode.com/problems/reverse-bits/)

---

### Dynamic Programming

- [Climbing Stairs](https://leetcode.com/problems/climbing-stairs/)
- [Coin Change](https://leetcode.com/problems/coin-change/)
- [Longest Increasing Subsequence](https://leetcode.com/problems/longest-increasing-subsequence/)
- [Longest Common Subsequence](https://leetcode.com/problems/longest-common-subsequence/)
- [Word Break Problem](https://leetcode.com/problems/word-break/)
- [Combination Sum](https://leetcode.com/problems/combination-sum-iv/)
- [House Robber](https://leetcode.com/problems/house-robber/)
- [House Robber II](https://leetcode.com/problems/house-robber-ii/)
- [Decode Ways](https://leetcode.com/problems/decode-ways/)
- [Unique Paths](https://leetcode.com/problems/unique-paths/)
- [Jump Game](https://leetcode.com/problems/jump-game/)

---

### Graph

- [Clone Graph](https://leetcode.com/problems/clone-graph/)
- [Course Schedule](https://leetcode.com/problems/course-schedule/)
- [Pacific Atlantic Water Flow](https://leetcode.com/problems/pacific-atlantic-water-flow/)
- [Number of Islands](https://leetcode.com/problems/number-of-islands/)
- [Longest Consecutive Sequence](https://leetcode.com/problems/longest-consecutive-sequence/)
- [Alien Dictionary (Leetcode Premium)](https://leetcode.com/problems/alien-dictionary/)
- [Graph Valid Tree (Leetcode Premium)](https://leetcode.com/problems/graph-valid-tree/)
- [Number of Connected Components in an Undirected Graph (Leetcode Premium)](https://leetcode.com/problems/number-of-connected-components-in-an-undirected-graph/)

---

### Interval

- [Insert Interval](https://leetcode.com/problems/insert-interval/)
- [Merge Intervals](https://leetcode.com/problems/merge-intervals/)
- [Non-overlapping Intervals](https://leetcode.com/problems/non-overlapping-intervals/)
- [Meeting Rooms (Leetcode Premium)](https://leetcode.com/problems/meeting-rooms/)
- [Meeting Rooms II (Leetcode Premium)](https://leetcode.com/problems/meeting-rooms-ii/)

---

### Linked List

- [Reverse a Linked List](https://leetcode.com/problems/reverse-linked-list/)
- [Detect Cycle in a Linked List](https://leetcode.com/problems/linked-list-cycle/)
- [Merge Two Sorted Lists](https://leetcode.com/problems/merge-two-sorted-lists/)
- [Merge K Sorted Lists](https://leetcode.com/problems/merge-k-sorted-lists/)
- [Remove Nth Node From End Of List](https://leetcode.com/problems/remove-nth-node-from-end-of-list/)
- [Reorder List](https://leetcode.com/problems/reorder-list/)

---

### Matrix

- [Set Matrix Zeroes](https://leetcode.com/problems/set-matrix-zeroes/)
- [Spiral Matrix](https://leetcode.com/problems/spiral-matrix/)
- [Rotate Image](https://leetcode.com/problems/rotate-image/)
- [Word Search](https://leetcode.com/problems/word-search/)

---

### String

- [Longest Substring Without Repeating Characters](https://leetcode.com/problems/longest-substring-without-repeating-characters/) two pointer
- [Longest Repeating Character Replacement](https://leetcode.com/problems/longest-repeating-character-replacement/) -> X
- [Minimum Window Substring](https://leetcode.com/problems/minimum-window-substring/)
- [Valid Anagram](https://leetcode.com/problems/valid-anagram/)
- [Group Anagrams](https://leetcode.com/problems/group-anagrams/)
- [Valid Parentheses](https://leetcode.com/problems/valid-parentheses/)
- [Valid Palindrome](https://leetcode.com/problems/valid-palindrome/)
- [Longest Palindromic Substring](https://leetcode.com/problems/longest-palindromic-substring/)
- [Palindromic Substrings](https://leetcode.com/problems/palindromic-substrings/)
- [Encode and Decode Strings (Leetcode Premium)](https://leetcode.com/problems/encode-and-decode-strings/)

---

### Tree

- [Maximum Depth of Binary Tree](https://leetcode.com/problems/maximum-depth-of-binary-tree/)
- [Same Tree](https://leetcode.com/problems/same-tree/)
- [Invert/Flip Binary Tree](https://leetcode.com/problems/invert-binary-tree/)
- [Binary Tree Maximum Path Sum](https://leetcode.com/problems/binary-tree-maximum-path-sum/)
- [Binary Tree Level Order Traversal](https://leetcode.com/problems/binary-tree-level-order-traversal/)
- [Serialize and Deserialize Binary Tree](https://leetcode.com/problems/serialize-and-deserialize-binary-tree/)
- [Subtree of Another Tree](https://leetcode.com/problems/subtree-of-another-tree/)
- [Construct Binary Tree from Preorder and Inorder Traversal](https://leetcode.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal/)
- [Validate Binary Search Tree](https://leetcode.com/problems/validate-binary-search-tree/)
- [Kth Smallest Element in a BST](https://leetcode.com/problems/kth-smallest-element-in-a-bst/)
- [Lowest Common Ancestor of BST](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-search-tree/)
- [Implement Trie (Prefix Tree)](https://leetcode.com/problems/implement-trie-prefix-tree/)
- [Add and Search Word](https://leetcode.com/problems/add-and-search-word-data-structure-design/)
- [Word Search II](https://leetcode.com/problems/word-search-ii/)

---

### Heap

- [Merge K Sorted Lists](https://leetcode.com/problems/merge-k-sorted-lists/)
- [Top K Frequent Elements](https://leetcode.com/problems/top-k-frequent-elements/)
- [Find Median from Data Stream](https://leetcode.com/problems/find-median-from-data-stream/)

---
### Amazon
- https://leetcode.com/problems/copy-list-with-random-pointer/  #linked_list #hash_table #tree
- https://leetcode.com/problems/merge-two-sorted-lists/ #linked_list
- https://leetcode.com/problems/valid-anagram/ #hash_table #string #sort
- https://leetcode.com/problems/binary-tree-level-order-traversal #binary_tree #bfs
- https://leetcode.com/problems/search-insert-position/ #binary_search 
- https://leetcode.com/problems/the-kth-factor-of-n/submissions/ #math
- https://leetcode.com/problems/optimal-partition-of-string #string #set
- https://leetcode.com/problems/3sum/ #sorting #two_pointer
	- https://leetcode.com/problems/two-sum/ #hash_table
- https://leetcode.com/problems/count-complete-tree-nodes/ #divide_conquer #dfs
## Appendix
---
- [Coding Interview Preparation | Codinginterview](https://www.codinginterview.com/)
- [Cracking the top Amazon coding interview questions (educative.io)](https://www.educative.io/blog/crack-amazon-coding-interview-questions)
- [Top Interview 150 - Study Plan - LeetCode](https://leetcode.com/studyplan/top-interview-150/)
- [14 Patterns to Ace Any Coding Interview Question](https://hackernoon.com/14-patterns-to-ace-any-coding-interview-question-c5bb3357f6ed)
- [Grind 75](https://www.techinterviewhandbook.org/grind75)





