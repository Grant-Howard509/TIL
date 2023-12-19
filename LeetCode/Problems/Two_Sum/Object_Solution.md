# Object Solution: Two Sum

Iterate through the array where for each indice, find its complement with respect to `target`. If the complement is in the object, then return that object's property value and the current index. if the complement is not in the object, create a new property being the current `nums` element with the property value being that element's index value.

## Code

```
    const twoSum = (nums, target) => {
        let numValues = {}; // Object used to store elements and there indicies

        for(let i = 0; i < nums.length; i++) {
            let complement = target - nums[i];

            if(numValues[complement] !== undefined) {
                return [numValues[complement], i];
            }

            numValues[nums[i]] = i;
        }

    } //End
```

- Time Complexity: O(n)
- Space Complexity: O(n)
