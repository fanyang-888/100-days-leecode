# Day 5: Hash Table
- **题目 1**：[242. 有效字母异位词](https://leetcode.com/problems/valid-anagram/description/)
  - **知识点**：哈希表，字符串，排序
  - **解题思路**：
    1.  创建一个长度为 26 的数组 record，对应 26 个英文字母
    2.  遍历第一个字符串 s，将每个字符的出现次数 +1
    3.  遍历第二个字符串 t，将每个字符的出现次数 -1
    4.  检查 record 数组，如果所有元素都为 0，说明两个字符串包含相同的字符且数量相等
  - **代码**：
  ```python
  class Solution:
      def isAnagram(self, s: str, t: str) -> bool:
          record = [0] * 26
          for i in s:
              #并不需要记住字符a的ASCII，只要求出一个相对数值就可以了
              record[ord(i) - ord("a")] += 1
          for i in t:
              record[ord(i) - ord("a")] -= 1
          for i in range(26):
              if record[i] != 0:
                  return False
          return True
  ```

- **题目 2**：[1002. 找共同字符](https://leetcode.com/problems/find-common-characters/)
  - **知识点**：数组，哈希表，字符串
  - **解题思路**：
    1.  创建长度为26的数组，对应26个英文字母
    2.  用第一个字符串初始化：统计第一个字符串中每个字符的出现次数
    3.  遍历其他字符串，更新最小频率
    4.  将结果转换为字符列表
  - **代码**：
  ```python
  class Solution:
      def commonChars(self, words: List[str]) -> List[str]:
          if not words: return []
          result = []
          hash = [0] * 26 # 用来统计所有字符串里字符出现的最小频率
          for i, c in enumerate(words[0]):  # 用第一个字符串给hash初始化
              hash[ord(c) - ord('a')] += 1
          # 统计除第一个字符串外字符的出现频率
          for i in range(1, len(words)):
              hashOtherStr = [0] * 26
              for j in range(len(words[i])):
                  hashOtherStr[ord(words[i][j]) - ord('a')] += 1
              # 更新hash，保证hash里统计26个字符在所有字符串里出现的最小次数
              for k in range(26):
                  hash[k] = min(hash[k], hashOtherStr[k])
          # 将hash统计的字符次数，转成输出形式
          for i in range(26):
              while hash[i] != 0: # 注意这里是while，多个重复的字符
                  result.extend(chr(i + ord('a')))
                  hash[i] -= 1
          return result
  ```

- **题目 3**：[394. 两个数组的交集](https://leetcode.com/problems/intersection-of-two-arrays/description/)
  - **知识点**：哈希表，数组，字典，指针
  - **解题思路**：
    1.  创建一个字典，包含第一个数组的所有
    2.  对比第二个数组，取交集
  - **代码**：
  ```python
  class Solution:
      def intersection(self, nums1: List[int], nums2: List[int]) -> List[int]:
          table = {}
          for num in nums1:
              table[num] = table.get(num, 0) + 1
          res = set()
          for num in nums2:
              if num in table:
                  res.add(num)
                  del table[num]
          
          return list(res)
  ```

- **题目 4**：[202. 快乐数](https://leetcode.com/problems/happy-number/description/)
  - **知识点**：循环检测，哈希表，数学运算
  - **解题思路**：
    1.  特殊情况处理：如果 n == 1，直接返回 True
    2.  循环检测：使用集合 seen 记录已经出现过的数字
    3.  计算平方和：将数字转换为字符串，计算各位数字的平方和
    4.  重复过程：直到得到 1 或检测到循环
  - **代码**：
  ```python
  class Solution:
      def isHappy(self, n: int) -> bool:
          if n == 1:
              return True
          else:
              happy = str(n)
              sos = 0
              seen = set()
              while sos != 1:
                  if happy in seen:
                      return False
                  seen.add(happy)
                  sos = 0
                  for i in range(len(happy)):
                      sos += int(happy[i]) ** 2
                  happy = str(sos)
              return True
          return False
  ```

- **题目 5**：[1. 两数之和](https://leetcode.com/problems/two-sum/description/)
  - **知识点**：数组，哈希表
  - **解题思路**：
    1.  初始化哈希表
    2.  遍历数组
    3.  计算，查找互补数
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
          return []
  ```
