# Recover-Binary-Search-Tree

This solution fixes a binary search tree (BST) where exactly two nodes have been swapped by mistake, restoring the BST to its correct form without altering its structure. The tree needs to be recovered while maintaining the properties of the BST: for every node, the left subtree contains values less than the node’s value, and the right subtree contains values greater than the node’s value.

Approach:
Perform an in-order traversal of the tree to identify the two nodes that are out of order.
Swap the values of these nodes to restore the tree's structure.
The solution ensures that the tree's shape remains unchanged, and only the values of the incorrect nodes are fixed.

This approach runs in O(n) time, where 𝑛 is the number of nodes in the tree, and uses O(h) space, where h is the height of the tree.

class Solution:
    def recoverTree(self, root: Optional[TreeNode]) -> None:
        traverse_lst = []
        violated_pairs = []
        prev = None

    
        def get_violated_pairs():
            node1, node2 = None, None
            if len(violated_pairs) == 1:
                node1, node2 = violated_pairs[0] # case 1
            else:
                node1, node2 = violated_pairs[0][0], violated_pairs[1][1] # case 2
            
            return node1, node2
                

        def inorder(node):
            nonlocal prev
            if node:
                inorder(node.left)
                if prev and node.val < prev.val:
                    violated_pairs.append((prev, node))
                traverse_lst.append(node.val)
                prev = node
                inorder(node.right)
        
        inorder(root)
        a, b  = get_violated_pairs()       
        a.val, b.val = b.val, a.val

