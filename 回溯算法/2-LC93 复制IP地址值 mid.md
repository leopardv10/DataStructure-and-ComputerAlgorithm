<img src =  'https://github.com/leopardv10/DataStructure-and-ComputerAlgorithm/blob/master/%E5%9B%9E%E6%BA%AF%E7%AE%97%E6%B3%95/images/2.png?raw=true' width = 50%>

### 回溯法：

1. 回溯法很重要的一点是剪枝，对于本题而言：
   + 每一位数的范围在0到255之间，不满足则舍弃；
   + 数字开头不得为0，0本身除外，不满足则舍弃；
   + IP地址最多只有四段，超过四段舍弃； 

2. IP地址的每一段最多为三位数，因此回溯法中for i in range(xxx)中选择的范围有三位（可结合代码理解）

3. code：

   ```python
   class Solution:
       def restoreIpAddresses(self, s: str) -> List[str]:
           size = len(s)
           res = []  # 用来返回最终结果
   
           def dfs(tmp, start, flag):  # flag表示已经有了几段IP
               if len(tmp) == size + 4 and flag == 0:  # 已经有了四段IP，并且字符串中所有数字都已用上
                   res.append(tmp[:-1])
                   return 
               if flag < 0:  # 可能出现已经有了四段IP，但是并未将字符串中所有数字用上的情况
                   return
               for i in range(0, 3):  # 选择该段IP长度为1 or 2 or 3
                   if not start + i < size: break  # 如果超过字符串的范围
                   if i == 0 and s[start] == '0':  # 该段IP起始数字为0：该段只能为0，类似025，012等全部不符合要求
                       dfs(tmp + s[start] + '.', start + 1, flag - 1)
                       break  # 该段只能为0其余选择不符合要求
                   if 0 < int(s[start: start + i + 1]) <= 255:
                       dfs(tmp + s[start: start+i+1] + '.', start + i + 1, flag - 1)
               return 
   
           dfs("", 0, 4)
           return res
   ```

   

   