# [Integer addition in array form](https://leetcode-cn.com/problems/add-to-array-form-of-integer/)

For non-negative integer X, the array form of X is an array formed by each digit in the order from left to right. For example, if X = 1231, then its array form is [1,2,3,1].

Given the array form A of non-negative integer X, return the array form of integer X+K.

## Solution

```java
class Solution {
    public List<Integer> addToArrayForm(int[] A, int K) {

        int n = A.length;
        List<Integer> res = new ArrayList<>();

        for (int i = n-1; i>0; --i){
            int sum = A[i]+K%10;
            K = K/10;
            if (sum >= 10){
                sum -= 10;
                K += 1;
            }
            res.add(sum);
        }
        for (; K > 0;K /= 10) {
            res.add(K % 10);
        }

        Collections.reverse(res);
        return res;

    }
}
```

