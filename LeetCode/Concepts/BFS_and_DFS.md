# Breath First Search and Depth First Search

Both BFS and DFS are used to tranverse tress and graphs in a particular order. BFS focuses on the level order while DFS focuses on depth-first order. We will explain each in more deatail.

## BFS

Breath First Search as mentioned before focuses on visting each node at a given depth before moving on. For a tree data structure, this could mean starting at the root, then the children, then finally grandchildren in that order. Queues are used in the BFS algorithm to keep track of all the nodes that need to be visted next.

Let take a look at an example using an adjacent graph:

```
const graph = {
    A: ['B', 'C'],
    B: ['A', 'C', 'D'],
    C: ['B']
};
```

BFS Algorithm:

```
function bfs(graph, start) {
  const queue = [start];
  const visited = new Set();
  const result = [];

  while (queue.length) {
    const vertex = queue.shift();

    if (!visited.has(vertex)) {
      visited.add(vertex);
      result.push(vertex);

      for (const neighbor of graph[vertex]) {
        queue.push(neighbor);
      }
    }
  }

  return result;
}

bfs(graph, 'A'); // [A, B, C, D]
```

## DFS

Depth First Seach is quite similar to the BFS with the exception that DFS uses a stack instead of a queue. This allows for transversal in depth rather than level. For example, imagine a tree where we start at the root node, instead of transversing through all the roots children (level) we explore all the options of one child, their grandchild etc. After we have traversed a child node in depth is where we then go to its neighbors. This is in effect because the stack is a FIFO (fist in first out) data struture.

Lets take a look at an example:

```
function dfs(graph, start) {
  const stack = [start];
  const visited = new Set();
  const result = [];

  while (stack.length) {
    const vertex = stack.pop();

    if (!visited.has(vertex)) {
      visited.add(vertex);
      result.push(vertex);

      for (const neighbor of graph[vertex]) {
        stack.push(neighbor);
      }
    }
  }

  return result;
}

dfs(graph, 'A') // [A, B, C, D]
```

## BFS and DFS with Trees

BFS and DFS are very similar to graph but instead of checking the neighbor of each node and adding that neighbor to either a queue or stack, we check to see if the node has a left or right child. If the node has children, those children get added to the queue or stack to later be evaluated.

Here is an example of a BFS with a tree data structure:

```
Tree:
        1
       / \
      2   3
     / \
    4   5

function bfs(node) {
  if (!node) {
    return [];
  }

  const queue = [node];
  const result = [];

  while (queue.length) {
    const current = queue.shift();
    result.push(current.value);

    if (current.left) {
      queue.push(current.left);
    }

    if (current.right) {
      queue.push(current.right);
    }
  }

  return result;
}

bfs(tree); // [1, 2, 3, 4, 5]
```

Here is the DFS implementation using the same tree structure:

```
function dfs(node) {
  if (!node) {
    return [];
  }

  const stack = [node];
  const result = [];

  while (stack.length > 0) {
    const current = stack.pop();
    result.push(current.value);

    if (current.right) {
      stack.push(current.right);
    }

    if (current.left) {
      stack.push(current.left);
    }
  }

  return result;
}

dfs(tree); // [1, 2, 4, 5]
```

## Resources

- [hackernoon](https://hackernoon.com/a-beginners-guide-to-bfs-and-dfs-in-javascript)
- [youtube](https://www.youtube.com/watch?v=Urx87-NMm6c&t=166s&ab_channel=MichaelSambol)
