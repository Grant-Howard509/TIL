# Stack Solution

## Steps:

1. Declare an empty stack called `stack`.
2. Iterate through the each character in string `s`.
3. Check if the current character in string `s` is an opening bracket.
4. If true, push the opening bracket character to the top of `stack`.
5. If false, the current character is a closing bracket.
6. Check if the closing bracket and the top of the stack are the same type.
7. If they are the same type, pop the stack.
8. After iterating through the entire string, check if the `stack` is empty to confirm all open and closed bracket pair were found.
9. Return true is `stack` was empty, false if `stack` is not empty.

## Code:

```
const isValid = (s) => {
    const stack = [];

    for(let i = 0; i < s.length; i++) {
        if(s[i] === '(' || s[i] === '[' || s[i] === '{') {
            stack.push(s[i]);
        }else if (s[i] === ')' && stack[stack.length - 1] === '(') {
            stack.pop();
        } else if ( s[i] === ']' && stack[stack.length - 1] === '['){
           stack.pop();
        } else if(s[i] === '}' && stack[stack.length - 1] === '{') {
            stack.pop();
        } else {
            return false;
        }
    }

    return stack.length === 0;
}
```

- Time Complexity: O(n)
- Space Complexity: O(n)
