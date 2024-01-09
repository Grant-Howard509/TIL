# Recursive Solution

### Concept: Recursion

## Steps

1. Create a base case that checks for `array out of bound` errors and if the image not equal to the initial color. If any of these conditions are true, return nothing.
2. If the base case is false, change the current node's color to the new color.
3. Recursively call the function with indices representing each of the 4-directional (up, down, left, right) nodes.
4. Once the recursive call is finished, return the image.

## Code

```
const floodFill = function(image, sr, sc, newColor) {
   if(image[sr][sc] === newColor) return image;


   flood(image, image[sr][sc], sr, sc, newColor);


   return image;
};


const flood = function(image, color, sr, sc, newColor) {
   if( sr < 0 || sc < 0 || sr >= image.length || sc >= image[0].length || image[sr][sc] != color) return


   image[sr][sc] = newColor;


   flood(image, color, sr + 1, sc, newColor);
   flood(image, color, sr - 1, sc, newColor);
   flood(image, color, sr, sc + 1, newColor);
   flood(image, color, sr, sc - 1, newColor);
}
```

- Time Complexity: O(M \* N)
- Space Complexity: O(M + N)
