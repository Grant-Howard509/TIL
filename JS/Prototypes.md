# Prototypes in JS

## What is a Prototype?

For every Javascript function, there is a prototype property that references another object. We as programmers can use prototypes to call properties which may contains primitives, strings, and other functions.

Here is an example of a function, `Dragon`, which acts as a constructor to create a `Dragon` object. This object will contain the name of the dragon, and its color. We can then use `Object.create`, which references another object when looking up a property fails, to place our contructors protytpe as a fallback. Inside our prototype object, lets create a function for our dragon to breath fire like so.

```
// Constructor

const Dragon(name, color) {
    let dragon = Object.create(Dragon.prototype);
    dragon.name = name;
    dragon.color = color;

    return dragon;
};

Dragon.breathFire = function (name) {
    console.log('${this.name} is breathing fire!!!');
};

const smog = Dragon('Smog', 'red'); // Using contructor "Dragon"

smog.breathFire(); // Will return function from Dragon prototype object.
```

As we can see above, when we call `smog.breathFire()` the method property `breathFire()` is not in our object `smog`, thus we look for that property in`Dragon.prototype`. Since our constructors prototype does in fact have the property we are looking for, it returns the message `'Smog is breathing fire'`.

Lets simplify this even more by using the `new` keyword. In Javascript, whenever we invoke the `new` keyword in object creation, our constructors`object.create(Dragon.prototype)`and `return dragon` happen implicity. Here is an example that does the same behavior as above but with `new`.

```
// Constructor

const Dragon(name, color) {
    // let this = Object.create(Dragon.prototype);

    this.name = name;
    this.color = color;

    // return this;
};

Dragon.breathFire = function (name) {
    console.log('${this.name} is breathing fire!!!');
};

const smog = new Dragon('Smog', 'red'); // Using contructor "Dragon"

smog.breathFire(); // Will return function from Dragon prototype object.
```

The comments inside of the constructor `Dragon` are what the `new` keyword does for us automatically. Note that when instantiating a dragon, we must use the `new` keyword again when calling the constructor. Using the `new` keyword when calling the constructor is the reason why `this` is created in `Dragon`.

This method of creating an object is called the `pseudoclassical pattern`. As of right now, we have been using a javascript function as a constructor, but we can also uses the ES6 `class` keyword which is essentially just a more readable syntaxical sugar of the functional pseudoclassical method above.

```
class Dragon {
    constructor(name, color) {
        this.name = name;
        this.color = color;
    }

    breathFire() {
        console.log('${this.name} is breathing fire!!!');
    }
}
```

As you can see, the code above is much more readable and clean in comparision.

## Array Methods

When declaring an array, most of the time we assign a variable with `[]` which is just again syntax sugar for `new Array()`. The array class also has a prototype object which is where all of our methods such as `slice`, `pop`, and `push` come from. This is because we use the new keyword which sets up that delegation to `Array.prototype` on failed lookups.

## Static Methods

Sometimes, we would prefer to have our classes to have a method that is not shared between all of its instances thus not in prototype object. Lets say only some dragons can use magic if that dragon is the color red, so we create a method that takes an array of dragons and only displays the dragons that are red. We can do so using the following method.

```
class Dragon {
    constructor(name, color) {
        this.name = name;
        this.color = color;
    }

    breathFire() {
        console.log('${this.name} is breathing fire!!!');
    }
}

function magic(dragons) {
	dragons.map((dragon) => {
  	if(dragon.color == 'red') console.log(dragon.name + ' is using magic!');
  });
}

const smog = new Dragon('Smog', 'red');
const blackFire = new Dragon('Black Fire', 'blue');

magic([smog, blackFire]);
```

This method works because the function is not in the scope of the class itself, however, we can place this function in the scope if we use the `static` keyword like so.

```
class Dragon {
    constructor(name, color) {
        this.name = name;
        this.color = color;
    }

    breathFire() {
        console.log('${this.name} is breathing fire!!!');
    }

    static magic(dragons) {
	    dragons.map((dragon) => {
  	        if(dragon.color == 'red') console.log(dragon.name + ' is using magic!');
        });
    }
}

const smog = new Dragon('Smog', 'red');
const blackFire = new Dragon('Black Fire', 'blue');

Dragon.magic([smog, blackFire]);
```

Notic how we call the method `magic` with the class itself rather than an instance.

## Object.getPrototypeOf Method

The `Object.getPrototypeOf` returns the prototype of an object.

```
class Dragon {
    constructor(name, color) {
        this.name = name;
        this.color = color;
    }

    breathFire() {
        console.log('${this.name} is breathing fire!!!');
    }
}

const smog = new Dragon('Smog', 'red');

const prototype = Object.getPrototypeOf(smog);
```

If we were to log `smog` in the console we would see a constructor method and a `breathFire` method. The constructor indicates that every instance has a constructor in their prototype that points to the orginal class itself. If we were to log `smog.constructor`, we would see the class `Dragon`. What `smog.constructor` doesn't actually exist in `smog`, so it looks it up in `Dragon.prototype` where a constructor is indeed present and returns the properties value.

`__proto__` has also been used in the past to get instances prototypes but now we use `Object.getPrototypeOf`.

## Determining If Property is in Prototype

If we loop through out `smog` instance using a `for in` loop, we will get the following result

```
Key: name, Value: 'Smog'
Key: color, Value: 'red'
Key: breathFire, Value: function () {
        console.log('${this.name} is breathing fire!!!');
    }
```

The reason why the method `breathFire` is displayed dispite not being a property of `smog` is because `for in` enumerates over all properties in the object as well as its prototype. To avoid enumerating over prototype properties, we can use the `hasOwnProperty` to determine whether or not the property is an object property or a prototype property.

`hasOwnProperty` will return a boolean, true meaning the property is owned by the object and false if the property is owned by the prototype. Here is an example:

```
Code:

for(let key in smog) {
    if(smog.hasOwnProperty(key)) {
        console.log(`Key: ${key}. Value: ${leo[key]}`);
    }
}

Output:

Key: name, Value: 'Smog'
Key: color, Value: 'red'
```

## Checking if an Object is an Instance of a Class

We can use the `instanceof` operator to determine if an object is an instance of a class. If the object is an instance of a class, it will return a boolean value `true` else it will return `false`.

```
object instanceof Class
```

How does `instanceof` really work? It works by checking for the existance of a `constructor.prototype` in the objects prototype chain. Rememeber that all instance have a constructor with their protototype that links to the class itself. Therefore the following two lines of code are the same.

```
// Instanceof operator
smog instanceof Dragon;

// Prototype version
Object.getPrototypeOf(smog) === Dragon.prototype;
```

## Arrow Functions

Arrow functions have their own `this` keyword and therefore cannot be constructor functions invoked with the `new` keyword. Doing so will produce an error.

Also, note that arrow function also do not have any prototype property.
