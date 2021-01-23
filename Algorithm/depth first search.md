# Depth first search

## Medium

### 1. [Minesweeper](https://leetcode.com/problems/minesweeper/)

```java
public char[][] updateBoard(char[][] board, int[] click) {
    int m = board.length;
    int n = board[0].length;
    int i = click[0];
    int j = click[1]; 
    if(board[i][j] == 'M'){
        board[i][j] = 'X';
        return board; 
    }
    else if(checkDigit(board, i, j) != 0){
        board[i][j] = Integer.toString(checkDigit(board, i, j)).charAt(0);
        return board; 
    } else {
        helper(board, i, j); 
    }
    return board;
}

public void helper(char[][] board, int i, int j){
    int m = board.length;
    int n = board[0].length;
    if(i < 0 || j < 0 || i >= m || j >= n || board[i][j] != 'E'){return;}
    if(board[i][j] == 'B'){return;}
    if(board[i][j] == 'M'){return;}
    if(checkDigit(board, i, j) != 0){
        board[i][j] = Integer.toString(checkDigit(board, i, j)).charAt(0);
        return;
    } else {
        board[i][j] = 'B';
        for(int k = i - 1; k < i + 2; k++){
            for(int l = j - 1; l < j + 2; l++){
                if(k == i && l == j) continue;
                helper(board, k, l);
            }
        }
    }
}

public int checkDigit(char[][] board, int i, int j){
    int m = board.length;
    int n = board[0].length;
    int digit = 0;
    for(int k = i - 1; k < i + 2; k++){
        for(int l = j - 1; l < j + 2; l++){
            if(k == i && l == j){continue;}
            if(k >= 0 && l >= 0 && k < m && l < n){
                if(board[k][l] == 'M'){
                    digit++;
                }
            }
        }
    }
    return digit;
}
```

## Hard

### 1. [Longest Consecutive Sequence ](https://leetcode.com/problems/longest-consecutive-sequence/)
```java
private boolean arrayContains(int[] arr, int num) {
    for (int i = 0; i < arr.length; i++) {
        if (arr[i] == num) {
            return true;
        }
    }

    return false;
}
public int longestConsecutive(int[] nums) {
    int longestStreak = 0;

    for (int num : nums) {
        int currentNum = num;
        int currentStreak = 1;

        while (arrayContains(nums, currentNum + 1)) {
            currentNum += 1;
            currentStreak += 1;
        }

        longestStreak = Math.max(longestStreak, currentStreak);
    }

    return longestStreak;
}
```