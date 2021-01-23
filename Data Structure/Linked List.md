# Linked List

## Easy

### 1. [Intersection of two Linked-Lists](https://leetcode.com/problems/intersection-of-two-linked-lists/)
```java
public ListNode getIntersectionNode(ListNode headA, ListNode headB) {
    var lenA = getLen(headA);
    var lenB = getLen(headB);
    var skipCount = Math.abs(lenA - lenB);
    if (lenA > lenB) {
        while (skipCount-- > 0) headA = headA.next;
    } else {
        while (skipCount-- > 0) headB = headB.next;
    }
    
    var commonLen = Math.min(lenA, lenB);
    while (commonLen-- > 0) {
        if (headA == headB) return headA;
        headA = headA.next;
        headB = headB.next;
    }
    
    
    return null;   


private static int getLen(ListNode head) {
    var len = 0;
    while (head != null) {
        len++;
        head = head.next;
    }
    return len;
}
```

## Medium

### 1. [Split Linked List in Parts](https://leetcode.com/problems/split-linked-list-in-parts/)
```java
public ListNode[] splitListToParts(ListNode root, int k) {
    ListNode cur = root;
    int N = 0;
    while (cur != null) {
        cur = cur.next;
        N++;
    }

    int width = N / k, rem = N % k;

    ListNode[] ans = new ListNode[k];
    cur = root;
    for (int i = 0; i < k; ++i) {
        ListNode head = new ListNode(0), write = head;
        for (int j = 0; j < width + (i < rem ? 1 : 0); ++j) {
            write = write.next = new ListNode(cur.val);
            if (cur != null) cur = cur.next;
        }
        ans[i] = head.next;
    }
    return ans;
}
```

## Hard
### 1. [Merge K Sorted Lists](https://leetcode.com/problems/merge-k-sorted-lists/)

```java
public ListNode mergeKLists(ListNode[] lists) {
    
    if(lists.length == 0 ) return null;
        
    PriorityQueue<ListNode> pq = new PriorityQueue<>((a,b)->{
        return a.val - b.val;  
    });  
    
    for(int i=0;i<lists.length;i++){
        if(lists[i] != null)pq.add(lists[i]);
    }
    
    
    if(pq.size() == 0) return null;
    
    ListNode dummy = new ListNode(-1);
    
    ListNode head = dummy;
    while(pq.size()>0){
        ListNode kk = pq.peek();
        pq.poll();
        if(kk.next != null) pq.add(kk.next);
        
        dummy.next =  kk;
        dummy = kk;
    }
    return head.next;   
}
```