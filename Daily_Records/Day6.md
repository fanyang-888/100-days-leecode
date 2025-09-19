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
  - **知识点**：数组，双指针，排序
  - **解题思路**：
    1.  排序预处理，外层循环固定第一个数nums[i]
    2.  如果第一个>0，则不可能合为0，直接返回空列表
    3.  对列表进行去重，内层循环找另外两个数
    4.  哈希表查找
  - **代码**：
  ```python
  class Solution:
      def threeSum(self, nums: List[int]) -> List[List[int]]:
          result = []
          nums.sort()
          for i in range(len(nums)):
              if nums[i] > 0:
                  break
              if i > 0 and nums[i] == nums[i - 1]: 
                  continue
              d = {}
              for j in range(i + 1, len(nums)):
                  if j > i + 2 and nums[j] == nums[j-1] == nums[j-2]:
                      continue
                  c = 0 - (nums[i] + nums[j])
                  if c in d:
                      result.append([nums[i], nums[j], c])
                      d.pop(c) 
                  else:
                      d[nums[j]] = j
          return result
  ```

- **题目 4**：[18. 四数之和](https://leetcode.com/problems/4sum/)
  - **知识点**：数组，双指针，排序
  - **解题思路**：
    1.  创建一个字典来存储输入列表中每个数字的频率
    2.  创建一个集合来存储最终答案，并遍历4个数字的所有唯一组合
  - **代码**：
  ```python
  class Solution:
      def fourSum(self, nums: List[int], target: int) -> List[List[int]]:
          freq = {}
          for num in nums:
              freq[num] = freq.get(num, 0) + 1
          ans = set()
          for i in range(len(nums)):
              for j in range(i + 1, len(nums)):
                  for k in range(j + 1, len(nums)):
                      val = target - (nums[i] + nums[j] + nums[k])
                      if val in freq:
                          # 确保没有重复
                          count = (nums[i] == val) + (nums[j] == val) + (nums[k] == val)
                          if freq[val] > count:
                              ans.add(tuple(sorted([nums[i], nums[j], nums[k], val])))
          return [list(x) for x in ans]
  ```

