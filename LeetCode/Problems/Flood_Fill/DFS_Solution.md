# DFS Solution

### Concept: Depth First Search

## Steps:

1. Create a stack that stores the initial indice values as an array.
2. Change the initial position color to the new color value.
3. Create a while loop where the condition states that the stack cannot be empty.
4. Pop the stack and store its contents into the variable `current`.
5. Get both x and y indices from `current`.
6. Check the edge cases for the 4-directional (up, down, left, right) positions relative to the `current` position.
7. If the edge cases are false, push the new position to the stack and change the new position color to the new color.
8. Once the stack is empty, return the image.

## Code:

```
const flood = function(image, color, sr, sc, newColor) {


   let stack = [[sr, sc]];


   image[sr][sc] = newColor;


   while(stack.length > 0) {
       let current = stack.pop();


       let posX = current[0];
       let posY = current[1];


       if(isValid(image, color, posX + 1, posY)) {
           stack.push([posX + 1, posY]);
           image[posX + 1][posY] = newColor;
       }


       if(isValid(image, color, posX - 1, posY)) {
           stack.push([posX - 1, posY]);
           image[posX - 1][posY] = newColor;
       }


       if(isValid(image, color, posX, posY + 1)) {
           stack.push([posX, posY + 1]);
           image[posX][posY + 1] = newColor;
       }


       if(isValid(image, color, posX, posY - 1)) {
           stack.push([posX, posY - 1]);
           image[posX][posY - 1] = newColor;
       }
   }


   return image;
}


const isValid = function(image, color, sr, sc) {
   if(sr < 0 || sc < 0 || sr >= image.length || sc >= image[0].length || image[sr][sc] != color) {
       return false;
   }


   return true;
}
```

- Time Complexity: O(M \* N)
- Space Complexity: O(M \* N)
