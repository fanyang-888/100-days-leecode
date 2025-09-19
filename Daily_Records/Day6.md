# Day 6: 哈希表

- **题目 1**：[454. 四数之和](https://leetcode.com/problems/4sum-ii/description/)
  - **知识点**：数组，哈希表
  - **解题思路**：
    1.  使用哈希表存储 nums1 和 nums2 的和
    2.  遍历 nums3 和 nums4，查找相反数
  - **代码**：
  ```python
  class Solution:
      def fourSumCount(self, nums1: List[int], nums2: List[int], nums3: List[int], nums4: List[int]) -> int:
          sum_count = {}
          for num1 in nums1:
              for num2 in nums2:
                  sum_val = num1 + num2
                  sum_count[sum_val] = sum_count.get(sum_val, 0) + 1
          count = 0
          for num3 in nums3:
              for num4 in nums4:
                  target = -(num3 + num4)
                  if target in sum_count:
                      count += sum_count[target]
          return count
  ```

- **题目 2**：[383. 赎金信](https://leetcode.com/problems/ransom-note/)
  - **知识点**：哈希表，字符串，计数
  - **解题思路**：
    1.  建立空哈希表，储存各字母在magazine出现的次数
    2.  减去在ransomnote中字母出现的次数
    3.  如果为负，则false
  - **代码**：
  ```python
  class Solution:
      def canConstruct(self, ransomNote: str, magazine: str) -> bool:
          record = [0] * 26
          for char in magazine:
              record[ord(char) - ord("a")] += 1
          for char in ransomNote:
              record[ord(char) - ord("a")] -= 1
              if record[ord(char) - ord("a")] < 0:
                  return False
          return True
  ```

- **题目 3**：[15. 三数之和](https://leetcode.com/problems/3sum/description/)
  - **知识点**：
  - **解题思路**：
    1.
  - **代码**：
  ```python
  ```

- **题目 4**：[]()
  - **知识点**：
  - **解题思路**：
    1.
  - **代码**：
  ```python
  ```

- **题目 5**：[]()
  - **知识点**：
  - **解题思路**：
    1.
  - **代码**：
  ```python
  ```
