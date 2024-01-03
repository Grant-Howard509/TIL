# JS Timers (setTimeout / setInterval)

## setTimeout Method

The `setTimeout` method is used to execute a piece of code when a given amount of time has passed. The time is set in milliseconds, so the following example will display`"Hello World"` to the console two seconds after execution.

```
setTimeout(function () {
    console.log("Hello World");
}, 2000);

console.log("Displays First");
```

As mentioned before, this program executes, waits for two seconds, and then displays `"Hello World"` to the console. Before that is displayed, `"Displays First"` appears on the console before `"Hello World"`. What this means is that the `setTimeout` is an asychronous method because other methods, such as displaying `"Displays First"` to the console, do not have to wait until the 2 seconds have elapsed and `"Hello World"` is executed.

Lets look at the `setTimeout` method syntax

```
setTimeout(callback function, milliseconds, param1, param2...);
```

Here we can see that time out takes two important arguments. The first argument is a the callback function that is to be executed once the time has elasped. The second argument is the time that is to be elapsed before running the callback function. The parameters that follow the first two arguments are parameters that will be used inside of our callback function call.

Lets take a closer look on how the additional parameters work.

```
setTimeout(greetings, 2000, "John", 27);

function greetings(name, age) {
    console.log(`Hello my name is ${name}`);
    console.log(`I am ${age} years old`);
}

console.log("First");
```

In this example, the arguments, `"John"` and `27`, are used for `name` and `age` inside of our callback function. So, after two seconds the console will display `"Hello my name is John"` and `"I am 27 years old"` respectively.

Why do we have to pass arguments like this for `setTimeout`? Lets look at the same example, except we will define the arguments `John` and `27` inside the callback function.

```
setTimeout (greetings("John", 27), 2000);

function greetings(name, age) {
    console.log(`Hello my name is ${name}`);
    console.log(`I am ${age} years old`);
}

console.log("First");
```

If we were to execute this program, the `greetings` method would execute first because we are making a function call inside of `setTimeout` rather than passing a reference to a function.

Every `setTimeout` method call returns a `id` value. This `id` is used to cancel `setTimeout` whenever needed. We can do this by using the `clearTimeout` method. Here is an example.

```
const timeoutID = setTimeout (greetings, 2000);

function greetings(name, age) {
    console.log(`Hello my name is ${name}`);
    console.log(`I am ${age} years old`);
}

clearTimeout(timeoutID);

console.log("Timeout does not execute");
```

Because `clearTimeout` was called before the two seconds have elapsed, the `setTimeout` callback was never executed.

## setInterval Method

The `setInterval` method is very similar to `setTimeout` method with one key difference: `setTimeout` executes the code only once while `setInterval` executes the code multiple time given a delay. Other than this key difference, the syntax between the two are identical.

```
const intervalID = setInterval(function () {
    console.log("Hello There");
}, 3000);

setTimeout(function () {
    console.log("End");
    clearInterval(intervalID);
}, 9000);
```

Here we call `setInterval` to execute a hello world program every three seconds while saving the method calls id in `intervalID`. We also call a `setTimeout` method which cancels the `setInterval` execution by passing the `intervalID` into `clearInterval` after nine seconds have passed. This means `"Hello There"` will be displayed three times before being timed out.

## Resources

- [freeCodeCamp](https://www.freecodecamp.org/news/javascript-settimeout-how-to-set-a-timer-in-javascript-or-sleep-for-n-seconds/)
- [JavaScript.info](https://javascript.info/settimeout-setinterval)
