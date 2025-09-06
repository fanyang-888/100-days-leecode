# Day 1：数组

- **题目 1**：[704. 二分查找](https://leetcode.com/problems/binary-search/)
  - **知识点**：二分查找，数组
  - **解题思路**：
    1.  用一个哈希表来存储数组中每个元素的索引。
    2.  遍历数组，对于每个元素 `num`，计算 `target - num`。
    3.  检查哈希表中是否已存在 `target - num`。如果存在，则返回当前元素的索引和哈希表中对应元素的索引。
    4.  如果不存在，将 `num` 和其索引存入哈希表。
  - **代码**：
    ```python
    class Solution:
        def twoSum(self, nums: List[int], target: int) -> List[int]:
            hashmap = {}
            for i, num in enumerate(nums):
                complement = target - num
                if complement in hashmap:
                    return [hashmap[complement], i]
                hashmap[num] = i
    ```
    - **初步思路**：
    1.  *为什么不如推荐（二分查找）*

- **题目 2**：[移除元素](https://leetcode.cn/problems/remove-element/)

