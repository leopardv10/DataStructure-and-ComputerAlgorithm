<img src = 'https://github.com/leopardv10/DataStructure-and-ComputerAlgorithm/blob/master/%E6%BB%91%E5%8A%A8%E7%AA%97%E5%8F%A3%EF%BC%88%E5%8F%8C%E6%8C%87%E9%92%88%E7%9A%84%E4%B8%80%E7%A7%8D%EF%BC%89/images/lc3.png?raw=true' width = 50%>

### 遇到字符串类的问题很自然想到双指针，而滑动窗口即为其中一种（且较难的一种）

#### 对于本题要注意窗口的移动规则：

1. 如s = “abcdecfgbfggg”，一开始left = 0，当right = 5时，出现重复char--> c
2. 然后left直接移动到3，也就是c的右边，right = 5；（原因很简单，请自行思考）
3. 继续移动right

```java
class Solution {
    public int lengthOfLongestSubstring(String s) {
        int left = 0;
        Set<Character> set = new HashSet<>();  // set即为不包含重复char的窗口
        int max = 0, cur = 0;
        for (int i = 0; i < s.length(); i++) {  // 增大窗口
            while (set.contains(s.charAt(i))) {  // 缩小窗口
            // 当前字符与set中某字符重复，故将left不断右移，并且在set中删除对应元素，起到缩小窗口的作用
                set.remove(s.charAt(left));
                left ++;
                cur --;  // 对应当前窗口的大小
            }
            set.add(s.charAt(i));  // left移到合适位置，去掉重复元素后，将当前字符加入窗口
            cur ++;  
            if (cur > max) max = cur;
        }
    return max;
    }
}
```