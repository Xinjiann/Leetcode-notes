# Heap

## Medium

### 1. [Top K Frequent Words](https://leetcode.com/problems/top-k-frequent-words/)

```java
public List<String> topKFrequent(String[] words, int k) {
    Map<String, Integer> count = new HashMap();
    for (String word: words) {
        count.put(word, count.getOrDefault(word, 0) + 1);
    }
    PriorityQueue<String> heap = new PriorityQueue<String>(
            (w1, w2) -> count.get(w1).equals(count.get(w2)) ?
            w2.compareTo(w1) : count.get(w1) - count.get(w2) );

    for (String word: count.keySet()) {
        heap.offer(word);
        if (heap.size() > k) heap.poll();
    }

    List<String> ans = new ArrayList();
    while (!heap.isEmpty()) ans.add(heap.poll());
    Collections.reverse(ans);
    return ans;
}
```
## Hard

### 1. [Sliding Window Maximum](https://leetcode.com/problems/sliding-window-maximum/)
```java
public int[] maxSlidingWindow(int[] nums, int k) {
    Deque<Integer> dq = new LinkedList<>();
    int[] res = new int[nums.length - k + 1];
    int r = 0, l = r - k + 1;
    while(r < nums.length){
        //elements in dq must be decreasing
        while(!dq.isEmpty() && nums[dq.peekLast()] <= nums[r]){
            dq.pollLast();
        }
        dq.offerLast(r);
        l = r - k + 1;
        //if num of elements > k, the elements in front of l is invalid
        if(dq.peekFirst() < l)
            dq.pollFirst();
        //get the result
        if(l >= 0)
            res[l] = nums[dq.peekFirst()];
        r++;
    }
    return res;
}
```