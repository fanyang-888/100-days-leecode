# Day 1：数组

- **题目 1**：[704. 二分查找](https://leetcode.com/problems/binary-search/)
  - **知识点**：二分查找，数组
  - **解题思路**：
    1.  由于数据是递增的，可以使用二分每次查找对应的一半
    2.  找到最中间值，对于每个中间index `mid`，检查是否 `nums[mid] == target`。
    3.  如果相等，则返回mid坐标
    4.  如果不存在，转入对应的一边继续取中点查找。
  - **代码**：
    ```python
    class Solution:
        def search(self, nums: List[int], target: int) -> int:
            start, end = 0, len(nums)-1
            mid = (start + end) // 2
            while start <= end:
                if nums[mid] == target:
                    return mid
                elif nums[mid] < target:
                    start = mid + 1
                    mid = (start + end) // 2
                else:
                    end = mid - 1
                    mid = (start + end) // 2
            return -1

    # 更优做法：减少memory
    class Solution:
        def search(self, nums: List[int], target: int) -> int:
            start, end = 0, len(nums)-1
            while start <= end:
                mid = (start + end) // 2
                if nums[mid] == target:
                    return mid
                elif nums[mid] < target:
                    start = mid + 1
                else:
                    end = mid - 1
            return -1
    ```
    
  - **初步思路**：
    1.  直接使用线性搜索，遍历整个list找到合适的数
    2.  *为什么不如推荐（二分查找）*：时间复杂度为O(n), 并不是题目要求的O(log n)
  - **代码**：
    ```python
    class Solution:
        def search(self, nums: List[int], target: int) -> int:
            i = 0
            for num in nums:
                if num == target:
                    return i
                else:
                    i += 1
            return -1
    ```
   
      

- **题目 2**：[移除元素](https://leetcode.cn/problems/remove-element/)

