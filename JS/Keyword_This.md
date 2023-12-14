# The `this` keyword in JS

The `this` keyword most often is used when an object is looking to call a property inside itself.

Consider the following example:

```
    const dog = {
        tail: 'Wag',
        nose: 'Sniff',
        mouth: 'Bark'
    }
```

Here we have created an object call `dog` and within the object we have properties `tail, nose, and mouth` that when called to some sort of action. Now lets say that when a dog is happy the dog wags its tail, then we can do the following method within dog.

```
    const dog = {
        tail: 'Wag',
        nose: 'Sniff',
        mouth: 'Bark'

        happy() {
            console.log(dog.mouth);
        }
    }
```

When we call the method `happy()` property inside the dog object, we get a message saying `"Wag"` displayed to the screen. But what if we had a cat object?

```
    const cat = {
        tail: 'Swag',
        nose: 'Sniff',
        mouth: 'Meow'

        happy() {
            console.log(cat.mouth);
        }
    }
```

Here we have two objects, dog and cat, that have the same properties but varying values. Each have a method `happy()` but the dog object barks and the cat object meows. We ask ourselves, how can we write the `happy()` method once but call the correct property inside both dog and cat? This is where the `this` keyword comes in. With the `this` keyword, we can do the following:

```
    const dog = {
        tail: 'Wag',
        nose: 'Sniff',
        mouth: 'Bark'
    }

    const cat = {
        tail: 'Swag',
        nose: 'Sniff',
        mouth: 'Meow'
    }

    function happyAnimal(){
        console.log(this.mouth);
    }

    cat.happy = happyAnimal;
    dog.happy = happyAnimal;

    cat.happy(); // "Meow"
    dog.happy(); // "Bark"
```

Lets break this down, both dog and cat objects are first created with the same properties as eachother but varying values. The function `happyAnimal()` is created and calls the keyword `this.mouth`. Both cat and dog are referenced to the SAME FUNCTION `happyAnimal` and are assigned to each the property `happy`. When the cat object calls `cat.happy()`, the `this` keyword calls the object itself, in this case cat, and its property `mouth`. Same thing happens inside the dog object.

What would happen if we did the following:

```
    console.log(this.tail);
```

This statement is valid inside of JS despite the keyword `this` not being inside of an object. However, the `this.tail` keyword would be undefined since property `tail` does not exist.
