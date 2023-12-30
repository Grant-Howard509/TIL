# Recusive Solution

## Concept: Divide and Conquer

Steps:

1. Create a base case which checks if the root is null, if true, return the root node.
2. If the root is not null, make a recusive call to the function with `root.left` as an argument.
3. Do the same thing in step `2` but with `root.right` as an argument.
4. Once both recusive calls are complete, swap `root.left` with `root.right`.
5. Finally, return the root node.

## Code

```
const invertTree = (root) => {
    if(root === null) return root;

    invertTree(root.left);

    invertTree(root.right);

    let prevLeft = root.left;
    root.left = root.right;
    root.right = prevLeft;

    return root;
};
```

- Time Complexity: O(2<sup>n</sup>)
- Space Complexity: O(1)
