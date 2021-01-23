# Greedy

## Medium

### 1. [Jump Game ](https://leetcode.com/problems/jump-game/)
```java
Index[] memo;

public boolean canJumpFromPosition(int position, int[] nums) {
    if (memo[position] != Index.UNKNOWN) {
        return memo[position] == Index.GOOD ? true : false;
    }

    int furthestJump = Math.min(position + nums[position], nums.length - 1);
    for (int nextPosition = position + 1; nextPosition <= furthestJump; nextPosition++) {
        if (canJumpFromPosition(nextPosition, nums)) {
            memo[position] = Index.GOOD;
            return true;
        }
    }

    memo[position] = Index.BAD;
    return false;
}

public boolean canJump(int[] nums) {
    memo = new Index[nums.length];
    for (int i = 0; i < memo.length; i++) {
        memo[i] = Index.UNKNOWN;
    }
    memo[memo.length - 1] = Index.GOOD;
    return canJumpFromPosition(0, nums);
}
```
## Hard

### 1. [IPO](https://leetcode.com/problems/ipo/)
```java
public int findMaximizedCapital(int k, int W, int[] Profits, int[] Capital) {
    int N = Profits.length;
    Set<Integer> set = new HashSet<>();
    PriorityQueue<Integer> maxPQ = new PriorityQueue<>(new Comparator<Integer>() {
        @Override
        public int compare(Integer o1, Integer o2) {
            return o2 - o1;
        }
    });

    for(int i = 0; i < N; i++) {
        if(Capital[i] <= W) {
            maxPQ.add(Profits[i]);
        } else {
            set.add(i);
        }
    }

    for(int i = 0; i < k && !maxPQ.isEmpty(); i++) {
        W += maxPQ.poll();
        for (Iterator<Integer> it = set.iterator(); it.hasNext();) {
            Integer index = it.next();
            if(Capital[index] <= W) {
                maxPQ.add(Profits[index]);
                it.remove();
            }
        }
    }

    return W;
}
```