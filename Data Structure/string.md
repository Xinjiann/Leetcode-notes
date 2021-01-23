# String 

## Easy

### 1. [First Unique Character In a String](https://leetcode.com/problems/first-unique-character-in-a-string/)

```java
public int firstUniqChar(String s) {
    HashMap<Character, Integer> count = new HashMap<Character, Integer>();
    int n = s.length();
    // build hash map : character and how often it appears
    for (int i = 0; i < n; i++) {
        char c = s.charAt(i);
        count.put(c, count.getOrDefault(c, 0) + 1);
    }
    
    // find the index
    for (int i = 0; i < n; i++) {
        if (count.get(s.charAt(i)) == 1) 
            return i;
    }
    return -1;
}
```

## Medium

### 1. [Reverse Words In a String](https://leetcode.com/problems/reverse-words-in-a-string/)
```java
public String reverseWords(String s) {
        s=s.trim();
        String []arr=s.split("\\s+");
        String ans="";
        for(String i:arr){
            ans=i+" "+ans;
        }
        return ans.substring(0,ans.length()-1);
    }
```

## Hard

### 1. [Text Justification](https://leetcode.com/problems/text-justification/)

```java
public List<String> fullJustify(String[] words, int maxWidth) {
    List<String> ans = new ArrayList<>();
    
    int l = 0;
    int len = 0;
    
    for (int i = 0; i < words.length; i++) {
        // total len so far + current word + min spaces
        if (len + words[i].length() + (i - l) > maxWidth) {
            // justify
            int totalSpaces = maxWidth - len;
            int minSpaces = (i - l - 1) == 0 ? 0 : totalSpaces / (i - l - 1);
            int extraSpaces = totalSpaces - minSpaces * (i - l - 1);
            
            StringBuilder sb = new StringBuilder();
            
            for (int j = l; j < i; j++) {
                sb.append(words[j]);
                
                for (int k = 0; k < minSpaces && j + 1 != i; k++) {
                    sb.append(' ');
                }
                
                if (extraSpaces > 0) {
                    sb.append(' ');
                    extraSpaces--;
                }
                
                while (minSpaces == 0 && extraSpaces > 0) {
                    sb.append(' ');
                    extraSpaces--;
                }                    
            }
            
            ans.add(sb.toString());
            
            len = 0;
            l = i;
        }    
        
        len += words[i].length();
    }
    
    // last line if required
    StringBuilder sb = new StringBuilder();
    for (int i = l; i < words.length; i++) {
        sb.append(words[i]);
        
        if (i + 1 != words.length)
            sb.append(' ');
    }
    
    while (sb.length() < maxWidth)
        sb.append(' ');
    
    ans.add(sb.toString());
    
    return ans;
}
```