# Hashmap Solution: Valid Anagram

First, check whether string input `s` and `t` are of the same length. If they are not the same length, return false. Next, create an empty hashmap named `map`. Then, iterate over each character in `s`, while iterating through `s`, set a key value pair in `map` such that the key is the character in `s` and the value is the number of instances of that character. We then iterate through `t` checking if each character in `t` is a key in `map`. If it is a key, we decrement the keys value pair by 1, then check whether that keys value is equal to zero. If the value is equal to zero, delete that key value pair from `map`. If the character in `t` does not exist in map, return false. If all characters in `t` are in `s`, the hashmap `map` should equal to zero because all the keys in `map` are also all characters in `s`. Therefore, we return `map.size === 0` to check if all characters were evaluated.

## Code

```
    const isAnagram = (s, t) => {
        if(s.length !== t.length) return false;

        const map = new Map();

        for(let key of s) {
            map.set(key, map.get(key) + 1 || 1);
        }

        for(let key of t) {
            if(map.has(key)) {
                map.set(key, map.get(key) - 1);

                if(map.get(key) === 0) map.delete(key);
            } else {
                return false;
            }
        }

        return map.size === 0;
    }
```

- Time Complexity: O(n)
- Space Complexity: O(n)
