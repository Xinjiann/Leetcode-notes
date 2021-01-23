# Backtracking

## Medium

### 1. [Combinations Sum](https://leetcode.com/problems/combination-sum/)
```java
List<List<Integer>> result=new ArrayList<>();
    
public List<List<Integer>> combinationSum(int[] candidates, int target) {
    List<Integer> list=new ArrayList<>();

    //It is just like unbounded Knapsack
    combinationSumRec(candidates,candidates.length,target,list);
    return result;
}


public void combinationSumRec(int[] arr,int i,int target,List<Integer> list) {
    
    if(i<=0|| target<0)
    {
        list.clear();
        return;
    }
    
    if(target==0)
    {
        result.add(new ArrayList<Integer>(list));
        list.clear();
        return;
    }
    
    
    if(arr[i-1]<=target)
    {
        //Creating new copy and send to Rec just like appending String
        List<Integer> list2=new ArrayList<>();
        list2.addAll(list);
        list2.add(arr[i-1]);
        combinationSumRec(arr,i,target-arr[i-1],list2);
        //combinationSumRec(arr,i,target-arr[i-1],ans+","+arr[i-1],list2);
        //combinationSumRec(arr,i-1,target,ans,list); //Exclude
    }
    
    combinationSumRec(arr,i-1,target,list);
}
```
## Hard

### 1. [Remove Invalid Parentheses ](https://leetcode.com/problems/remove-invalid-parentheses/)
```java
private Set<String> validExpressions = new HashSet<String>();
private int minimumRemoved;

private void reset() {
this.validExpressions.clear();
this.minimumRemoved = Integer.MAX_VALUE;
}

private void recurse(
    String s,
    int index,
    int leftCount,
    int rightCount,
    StringBuilder expression,
    int removedCount) {

// If we have reached the end of string.
if (index == s.length()) {

    // If the current expression is valid.
    if (leftCount == rightCount) {

    // If the current count of removed parentheses is <= the current minimum count
        if (removedCount <= this.minimumRemoved) {

            // Convert StringBuilder to a String. This is an expensive operation.
            // So we only perform this when needed.
            String possibleAnswer = expression.toString();

            // If the current count beats the overall minimum we have till now
            if (removedCount < this.minimumRemoved) {
            this.validExpressions.clear();
            this.minimumRemoved = removedCount;
            }
            this.validExpressions.add(possibleAnswer);
        }
    }
} else {

    char currentCharacter = s.charAt(index);
    int length = expression.length();

    // If the current character is neither an opening bracket nor a closing one,
    // simply recurse further by adding it to the expression StringBuilder
    if (currentCharacter != '(' && currentCharacter != ')') {
        expression.append(currentCharacter);
        this.recurse(s, index + 1, leftCount, rightCount, expression, removedCount);
        expression.deleteCharAt(length);
    } else {

        // Recursion where we delete the current character and move forward
        this.recurse(s, index + 1, leftCount, rightCount, expression, removedCount + 1);
        expression.append(currentCharacter);

        // If it's an opening parenthesis, consider it and recurse
        if (currentCharacter == '(') {
            this.recurse(s, index + 1, leftCount + 1, rightCount, expression, removedCount);
        } else if (rightCount < leftCount) {
            // For a closing parenthesis, only recurse if right < left
            this.recurse(s, index + 1, leftCount, rightCount + 1, expression, removedCount);
        }

    // Undoing the append operation for other recursions.
        expression.deleteCharAt(length);
        }
}
}

public List<String> removeInvalidParentheses(String s) {

    this.reset();
    this.recurse(s, 0, 0, 0, new StringBuilder(), 0);
    return new ArrayList(this.validExpressions);
}

```