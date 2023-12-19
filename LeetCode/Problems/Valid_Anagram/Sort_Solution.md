# Sort Solution: Valid Anagram

First, check if the two string inputs, `s` and `t`, are of the same length. If they are not the same length, return false. If they are the same length, convert both `s` and `t` to and array using `Array.split('')`, sort using `Array.sort()`, and join the array elements back together as a string using `Array.join('')`.

NOTE: `Array.split('')` and `Array.join('')` time complexity is `O(n)`, and `Array.sort()` is `O(logn)`.

## Code

```
    const isAnagram = (s, t) => {
        if(s.length !== t.length) return false;

        return s.split('').sort().join('') === t.split('').sort().join('');
    }
```

- Time Complexity: O(nlogn)
- Space Complexity: O(n)
