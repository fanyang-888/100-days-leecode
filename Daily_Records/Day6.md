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

- **题目 2**：[383. 赎金信]()
  - **知识点**：
  - **解题思路**：
    1.
  - **代码**：
  ```python
  ```

- **题目 3**：[]()
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
