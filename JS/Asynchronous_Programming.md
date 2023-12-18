# Asynchronous Programming in JS

## What is Synchronous Programming?

A synchronous program is a set of instructions that executes one task at a time. To really show how this works, lets look at an example:

```
    console.log("Task 1");
    console.log("Task 2");
    console.log("Task 3");
```

This is a very basic program that demonstrates the idea of synchronous programming. Each task is executed line by line, just like a recipe for a dish is done in a particular order. Asynchronous programming, on the other hand, is where tasks do not wait on one another to execute, rather they execute simultaneously. This is particularly usefull if a certain task is known to be time costly.

`Blocking` is a term used when a task in a program halts all other operations causing the user to experience an unresponsive frozen screen. All other task stuck in waiting for a particular time costly task to complete before continuing.

## What is Asynchronous Programming?

Asynchronous programming is a way for a program to handle multiple tasks simultaneously. Here is an example from `freecodecamp` that demonstrates the use of asynchronous programming using `setTimeout`:

```
    console.log("Start of script");

    setTimeout(function() {
        console.log("First timeout completed");
    }, 2000);

    console.log("End of script");
```

In this example, the program begins by displaying "Start of script" to the console. The setTimeout function contains a function that displays to the console "First timeout completed" to indicate when the function is executed. There is also a delay of 2000 ms before the function is called. `setTimeout` function is asynchronous, because of this the last task, `console.log("End of script")`, is executed before the `setTimeout` function. The output is as follows:

```
    "Start of script"
    "End of script"
    "First timeout completed"
```

## How to Use a Callback Function

A callback function is when a function is passed as an argument for another function. The main function passing the callback executes first, while the callback is executed after the main function has finished. Here is another example from `freecodecamp` that demonstrates how callback functions can be used with asynchronous programs:

```
    // Declare function
    function fetchData(callback) {
        setTimeout(() => {
            const data = {name: "John", age: 30};
            callback(data);
        }, 3000);
    }

    // Execute function with a callback
    fetchData(function(data) {
        console.log(data);
    });

    console.log("Data is being fetched...");
```

In the code above, we delare a function called `fetechData`. This function has a callback function as its parameter. `setTimeout` represents a asynchrous function that is to be executed using the callback function. After 3 seconds, the callback function is executed within the `fetchData` function. However, if we look at the output we see that `console.log("Data is being fetched...");` is executed first while `fetchData` runs in the background. Therefore, our output looks like...

```
    "Data is being fetched..."
    {name: "John", age: 30}
```

## Callback Hell

Callback hell is when we have multiple callback functions that chained together. This can lead to a pyrimid structure called the "pyrimid of doom". Essentially, chaining callbacks together can make code hard to read, follow, and understand. Here is yet another example from `freecodecamp` demonstrating this concept:

```
    getData(function(a) {
        getMoreData(a, function(b) {
            getEvenMoreData(b, function(c) {
                getEvenEvenMoreData(c, function(d) {
                    getFinalData(d, function(finalData) {
                        console.log(finalData);
                    });
                });
            });
        });
    });
```

Avoid using callback functions for asynchronous programming, instead use promises.

## Promises

According to `freecodecamp`, a promise is a "A promise in JavaScript is a placeholder for a future value or action. By creating a promise, you are essentially telling the JavaScript engine to 'promise' to perform a specific action and notify you once it is completed or fails." Callback are used to handle the responses from promises. Callbacks are called when the promise is successful, or when the promises fails.

## Creating a Promise

Create an instance of a promise using the following syntax:

```
const promise = new Promise(function (resolve, reject) {} );
```

Lets break this down, first we have a constructor `Promise` that takes a function as its arugment. This function is called the `executor` and is immediately called upon instantiation. The `executor` takes two function arguments called `resolve` and `reject`. The `resolve` function is called if the operation is successful. The `reject` function is called if the operation fails.

A promise has 3 states:

- Pending: Initial state.
- Fulilled: Operation was successful.
- Rejected: Operation failed.

## How to Consume a Promise

Here are the steps to consume a promise:

1. Obtain a reference to the promise.
2. Attach callbacks to the promise: use the `.then` and `.catch` methods. `.finally` method can be used and will be called no matter what the promises status.
3. Wait for promise to be fulfilled or rejected.

## How to Chain Promises

We can chain promises with the `.then` method. The `.then` method takes a callback function as its argument and returns a new promise. The new promise is then resolved with the value returned by the callback function.

## How to Use Promise.all

The `Promise.all` method takes an array of promises as its array and returns a singluar promise based upon if the array of promises where fulfilled or rejected.

## How to Use the Fetch API with Promises

The `Fetch API` is a build-in JS feature for making network request to servers, such as fetching for server data. The following example provided by `freecodecamp` shows how a promise can make a network request for server data, extract the json data, and then display the json to the conosle.

```
    fetch('https://some-api.com/data')
        .then(response => response.json())
        .then(data => {
            console.log(data);
        })
        .catch(error => {
            console.error('Error:', error);
        });
```

## Async / Await Functions

Async and Await are used to write synchronous code in a more synchronous and readable way.

The `async` keyword is used to declare a function as asynchronous and the `await` keyword is used inside of the asynchronous function to pause execution of that function until a promise is resolved.

Here is an example from `freecodecamp`:

```
    async function getData() {
    const response = await fetch('https://jsonplaceholder.typicode.com/posts/1');
    const data = await response.json();
    console.log(data);
    }

    getData();
```

## Resources:

- [freecodecamp](https://www.freecodecamp.org/news/asynchronous-programming-in-javascript/)
