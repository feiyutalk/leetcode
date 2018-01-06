# 652. Find Duplicate Subtrees

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    public List<TreeNode> findDuplicateSubtrees(TreeNode root) {
        List<TreeNode> res = new ArrayList<>();
        postOrder(root, new HashMap<String, Integer>(), res);
        return res;
    }
    
    private String postOrder(TreeNode root, Map<String, Integer> map, List<TreeNode> res){
        if(root == null) return "#";
        String serial = root.val + "," + postOrder(root.left, map, res) + "," + postOrder(root.right, map, res);
        if(map.getOrDefault(serial, 0) == 1) res.add(root);
        map.put(serial, map.getOrDefault(serial, 0)+1);
        return serial;
    }
}
```

