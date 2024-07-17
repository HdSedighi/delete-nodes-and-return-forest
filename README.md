# Intuition
 We need to split a binary tree into a forest after deleting specified nodes. The nodes to delete are given in an array.

# Approach

To solve the problem, we can use a recursive approach to traverse the tree:
1. Start from the root and recursively process each node.
2. Check if the current node's value is in the set of nodes to delete.
3. If the current node is marked for deletion and it's also a root (not a child of any other node), skip adding it to the forest.
4. Recursively process the left and right children of the current node.
5. If a node is not deleted and it's a root (marked by the `isRoot` flag), add it to the forest.
6. Return `null` for nodes that are marked for deletion to remove them from the tree structure.

By using recursion and maintaining a list (`forest`) to collect roots of valid trees after deletion, we can efficiently split the binary tree into a forest.


# Complexity
- Time complexity:

The time complexity is O(n), where n is the number of nodes in the binary tree. We visit each node once to check if it should be deleted and to adjust the tree structure accordingly.


- Space complexity:

The space complexity is O(n) in the worst case due to the recursion stack and the space used by the `forest` list to store the roots of remaining trees. The additional space used by the `toDeleteSet` is O(d), where d is the number of nodes to delete.


# Code
```
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     public int val;
 *     public TreeNode left;
 *     public TreeNode right;
 *     public TreeNode(int val=0, TreeNode left=null, TreeNode right=null) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
public class Solution {
    public IList<TreeNode> DelNodes(TreeNode root, int[] to_delete) {
        HashSet<int> toDeleteSet = new HashSet<int>(to_delete);
        List<TreeNode> forest = new List<TreeNode>();
        
        DelNodesHelper(root, toDeleteSet, true, forest);
        
        return forest;
    }
    
    private TreeNode DelNodesHelper(TreeNode node, HashSet<int> toDeleteSet, bool isRoot, List<TreeNode> forest) {
        if (node == null) return null;
        
        bool deleted = toDeleteSet.Contains(node.val);
        
        if (isRoot && !deleted) {
            forest.Add(node);
        }
        
        node.left = DelNodesHelper(node.left, toDeleteSet, deleted, forest);
        node.right = DelNodesHelper(node.right, toDeleteSet, deleted, forest);
        
        return deleted ? null : node;   
    }
}
```
