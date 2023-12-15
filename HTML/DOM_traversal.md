# DOM Traversal

The Document Object Model (DOM) is a structured tree of nodes in which we as front-end developers can use to access these nodes to do any kind of operation. Built-in methods are also included with the DOM object `document` that allow users to select an element by ID, class, tag name, and query selectors.

We will learn how to walk through the DOM tree using Javascript starting from the root node to the leaf nodes.

## Root Node

The `document` object is the root node for every other node inside of the DOM. `document` is also a property of the `window` object representing the browser window with properties such as height and width. `document`, however, contains everything inside the inner window.

| Property                 | Node      | Node Type     |
| ------------------------ | --------- | ------------- |
| document                 | #document | DOCUMENT_NODE |
| document.documentElement | html      | ELEMENT_NODE  |
| document.head            | head      | ELEMENT_NODE  |
| document.body            | body      | ELEMENT_NODE  |

## Parent Nodes

What determines whether a node is a parent node, lets look at the following example:

```
  <html>
      <body>
          <h1> Heading tag </h1>




          <ul>
              <li> item 1 </li>
              <li> item 2 </li>
              <li> item 3 </li>
          </ul>
      </body>
  </html>
```

Given this tree above, we can safely say that our element node `html` is a parent of `body`. This is because `html` is closer to the `#document` which is our root node. Going a little further we can also say that `body` is a parent for both `h1` and `ul` for the same reason. `#document` is called a root node because it does not have any parent node.

If we don't know a nodes parent, we can use the following two properties

| Property      | gets           |
| ------------- | -------------- |
| parentNode    | Parent Node    |
| parentElement | Parent Element |

Once we find the parent node using either `parentNode` or `parentElement` properties, we can use the same properties again to find the grandparent element. We can do the following using our previous example above:

```
  const h1 = document.getElementsByTagName('h1')[0];




  console.log(h1.parentNode.parentNode); // Gets the grandparent or 'html'
```

## Children Nodes

Nodes that are a parent, their branches (or internal nodes) are called children, sometimes called descendants.

| Property          | gets                     |
| ----------------- | ------------------------ |
| childNodes        | Child Nodes              |
| firstChild        | First Child Node         |
| lastChild         | Last Child               |
| children          | Element Child Nodes      |
| firstElementChild | First Child Element Node |
| lastElementChild  | Last Child Element Node  |

Using the same HTML example above, when we inspect the `ul` element children using `childNodes, firstChild,` and `lastChild` we get the following:

```
ul.childNodes // (7) [text, li, text, li, text, li, text]
ul.firstChild // #text
ul.lastChild // #text
```

Why is `text` in the node list? This is because the indentation between elements is counted as text nodes in the DOM. To avoid this, it is better to use the `children, firstElementsChild,` and `lastElementChild` to avoid this feature in the DOM.

That being said, if an element in the DOM has both text and elements as children, the node properties prove to be useful.

For example:

```
HTML:
  <h1> This is a <strong>HUGE</strong> sale!</h1>




JS:
  const h1 = document.getElementsByTagName('h1')[0];




  for (let elements of h1.childNodes) {
      console.log(elements);
  }
```

Although `children` and `childNodes` are not arrays, they have array-like properties such as indices and a length property.

## Sibling Nodes

Siblings are nodes that are on the same tree level as other nodes. In our `ul` list, all `li` elements are siblings because they are all direct children of `ul`. Here are some properties we can use for traversing sibling nodes:

| Property               | gets                          |
| ---------------------- | ----------------------------- |
| previousSibling        | Previous Sibling Node         |
| nextSibling            | Next Sibling Node             |
| previousElementSibling | Previous Sibling Element Node |
| nextElementSibling     | Next Sibling Element Node     |

Just like `firstChild` and `lastChild`, `previousSibling` and `nextSibling` return all node values, including indentation or `text` nodes. Now let's say we want to access both siblings for this item 2 in our `ul`. We can display each sibling by doing the following:

```
   const ul = document.getElementsByTagName('ul')[0];


   const item2 = ul.children[1];


   console.log(item2.previousElementSibling); // returns 'item1'
   console.log(item2.nextElementSibling); // returns 'item3'
```

## Resources

1. [Digital Ocean Tutorial](https://www.digitalocean.com/community/tutorials/how-to-traverse-the-dom)
2. [My codepen.io](https://codepen.io/Havic412/pen/poGXaPq)
