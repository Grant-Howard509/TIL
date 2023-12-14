# The `this` keyword in JS

The `this` keyword most often is used when an object is looking to call a property inside itself.

Consider the following example:

```
   const dog = {
       tail: 'Wag'
   }
```

Here we have created an object called `dog` and within the object we have property `tail`that when called returns the value `Wag`. Now let's say that when a dog is happy the dog wags its tail, then we can do the following method within dog.

```
   const dog = {
       tail: 'Wag',


       happy() {
           console.log(dog.tail);
       }
   }
```

When we call the method `happy()` property inside the dog object, we get a message saying `"Wag"` displayed on the screen. But what if we had a cat object?

```
   const cat = {
       tail: 'Swag',


       happy() {
           console.log(cat.tail);
       }
   }
```

Here we have two objects, dog and cat, that have the same property, `tail`, but with different values. Both objects have a method `happy()` but the dog wags its tail while the cat sways its tail. We ask ourselves, how can we write the `happy()` method once but call the correct property inside both dog and cat? This is where the `this` keyword comes in. With the `this` keyword, we can do the following:

```
   const dog = {
       tail: 'Wag',
   }


   const cat = {
       tail: 'Swag',
   }


   function happyAnimal(){
       console.log(this.tail);
   }


   cat.happy = happyAnimal;
   dog.happy = happyAnimal;


   cat.happy(); // "Wag"
   dog.happy(); // "Sway"
```

Breaking this down we see we have our two objects, dog and cat, each with a property of tail same as before. We also have a function named `happyAnimal()` which displays the message `this.tail`. The `this` keyword references all the internal properties inside a given object, so if we were to call `happyAnimal()` as is we would have undefined displayed. That is why after we declare the function, we create a property called `happy` for dog and cat and assign `happyAnimal`s reference to the property. When we then call `dog.happy()`, the `this` keyword will have access to all of dogs properties, in this case `tail`.

What would happen if we did the following:

```
   console.log(this.tail);
```

This statement is valid inside of JS despite the keyword `this` not being inside of an object. However, the `this.tail` keyword would be undefined since property `tail` does not exist.

Now lets look at one more example to understand the relationship between methods and objects in regards to the keyword `this`.

```
function makeUser() {
 return {
   name: "John",
   ref: this
 };
}


let user = makeUser();


alert( user.ref.name ); // What's the result?
```

At first glance, one would assume that `user.ref.name` would return the value `John`. However, the actual result itself is an error. This is because `this` only looks for what is called at that moment, since the returned object inside of `makeUser()` is not called with a dot operator, the `this` keyword will reference the `makeUser()`. Because there is no reference to `makeUser().ref.name`, we receive an error. So, to make this work, we must make the property `ref` a method call inside of the returned object, and because the method is called inside of the returned object `this` will have access to the property `name`.

Solution:

```
function makeUser() {
 return {
   name: "John",
   ref() {
     return this;
   }
 };
}


let user = makeUser();


alert( user.ref().name ); // John
```

For a more detailed explanation, refer to the link below. Example is the first task in the `Tasks` section.

## Resources

[Javascript Info](https://javascript.info/object-methods)
