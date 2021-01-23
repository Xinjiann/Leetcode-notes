# Stack

## Easy

### 1。[Min Stack](https://leetcode.com/problems/min-stack/)

```java
private Stack<Helper> stack=null;
Integer min;
public MinStack() {
    this.stack= new Stack();
}

public void push(int x) {
    if(min ==null){
        this.min=x;
    }
    this.min=Math.min(this.min,x);
    this.stack.push(new Helper(x,this.min));
}

public void pop() {
    this.stack.pop();
    this.min=stack.isEmpty()? null : stack.peek().min;
}

public int top() {
    return this.stack.peek().val;
}

public int getMin() {
    return this.stack.peek().min;
}
}

class Helper{
int val;
int min;
public Helper(int val, int min){
    this.val=val;
    this.min=min;
}
```
## Medium

### 1. [Exclusive Time of Functions](https://leetcode.com/problems/exclusive-time-of-functions/)

```java
public int[] exclusiveTime(int n, List < String > logs) {
    Stack < Integer > stack = new Stack < > ();
    int[] res = new int[n];
    String[] s = logs.get(0).split(":");
    stack.push(Integer.parseInt(s[0]));
    int i = 1, time = Integer.parseInt(s[2]);
    while (i < logs.size()) {
        s = logs.get(i).split(":");
        while (time < Integer.parseInt(s[2])) {
            res[stack.peek()]++;
            time++;
        }
        if (s[1].equals("start"))
            stack.push(Integer.parseInt(s[0]));
        else {
            res[stack.peek()]++;
            time++;
            stack.pop();
        }
        i++;
    }
    return res;
}
```
## Hard

### 1. [Largest Rectangle In Histogram ](https://leetcode.com/problems/largest-rectangle-in-histogram/)

```java
public int largestRectangleArea(int[] heights) {
    int maxArea = 0;
    List<int[]> stack = new ArrayList<>(); // list of pair: [index, height]
    
    for (int i = 0; i < heights.length; i++) {
        int start = i;
        
        while (stack.size() > 0 && stack.get(stack.size() - 1)[1] > heights[i]) {
            int height = stack.get(stack.size() - 1)[1];
            int width = i - stack.get(stack.size() - 1)[0];
            maxArea = Math.max(maxArea, height * width);
            start = stack.get(stack.size() - 1)[0];
            stack.remove(stack.size() - 1);
        }
        stack.add(new int[]{start, heights[i]});
    }
    for (int i = 0; i < stack.size(); i++) {
        int height = stack.get(i)[1], start = stack.get(i)[0];
        int area = height * (heights.length - start);
        maxArea = Math.max(area, maxArea);
    }
    return maxArea;
}
```