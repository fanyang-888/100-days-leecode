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

    # 更优做法：在while内部开始时为mid赋值，减少memory，不用每次更新变量都重新为mid赋值
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
   
      

- **题目 2**：[27. 移除元素](https://leetcode.com/problems/remove-element/)
  - **知识点**：移除元素，数组
  - **解题思路**：
    1.  只要val还在lis中，就进行删除操作
    2.  for循环遍历数组，查找num == val
    3.  如果满足，就删除该num
  - **代码**：
    ```python
    class Solution:
        def removeElement(self, nums: List[int], val: int) -> int:
            while val in nums:
                for num in nums:
                    if num == val:
                        nums.remove(num)
            return len(nums)

    # 更优做法：直接remove val，不用乱七八糟的for了
    class Solution:
        def removeElement(self, nums: List[int], val: int) -> int:
            while val in nums:
                nums.remove(val)
            return len(nums)
    ```


- **题目 3**：[977. 排序数组中的平方](https://leetcode.com/problems/squares-of-a-sorted-array/)
  - **知识点**：数组平方
  - **解题思路**：
    1.  将数组中的每个元素平方后，返回按非递减顺序排列的数组
    2.  原数组可能包含负数，平方后顺序会改变，不能先排序后平方
  - **代码**：
  ```python
  class Solution:
      def sortedSquares(self, nums: List[int]) -> List[int]:
          for i in range(len(nums)):
              nums[i] = nums[i]**2
          return sorted(nums)

  # 更优（简洁代码）
  class Solution:
      def sortedSquares(self, nums: List[int]) -> List[int]:
          return sorted([num**2 for num in nums])
  ```

- **题目 4**：[209. 最小子数组之和](https://leetcode.com/problems/minimum-size-subarray-sum/description/)
  - **知识点**：滑动窗口（sliding window）
  - **解题思路**：
    1.  扩展阶段：right 向右移动，增加窗口和
    2.  收缩阶段：当和 ≥ target 时，尝试缩小窗口
    3.  更新答案：每次满足条件时更新最小长度
  - **代码**：
  ```python
  class Solution:
      def minSubArrayLen(self, target: int, nums: List[int]) -> int:
          if target <= max(nums):
              return 1
          if target > sum(nums):
              return 0
          min_len = float('inf')
          left = 0
          sub_sum = 0
          for right in range(len(nums)):
              sub_sum += nums[right]
              while sub_sum >= target:
                  min_len = min(min_len, right - left + 1)
                  sub_sum -= nums[left]
                  left += 1
          return min_len

  # 另一版本：不先判断特殊情况
  class Solution:
      def minSubArrayLen(self, target: int, nums: List[int]) -> int:
          left = 0
          min_len = float('inf')
          window_sum = 0
          for right in range(len(nums)):
              window_sum += nums[right] # 1. 扩展窗口
              while window_sum >= target: # 2. 收缩窗口（寻找最小长度）
                  min_len = min(min_len, right - left + 1)
                  window_sum -= nums[left]
                  left += 1
          return min_len if min_len != float('inf') else 0
  ```


