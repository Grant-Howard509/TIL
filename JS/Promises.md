# Promises in JS

## Syntax

Before we go in further on the details of promises we must understand the structure of a promise. Below you will find the syntax used to declare and assign a promise.

```
let promise = new Promise(function(resolve, reject) {
   // Executor
});
```

Let us break this down. We are first declaring a variable `promise` and assigning it to an initialized promise object. In the constructor, we can see a callback function that has two parameters resolve and reject. These parameters are actually callbacks themselves have received a value if an operation is a success or fails, for example the syntax may look like: `resolve("Success!")` or `reject("Error!")`.

We will also note that a promise has two properties, `state` and `result`. When initialized, the promise sets these properties such that the `state` property has value of `"pending"`, and `result` has a value of `undefined`.

Inside of initial callback function inside our constructor, the body of the function is called the `executor` because it executes immediately after instantiation. Whether the execution was successful or rejected determines the `state` and `result`s values.

For example, `resolve("Success!")` will have:

```
state: "fulfilled"
result: "Success!"
```

and `reject("Error!")` will have:

```
state: "rejected"
result: "Error!"
```

The executor performs a job and calls the predefined `resolve` and `reject` (JS engine defines them) callbacks. A promise that has completed a job and has either been called resolve or reject is called a `settled` promise (initially it's a `pending` promise).

Note: it is best practice to initialize an `Error` object and pass it through `reject`.

## .then and .catch

The `state` and `result` properties are internal to the promise object, but we can gain access to both using `.then` and `.catch` methods.

Lets look at the `.then` syntax and then break it down further.

```
promise.then(
   function(result) { // Handle fulfilled promise },
   function(error) { // Handle rejected promise }
);
```

The first callback argument handles a fulfilled promise, while the other handles the rejected promise.

If we only care about fulfilled promises, we can shorten this method to one argument.

```
let promise = new Promise(resolve("Success!"));


promise.then((result) => console.log(result)); // Prints "Success!"
```

If we are only interested in rejected promises, we can do so in two ways: one way is setting the first argument of `.then` to null, and another is just using a singular `.catch` method.

Here are both methods in action, both do identical operations.

```
let promise = new Promise((resolve ,reject) => reject(new Error("REJECTED!")));


// .then method


promise.then(null, (error) => console.log(error.message)); // Prints "REJECTED!"


// .catch method


promise.catch((error) => console.log(error.message)); // Prints "REJECTED!"
```

You can see here that `.catch` is really just the shorthand version of the `.then` rejected only method we provided above.

## .finally

The final method runs no matter what. It receives no arguments from the previous `.then` and `.catch` methods and does not return anything. `.finally` is often used as a cleanup function after all other `.then` methods are completed. However, `.finally` can be implemented anywhere and will execute in its given position.

Here is an example:

```
let promise = new Promise((resolve) => resolve("fulfilled!"));


promise.then((result) => console.log(result);)
      .finally(() => console.log("Promise end."));
```

In the example above, we will see that the console will get

```
fulfilled!
Promise ends.
```

However, if we flip `.then` and `.finally` the result would look like

```
let promise = new Promise((resolve) => resolve("fulfilled!"));


promise.finally(() => console.log("Promise start."));
      .then((result) => console.log(result);)


OUTPUT:


Promise start.
fulfilled!
```
