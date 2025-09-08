# Day 2: 数组

- **题目 1**：[59. 螺旋矩阵 II](https://leetcode.com/problems/spiral-matrix-ii/description/)
  - **知识点**：指针，边界收缩
  - **解题思路**：
    1.  用四个边界指针：top, bottom, left, right。
    2.  按顺序循环填充四条边：上行→右列→下行→左列，每填完一条边收缩相应边界。
    3.  当 top > bottom 或 left > right 时结束。
    4.  时间复杂度 O(n^2)，空间复杂度 O(n^2)。
  - **代码**：
  ```python
  class Solution:
      def generateMatrix(self, n: int) -> List[List[int]]:
          if n <= 0:
              return []
          top, bottom, left, right = 0, n-1, 0, n-1
          num = 1
          matrix = [[0]*n for _ in range(n)]
  
          while top <= bottom and left <= right:
              for i in range(left, right+1): #上
                  matrix[top][i] = num
                  num += 1
              top += 1
  
              for i in range(top, bottom+1): #右
                  matrix[i][right] = num
                  num += 1
              right -= 1
  
              for i in range(right, left-1, -1): # 下
                  matrix[bottom][i] = num
                  num += 1
              bottom -= 1
  
              for i in range(bottom, top-1, -1): #左
                  matrix[i][left] = num
                  num += 1
              left += 1
  
          return matrix
  ```

- **题目 2**：[58. 最后单词长度](https://leetcode.com/problems/length-of-last-word/description/)
  - **知识点**：字符串遍历，双指针
  - **解题思路**：
    1.  从字符串末尾开始：
    2.  先跳过所有尾部空格。
    3.  从第一个非空格字符开始向左计数，直到遇到空格或到达开头。
  - **代码**：
  ```python
  def lengthOfLastWord(s: str) -> int:
      i, n = len(s) - 1, len(s)
      while i >= 0 and s[i] == ' ':
          i -= 1
      length = 0
      while i >= 0 and s[i] != ' ':
          length += 1
          i -= 1
      return length
  ```
  - **我的解题思路**：更简便
    1.  直接使用split，因为字符串只包含string或者空格
    2.  返回最后一个值
  - **代码**：
  ```python
  class Solution:
      def lengthOfLastWord(self, s: str) -> int:
          str_split = s.split()
          return len(str_split[-1])
  ```

