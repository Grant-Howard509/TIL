# For Loop Solution JS

## Steps

1. Create a regex expression that matches non-alphanumeric values: `/[^A-Za-z0–9]/g`.
2. Use the built-in methods `toLowerCase` to make all characters lowercase and `replace` to replace all non-alphanumerics that match the regex expression to an empty string.
3. Loop through each character in the string.
4. Create a condition that checks if the string at index `i` matches the string parallel to the index: `s[s.length - 1 - i]`.
5. If the two characters do not match, return false, else if all characters match return true.

## Code:

```
const isPalindrome = (s) = {
   const reg = /[^A-Za-z0–9]/g;


   s = s.toLowerCase().replace(reg, '');


   let len = s.length;


   for(let i = 0; i < len / 2; i++){
       if(s[i] !== s[len - 1 - i]){
           return false;
       }
   }


   return true;
}
```

- Time Complexity: O(n)
- Space Complexity = O(1)
