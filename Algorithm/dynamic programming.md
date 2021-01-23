# Dynamic programming

## Medium

### 1. [Best Time to Buy and Sell Stock with Transaction Fee ](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-with-transaction-fee/)

```java
public int maxProfit(int[] prices, int fee) {
    int cash = 0, hold = -prices[0];
    for (int i = 1; i < prices.length; i++) {
        cash = Math.max(cash, hold + prices[i] - fee);
        hold = Math.max(hold, cash - prices[i]);
    }
    return cash;
}
```
## Hard

### 1. [Concatenated Words ](https://leetcode.com/problems/concatenated-words/)
```java
List<String> res = new ArrayList<>();
int count = 0;
public List<String> findAllConcatenatedWordsInADict(String[] words) {
    Set<String> setwords = new HashSet<>();
    for (String word : words) {
        setwords.add(word);
    }
    
    for (String word : words) {
        if (word == null || word.length() == 0) continue;
            
        if (dfs(word, 0, setwords, new HashMap<>())){
            res.add(word);
        }
    }

    return res;
}

private boolean dfs(String word, int startIndex, Set<String> words, Map<Integer, Boolean> memo) {

    if (memo.containsKey(startIndex)) return memo.get(startIndex);
    if (startIndex == word.length()) {
        return true;
    }
    
    if (startIndex >= word.length()) {
        return false;
    }
    
    for (int i = startIndex; i < word.length(); i++) {
        String str = word.substring(startIndex, i + 1);
        if (str.equals(word)) continue;

        if (!words.contains(str))  continue;
        
        boolean found = dfs(word, startIndex + str.length(), words, memo);
        if(found){
            memo.put(startIndex, true);
            return true;
        }
    }
    
    memo.put(startIndex, false);
    return false;
}
```