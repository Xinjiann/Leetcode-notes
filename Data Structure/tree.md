# Tree

## Easy
### 1. [Lowest Common Ancestor of a BST](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-tree/)

```java
private TreeNode ans;

public Solution() {
    // Variable to store LCA node.
    this.ans = null;
}

private boolean recurseTree(TreeNode currentNode, TreeNode p, TreeNode q) {

    // If reached the end of a branch, return false.
    if (currentNode == null) {
        return false;
    }

    // Left Recursion. If left recursion returns true, set left = 1 else 0
    int left = this.recurseTree(currentNode.left, p, q) ? 1 : 0;

    // Right Recursion
    int right = this.recurseTree(currentNode.right, p, q) ? 1 : 0;

    // If the current node is one of p or q
    int mid = (currentNode == p || currentNode == q) ? 1 : 0;


    // If any two of the flags left, right or mid become True
    if (mid + left + right >= 2) {
        this.ans = currentNode;
    }

    // Return true if any one of the three bool values is True.
    return (mid + left + right > 0);
}

public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
    // Traverse the tree
    this.recurseTree(root, p, q);
    return this.ans;
}
```
## Medium

### 1. [Binaray Tree Right Side View ](https://leetcode.com/problems/binary-tree-right-side-view/)
```java
private int maxDepth;
private void rightSideViewUtil(TreeNode root, int currDepth, List<Integer> view){
    if(root == null){
        return;
    }
    if(currDepth > this.maxDepth){
        // add element here
        view.add(root.val);
        this.maxDepth = currDepth;
    }
    if(root.right != null){
        rightSideViewUtil(root.right, currDepth+1, view);
    }
    if(root.left != null){
        rightSideViewUtil(root.left, currDepth+1, view);
    }
} 
public List<Integer> rightSideView(TreeNode root) {
    List<Integer> view = new ArrayList<Integer>();
    this.maxDepth = 0;
    if(root == null){
        return view;
    }
    rightSideViewUtil(root, 1, view);
    return view;
}
```
## Hard

### 1. [Binary Tree Maximum Path Sum](https://leetcode.com/problems/binary-tree-maximum-path-sum/)

```java
int max = Integer.MIN_VALUE;

protected int helper(TreeNode root){

    if (root == null) return 0;
   
    int left = Math.max(0, helper(root.left));
    int right = Math.max(0, helper(root.right));
    
    max = Math.max(max , left + right + root.val);
 
 
    return root.val + Math.max(left, right);
}
public int maxPathSum(TreeNode root) {
    helper(root);
    return max;
}

```