# Built in JS Solution

## Steps

1. First, create a `regex` expression that removes non-alphanumerics in the given string: `/[^A-Za-z0–9]/g`.
2. We first use the `toLowerCase` method to return a string that has only lowercase letters.
3. The `replace` method to replace all characters that are non-alphanumeric values to an empty string `""`.
4. The `split` method is called which splits our string into a subarray of strings. In this case, elements of characters from our string value.
5. The `reverse` method reverses the order of the array.
6. Lastly, the `join` method joins all of the elements of the array into a string.
7. We assign the lowercase no spaced string value to a string variable called `original`.
8. We also assign the reversed string to a string variable called `reverse`
9. If the pair do not match, return false, else return true.

## Code

```
const isPalindrome = (s) = {


   const reg = /[^A-Za-z0–9]/g;


   const original = s.toLowerCase().replace(reg, '');


   const reverse = original.split('').reverse().join('');


   return original === reverse;
}
```

- Time Complexity: O(N)
- Space Complexity: O(N)
