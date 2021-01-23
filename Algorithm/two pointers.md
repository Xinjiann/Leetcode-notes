# Two Pointers

## Medium

### 1. [Longest Substring Witout Repeats](https://leetcode.com/problems/longest-substring-without-repeating-characters/)

```java
public int lengthOfLongestSubstring(String s) {
 
        
    if (s==null || s.length() < 1) {
        return 0;
    }         
    int rs = 0;
    char[] arr = s.toCharArray();
    Map<Character, Integer> map = new HashMap<>();
    int i = 0, j = 0;
    while (j < arr.length) {
        Integer prePos = map.get(arr[j]);
        if (prePos != null && prePos >= i) {    
            i = prePos + 1;
        }            
        rs = Math.max(rs, j - i + 1 ); 
        map.put(arr[j], j);
        j++;            
    }        
    return rs;
}
```

## Hard

### 1. [Trapping Rain Water](https://leetcode.com/problems/trapping-rain-water/)

```java
if(len == 0) return 0;
    
    int[] maxL = new int[len];
    int[] maxR = new int[len];
    int sum = 0;
    
    maxL[0] = h[0];
    for(int left = 1; left < len; left++){
        maxL[left] = Math.max(maxL[left - 1], h[left]);
    }
    
    maxR[len - 1] = h[len - 1];
    for(int right = len - 2; right >= 0; right--){
        maxR[right] = Math.max(maxR[right + 1], h[right]);
    }
    
    for(int i = 0; i < len; i++){
        int tmp = Math.min(maxL[i], maxR[i]);
        sum += tmp - h[i];
    }
    return sum;
}
```