# Hashmap Solution: Two Sum

Iterate through the array and find the complement between the target and the current `nums` element. If the complement exists as a key inside of the hashmap, return the key's value, or index, and the current index. The key value pair for the hashmap is the `nums` element and its indice as a value.

## Code

```
    const twoSum = (nums. target) => {
        let map = new Map();

        for(let i = 0; i < nums.length; i++) {
            let complement = target - nums[i];

            if(map.has(complement)) {
                return [map.get(complement), i];
            }

            map.set(nums[i], i);
        }
    } //End
```

- Time Complexity: O(n)
- Space Complexity: O(n)
