<img src = 'https://github.com/leopardv10/DataStructure-and-ComputerAlgorithm/blob/master/%E5%9B%9E%E6%BA%AF%E7%AE%97%E6%B3%95/images/%E5%89%91%E6%8C%87offer3.png?raw=true' width = 50%>

### 很明显的回溯法求解，但是要做好剪枝

#### 本题的难度在于：数组中可能有重复字符，比如'aba'中有两个a，因此不能每当出现重复字符时便跳过

#### 因此我们使用两个set来判断：

1. set1存储的是字符的index，即避免dfs搜索时同一位置的字符使用多次；
2. set2每次递归都会创建，目的是在当前递归层中，比如对于第一个位置，我们有'aba'三个选择，选过第一个a之后便不会选第二个a；

```java
class Solution {
    List<String> res = new ArrayList<>();
    char[] c; 
    char[] tmp;
    HashSet<Integer> set1 = new HashSet<>();

    public String[] permutation(String s) {
        c = s.toCharArray();  //将字符串转换成字符串数组
        tmp = s.toCharArray();
        dfs(0);
        return res.toArray(new String[res.size()]);  // 转换成数组
    }

    public void dfs(int x) {
        if (x == c.length) {
            res.add(String.valueOf(tmp));  //将数组c变成字符串
            return;
        }
        
        HashSet<Character> set2 = new HashSet<>();
        for (int i = 0; i < c.length; i++) {
            if (set1.contains(i)) continue;
            if (set2.contains(c[i])) continue;
            set1.add(i);
            set2.add(c[i]);
            tmp[x] = c[i];
            dfs(x + 1);
            set1.remove(i);
        }
    }
}
```

