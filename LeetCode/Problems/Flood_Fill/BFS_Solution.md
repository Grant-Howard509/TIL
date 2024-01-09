# BFS Solution

### Concept: Breath First Search

## Steps:

1. Create a queue that stores the inital indice values as an array.
2. Change the inital position color to the new color value.
3. Create a while loop where the condition states that the queue cannot be empty.
4. Dequeue the queue and store its contents into the variable `current`.
5. Get both x and y indicies from `current`.
6. Check the edge cases for the 4-directional (up, down, left, right) posititions relative the the `current` position.
7. If the edge cases are false, push the new position to the queue and change the new position color to the new color.
8. Once the queue is empty, return the image.

## Code:

```
const flood = function(image, color, sr, sc, newColor) {

    let queue = [[sr, sc]];

    image[sr][sc] = newColor;

    while(queue.length > 0) {
        let current = queue.shift();

        let posX = current[0];
        let posY = current[1];

        if(isValid(image, color, posX + 1, posY)) {
            queue.push([posX + 1, posY]);
            image[posX + 1][posY] = newColor;
        }

        if(isValid(image, color, posX - 1, posY)) {
            queue.push([posX - 1, posY]);
            image[posX - 1][posY] = newColor;
        }

        if(isValid(image, color, posX, posY + 1)) {
            queue.push([posX, posY + 1]);
            image[posX][posY + 1] = newColor;
        }

        if(isValid(image, color, posX, posY - 1)) {
            queue.push([posX, posY - 1]);
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
