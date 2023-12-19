# Stack Solution: Two Sum

Iterate through the array, then check all other indices ahead of it and determine whether both indices add up to the `target`. If both add up to the `target`, push each indice to the stack and return the stack.

## Code

```
    const twoSum = (nums, target) => {
        let indexes = []; // The "stack"

        for(let i = 0; i < nums.length; i++) {
            for(let j = i + 1; j < nums.length; j++) {
                if(nums[i] + nums[j] === target) {
                    indexes.push(i);
                    indexes.push(j);
                }
            }
        }

        return indexes; // returns "[i,j]"

    } //End
```

- Time Complexity: O(n<sup>2</sup>)
- Space Complexity: O(1)
