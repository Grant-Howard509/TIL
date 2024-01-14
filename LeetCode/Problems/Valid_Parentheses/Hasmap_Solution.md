# Hashmap Solution

## Steps:

1. Create a hasmap called `map` that contains all of the closing tags as `keys` and opening tags as the `value`.
2. Create an empty stack called = `openBracketStack`.
3. Iterate through each character in the string.
4. Check if the character is a key in `map` and if that key has the same value as the top of `openBracketStack`.
5. If the condition is true, then pop the `openBracketStack`, else push the character onto the `openBracketStack`.
6. After iterating through the entire string, check if `openBracketStack` is empty.
7. If the `openBracketStack` is empty, return true, else false.

## Code:

```
const isValid = (s) = {
    const map = new Map([
        [')', '('],
        ['}', '{'],
        [']', '[']
    ]);

    const openBracketStack = [];

    for(let i = 0; i < s.length; i++>) {
        if(map.has(s[i] && map.get(s[i]) === openBracketStack[openBrackStack.length - 1])){
            openBracketStack.pop();
        }else {
            openBracketStack.push(s[i]);
        }
    }

    return openBracketStack.length === 0;
}
```

- Time Complexity: O(n)
- Space Complexity: O(n)
