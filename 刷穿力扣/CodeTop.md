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

****

## [146. LRU 缓存](https://leetcode.cn/problems/lru-cache/)

****

- LRU 是指最近最少使用，即淘汰掉最近未使用到的 key
- 具体地，我们需要维护一个链表结构：
  - get：判断是否存在 key，有直接返回，没有返回 -1
  - put：首先判断是否存在 key，有则更新，否则为新增
  - 新增 key 后，需要判断缓存空间是否足够，若超过最大缓存容量，则需要删除链表尾部节点
  - 上述的每一次对链表操作 key，都要将 key 移动到链表头部
- 这里链表的选择必须为双向链表：
  - 目的是在将其移动到链表头部时可以快速修改原来前后节点的指向
  - 容量不足删除时也可以通过伪尾部节点快速删除
- 对于判断是否存在 key，内部可以维护一个哈希表

```java
class LRUCache {

    class Node {
        int key;
        int value;
        Node next;
        Node pree;
    }

    private Node head;
    private Node tail;
    private int capacity;
    private HashMap<Integer, Node> vis;

    public LRUCache(int capacity) {
        this.capacity = capacity;
        this.head = new Node();
        this.tail = new Node();
        head.next = tail;
        tail.pree = head;
        this.vis = new HashMap<>();
    }
    
    public int get(int key) {
        if (vis.containsKey(key)) {
            return moveHead(vis.get(key)).value;
        }
        return -1;
    }
    
    public void put(int key, int value) {
        if (vis.containsKey(key)) {
            Node t = vis.get(key);
            vis.remove(key);
            t.value = value;
            vis.put(key, moveHead(t));
        } else {
            if (vis.size() >= capacity) {
                remove();
            }
            Node t = new Node();
            t.key = key;
            t.value = value;
            t.pree = head;
            t.next = head.next;
            vis.put(key, moveHead(t));
        }
    }

    private Node moveHead(Node node) {
        node.pree.next = node.next;
        node.next.pree = node.pree;
        node.next = head.next;
        head.next.pree = node;
        head.next = node;
        node.pree = head;
        return node;
    }

    private void remove() {
        Node t = tail.pree;
        vis.remove(t.key);
        t.pree.next = tail;
        tail.pree = t.pree;
    }
}

/**
 * Your LRUCache object will be instantiated and called as such:
 * LRUCache obj = new LRUCache(capacity);
 * int param_1 = obj.get(key);
 * obj.put(key,value);
 */
```

****

## [206. 反转链表](https://leetcode.cn/problems/reverse-linked-list/)

****

- 利用两个指针，l 和 r
- r：指向当前节点，初始化为 head
- l：指向 r 的前一个节点，初始化为 null
- 翻转过程：
  - 用 t 暂存 r 的下一个节点
  - 使得 r -> l，即 r.next = l;
  - 更新 l = r，即 l = r
  - 将 r 后移，即 r = t;
- 所有节点反转完毕后，l 就是新链表的头节点

```java
class Solution {
    public ListNode reverseList(ListNode head) {
        ListNode l = null, r = head;
        while (r != null) {
            ListNode t = r.next;
            r.next = l;
            l = r;
            r = t;
        }
        return l;
    }
}
```

****
