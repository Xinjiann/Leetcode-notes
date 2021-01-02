# Common data structures

## Array

数组优点： 
- 构建简单
- 可以在 O(1) 的时间里返回某个下标的元素

数组缺点：
- 构建时必须分配一段连续的空间
- 查询某个元素是否存在需要遍历整个数组，耗时O(n)
- 删除或添加某个元素时，需要消耗O(n)

## Linked List

链表优点：

- 灵活的分配内存空间
- 能在O(1)时间内删除/添加元素（前一个元素一直的前提下，双链表中已知后一个元素也可实现）

链表缺点：

- 查询需要O(n)时间复杂度

<font color=Red>如果元素个数已知，且需要经常查询，则选择数组；如果元素个数未知，且经常添加删除，则使用链表。</font><br /> 


## Leetcode示例(Array)：

给定两个字符串 s 和 t ，编写一个函数来判断 t 是否是 s 的字母异位词。

```
输入: s = "anagram", t = "nagaram"                                输入: s = "rat", t = "car"
输出: true                                                        输出: false
```
### 思路

由于字符串只包含 26 个小写字母，因此我们可以维护一个长度为 26 的频次数组 table，先遍历记录字符串 s 中字符出现的频次，然后遍历字符串 t，减去 table 中对应的频次，如果出现 table[i]<0，则说明 t 包含一个不在 s 中的额外字符，返回 false 即可。

### 代码实现
```java

public boolean isAnagram(String s, String t) {
    if (s.length() != t.length()){
        return false;
    }
    int[] table = new int[26];

    for (int i=0; i<s.length(); i++){
        table[s.charAt(i)-'a']++;

    }
    for (int i=0; i<t.length(); i++){
        table[t.charAt(i)-'a']--;
        if (table[t.charAt(i)-'a']<0){
            return false;
        }
    }
    return true;
}
```
## Leetcode示例(Linked List)

定义一个函数，输入一个链表的头节点，反转该链表并输出反转后链表的头节点。

```
输入: 1->2->3->4->5->NULL
输出: 5->4->3->2->1->NULL
```

### 思路1：双指针

![](https://github.com/Xinjiann/Leetcode-notes/blob/main/images/IMG_0245.jpg)

### 代码实现

```java
public ListNode reverseList(ListNode head) {

    ListNode cur = null;
    ListNode pre = head;

    while(pre != null){
        ListNode t = pre.next;
        pre.next = cur;
        cur = pre;
        pre = t;
    }
    return cur;

}
```

### 思路2：递归

![](https://github.com/Xinjiann/Leetcode-notes/blob/main/images/recursion.gif)

### 代码实现

```java
public ListNode reverseList(ListNode head) {

  if (head == null || head.next == null){
      return head;
  }
  ListNode t = reverseList(head.next);
  head.next.next = head;
  head.next = null;
  return t;
}
```



