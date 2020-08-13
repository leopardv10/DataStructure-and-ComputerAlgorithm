<img src = 'https://github.com/leopardv10/DataStructure-and-ComputerAlgorithm/blob/master/%E5%9B%9E%E6%BA%AF%E7%AE%97%E6%B3%95/images/37-1.png?raw=true' width = 50%>

<img src = 'https://github.com/leopardv10/DataStructure-and-ComputerAlgorithm/blob/master/%E5%9B%9E%E6%BA%AF%E7%AE%97%E6%B3%95/images/37-2.png?raw=true' width = 50%>

```python
class Solution:
    def solveSudoku(self, board: List[List[str]]) -> None:
        """
        Do not return anything, modify board in-place instead.
        """
        row = [set(range(1, 10)) for i in range(9)]  # 存储每一行还可以填的数字
        col = [set(range(1, 10)) for i in range(9)]  # 存储每一列还可以填写的数字
        block = [set(range(1, 10)) for i in range(9)]  # 存储每个九宫格还可以填写的数字
        empty = []  # 存储需要填写数字的位置

        for i in range(9):
            for j in range(9):
                if board[i][j] != '.':
                    val = int(board[i][j])
                    row[i].remove(val)
                    col[j].remove(val)
                    block[(i // 3)*3 + j // 3].remove(val)  # 注意此处的(i // 3)*3 + j // 3
                else:
                    empty.append((i, j))  # (i, j)处需要填充

        def dfs(ite):
            if ite == len(empty): return True  # 一如既往的递归终止条件
            i, j = empty[ite]
            b = (i // 3)*3 + j // 3
            # 对于[i, j]这个位置，可以填的数字在row[i], col[j], block[b]的交集中
            for val in row[i] & col[j] & block[b]:  
                row[i].remove(val)
                col[j].remove(val)
                block[b].remove(val)
                board[i][j] = str(val)

                if dfs(ite + 1): return True

                row[i].add(val)
                col[j].add(val)
                block[b].add(val)
            return False
            
        return dfs(0)
```

