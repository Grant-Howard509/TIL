# HTML Delegation

Event delegation is where events, such as a click event for example, are handled higher up on the DOM tree rather than where the event was first orginated from. We are able to handle events higher in the DOM hierarchy because of a concept known as a event bubbling.

Here is an example of event bubbling

```
<div>
    <span>
        <button>Click Me</button>
    </span>
</div>
```

Event bubbling is this idea that events are traversed upward in the DOM tree until we reach root HTML tag. So, in our example we have a `div` tag as our ancestor, `span` as a child of `div` but is a parent of `button`. Once a user triggers an event, such as clicking `button`, the event "bubbles" up the DOM tree where both `span` and `div` will recieve the triggered event.

Consider the following example:

```
<div>
    <span>
        <button>Click Me 1</button>
        <button>Click Me 2</button>
        <button>Click Me 3</button>
        <button>Click Me 4</button>
        <button>Click Me 5</button>
    </span>
</div>
```

This example is similar to the first, however, we have five buttons that could tigger a click event. In Event delegation, we delegate our event to the parent element. So, in our example above, ideally we would want to delegate our click event to the `div` element.

To do this, we use a query selector on `div`, and then find whether a button triggered the click event by calling the event object property `target` and its property 'tagName'.

```
const div = querySelector('div');

div.addEventListener('click', (event) =>  {
    if(event.target.tagName === 'BUTTON') {
        console.log('Button was click');
    }else {
        console.log('Not a button event');
    }
});
```

From here, we figure out what button was click either by `event.target.className` or any other identifier inside the `target` object.

## Resources used:

1. [freecodecamp](https://www.freecodecamp.org/news/event-delegation-javascript/)
2. [Javascript Info](https://javascript.info/event-delegation)
