# CodeTop

****

## [3. 无重复字符的最长子串](https://leetcode.cn/problems/longest-substring-without-repeating-characters/)

****

- 双指针滑窗
- 用 vis 存窗口内存在的字符
- 如果右边界的字符在 vis 中存在：
  - 不断收缩左边界，同时将左边界字符移出 vis
  - 直到不存在右边界的字符为止
- 每次更新 ans 为两个边界的长度取最大值

```java
class Solution {
    public int lengthOfLongestSubstring(String s) {
        int ans = 0;
        int[] vis = new int[200];
        int l = 0, r = 0;
        while (r < s.length()) {
            while (l < r && vis[s.charAt(r)] == 1) {
                vis[s.charAt(l ++)] --;
            }
            vis[s.charAt(r)] ++;
            ans = Math.max(r - l + 1, ans);
            r ++;
        }
        return ans;
    }
}
```

```go
func lengthOfLongestSubstring(s string) int {
    vis := map[byte]int{}
    l, ans := 0, 0
    for i := 0; i < len(s); i ++ {
        for ; l < i && vis[s[i]] == 1; l ++ {
            vis[s[l]] --
        }
        vis[s[i]] ++
        ans = max(i - l + 1, ans)
    }
    return ans;
}

func max(x, y int) int {
    if x < y {
        return y
    }
    return x;
}
```

