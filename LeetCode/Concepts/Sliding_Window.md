# Sliding Window

## Sliding Window Use Cases

1. Running Average
2. Formulating Adjacent Pairs
3. Target Value Identification
4. Longest/Shortest/Most Optimal Sequence

## Main Idea

To have a solution with two nested loops be just one loop. This decreases the time complexity from O(n<sup>2</sup>) or O(n<sup>3</sup>) to O(n). The idea is to keep track of sliding window, which is a fixed size subarray, while iterrating over the array. As the window slides across the orignal array, it keeps track of element that have were in the window.

## Fixed Window

A fixed window is when we have a predefined window size that stays contant as we iterrate through the orginal array. Usualy kept track with two pointer values each having an indice of the start/end of the subarray.

## Variable Window

A window size can change in size given under certain conditions. The window is also maintained with two pointers containing the indices of the current window representing teh start/end of the subarray.

## Resource

- [LeetCode Dicussion](https://leetcode.com/discuss/interview-question/3722472/mastering-sliding-window-technique-a-comprehensive-guide)
