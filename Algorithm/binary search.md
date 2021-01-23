# Binary Search

## Medium 

### 1. [Minimum Sorted Rotated Array](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/)
```java
public int findMin(int[] nums) {
// If the list has just one element then return that element.
    if (nums.length == 1) {
        return nums[0];
}

// initializing left and right pointers.
int left = 0, right = nums.length - 1;

// if the last element is greater than the first element then there is no rotation.
// e.g. 1 < 2 < 3 < 4 < 5 < 7. Already sorted array.
// Hence the smallest element is first element. A[0]
if (nums[right] > nums[0]) {
    return nums[0];
}

// Binary search way
while (right >= left) {
    // Find the mid element
    int mid = left + (right - left) / 2;

    // if the mid element is greater than its next element then mid+1 element is the smallest
    // This point would be the point of change. From higher to lower value.
    if (nums[mid] > nums[mid + 1]) {
        return nums[mid + 1];
    }

    // if the mid element is lesser than its previous element then mid element is the smallest
    if (nums[mid - 1] > nums[mid]) {
        return nums[mid];
    }

    // if the mid elements value is greater than the 0th element this means
    // the least value is still somewhere to the right as we are still dealing with elements
    // greater than nums[0]
    if (nums[mid] > nums[0]) {
        left = mid + 1;
    } else {
    // if nums[0] is greater than the mid value then this means the smallest value is somewhere to
    // the left
        right = mid - 1;
    }

    return -1;
}
```
## Hard

### 1. [Median of Two Sorted Arrays](https://leetcode.com/problems/median-of-two-sorted-arrays/)

```java
 public double findMedianSortedArrays(int[] A, int[] B) {
    int m = A.length;
    int n = B.length;
    if (m > n) { // to ensure m<=n
        int[] temp = A; A = B; B = temp;
        int tmp = m; m = n; n = tmp;
    }
    int iMin = 0, iMax = m, halfLen = (m + n + 1) / 2;
    while (iMin <= iMax) {
        int i = (iMin + iMax) / 2;
        int j = halfLen - i;
        if (i < iMax && B[j-1] > A[i]){
            iMin = i + 1; // i is too small
        }
        else if (i > iMin && A[i-1] > B[j]) {
            iMax = i - 1; // i is too big
        }
        else { // i is perfect
            int maxLeft = 0;
            if (i == 0) { maxLeft = B[j-1]; }
            else if (j == 0) { maxLeft = A[i-1]; }
            else { maxLeft = Math.max(A[i-1], B[j-1]); }
            if ( (m + n) % 2 == 1 ) { return maxLeft; }

            int minRight = 0;
            if (i == m) { minRight = B[j]; }
            else if (j == n) { minRight = A[i]; }
            else { minRight = Math.min(B[j], A[i]); }

            return (maxLeft + minRight) / 2.0;
        }
    }
    return 0.0;
}
```