# Binary Search Solution

## Concept: Divide and Conquer

## Steps

1. Create variables to keep track of the `startIndex`, `middleIndex`, and `endIndex`.
2. Start index will always be 0: `let startIndex = 0`.
3. End index will always be `let endIndex = array.length - 1`.
4. Find the middle index by finding the sum of `startIndex` and `endIndex` divided by 2. To avoid floating point values, use `Math.floor()` or `Math.ceil()` to round up/down.
5. Create a while loop with the following condition: `startIndex <= endIndex`
6. Determine if the `middleIndex`'s element is greater, or less than, the `target`.
7. If the `middleIndex`'s element is less than `target`, we assign `startIndex` as follows: `startIndex = middleIndex + 1`;
8. If the `middleIndex`'s element is greater than `target`, we assign the `endIndex` as follows: `endIndex = middleIndex - 1`;
9. If the `middelIndex` equal's the target, we have found our solution and return its index.
10. If `middleIndex` never equals `target`, we can assume `target` does not exist in the array and return -1;

# Resource

- [Medium](https://medium.com/@jeffrey.allen.lewis/javascript-algorithms-explained-binary-search-25064b896470)
