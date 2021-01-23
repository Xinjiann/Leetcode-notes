# Breadth first search

## Medium

### 1. [Binaray Tree Level Order Traversal](https://leetcode.com/problems/binary-tree-level-order-traversal/)

```java
public List<List<Integer>> levelOrder(TreeNode root) {
    if (root == null) {
        return Collections.EMPTY_LIST;
    }
    return bfs(root);
}

private List<List<Integer>> bfs(TreeNode root) {
    List<List<Integer>> result = new ArrayList<>();
    Queue<TreeNode> q = new LinkedList<>();
    q.offer(root);
    
    while(!q.isEmpty()) {
        List<Integer> list = new ArrayList<>();
        int size = q.size();
        for (int i = 0; i < size; i++) {
            TreeNode currentNode = q.poll();
            list.add(currentNode.val);
            
            if (currentNode.left != null) {
                q.offer(currentNode.left);
            }
            if (currentNode.right != null) {
                q.offer(currentNode.right);
            }
        }
        result.add(list);
    }
    return result;
}
```
## Hard

### 1. [Cut Off Trees for Golf Event ](https://leetcode.com/problems/cut-off-trees-for-golf-event/)

```java

int[] dr = {-1, 1, 0, 0};
int[] dc = {0, 0, -1, 1};

public int cutOffTree(List<List<Integer>> forest) {
    List<int[]> trees = new ArrayList();
    for (int r = 0; r < forest.size(); ++r) {
        for (int c = 0; c < forest.get(0).size(); ++c) {
            int v = forest.get(r).get(c);
            if (v > 1) trees.add(new int[]{v, r, c});
        }
    }

    Collections.sort(trees, (a, b) -> Integer.compare(a[0], b[0]));

    int ans = 0, sr = 0, sc = 0;
    for (int[] tree: trees) {
        int d = dist(forest, sr, sc, tree[1], tree[2]);
        if (d < 0) return -1;
        ans += d;
        sr = tree[1]; sc = tree[2];
    }
    return ans;
}
```