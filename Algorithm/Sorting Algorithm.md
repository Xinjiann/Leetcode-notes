# Sorting Algorithm

[useful link](https://www.cs.usfca.edu/~galles/visualization/Algorithms.html)

[Leetcode Problems](#Bubble&nbspSort)

## 1. Bubble Sort 冒泡排序
思路：遍历数组，两两对比， 大的放后面，保证最大的元素放到队尾，然后保持队尾不变，重新遍历。
```java
private void bubbleSort(int[] nums) {
    for (int i = nums.length - 1; i >= 1; i--) { 
        for (int j = 1; j <= i; j++) {
            if (nums[j-1]>nums[j])
                swap(nums, j, j-1);           
        }
    }
}
```

## 2. Selection Sort 选择排序
思路：和 Bubble Sort类似，只是不用每次对比都交换，而是将n个数中的最大数放到队尾。
```java
private void selectionSort(int[] nums) {
    for (int i = nums.length - 1; i > 0; i--) {
        int maxIndex = 0;         // 最大元素的位置
        for (int j = 0; j <= i; j++) {
            if (nums[maxIndex]<nums[j]) {
                maxIndex = j;
            }
        }
        swap(nums, maxIndex, i);   // 把这个最大的元素移到最后
    }
}
```

## 3. Insertion Sort 插入排序
思路：遍历数组，将每个元素插入其之前已排序列表中，并排序。for循环嵌套while循环
```java
public int[] sortArray(int[] nums) {
    int len = nums.length;

    for (int i = 1; i < len; i++) {

        int temp = nums[i];
        int j = i;

        while (j > 0 && nums[j - 1] > temp) {
            nums[j] = nums[j - 1];
            j--;
        }
        nums[j] = temp;
    }
    return nums;
}
```
- 时间复杂度：O(N^2)，这里 N 是数组的长度；
- 空间复杂度：O(1)，使用到常数个临时变量

[leetcode problem 147]()

## 3. Merge Sort 归并排序
思路：分而治之（divide-and-conquer），把原来的数组变成左右两个数组，然后分别进行排序，当左右的子数组排序完毕之后，
再合并这两个子数组形成一个新的排序数组。整个过程递归进行，当只剩下一个元素或者没有元素的时候就直接返回。
```java
private void mergeSort(int[] nums, int left, int right) {  
    if (left >= right) return;
    int mid = (left+right) / 2;

    mergeSort(nums, left, mid);                        
    mergeSort(nums, mid+1, right);

    int[] temp = new int[right-left+1];              
    int i=left,j=mid+1;
    int cur = 0;
    while (i<=mid&&j<=right) {                            
        if (nums[i]<=nums[j]) temp[cur] = nums[i++];
        else temp[cur] = nums[j++];
        cur++;
    }
    while (i<=mid) temp[cur++] = nums[i++];
    while (j<=right) temp[cur++] = nums[j++];

    for (int k = 0; k < temp.length; k++) {          
        nums[left+k] = temp[k];
    }
}
```
时间复杂度：O(nlogn)
空间复杂度：O(n)

## 4. Quick Sort 快速排序

思路：取第一个元素（或者最后一个元素）作为分界点，把整个数组分成左右两侧，左边的元素小于或者等于分界点元素，
而右边的元素大于分界点元素，然后把分界点移到中间位置，对左右子数组分别进行递归，最后就能得到一个排序完成的数组。当子数组只有一个或者没有元素的时候就结束这个递归过程。

```java
private void quickSort(int[] nums, int left, int right) {
    if (left >= right) return;
    int lo = left+1;               // 小于分界点元素的最右侧的指针
    int hi = right;                // 大于分界点元素的最左侧的指针
    while (lo<=hi) {
        if (nums[lo]>nums[left]) { // 交换元素确保左侧指针指向元素小于分界点元素
            swap(nums, lo, hi);
            hi--;
        } else {
            lo++;
        }
    }
    lo--;                          // 回到小于分界点元素数组的最右侧
    swap(nums, left, lo);          // 将分界点元素移到左侧数组最右侧
    quickSort2(nums, left, lo-1);
    quickSort2(nums, lo+1, right);
}
```
时间复杂度：O(nlogn)
空间复杂度：O(logn)

# Leetcode Problems
