# Javascript in web apps

A web app is usually made of 3 things. A frontend, backend and a database.

The frontend is what a user sees, the backend is what handles all the logics under the hood and the database stores data.

The frontend receives data from the backend and renders it ("draws it") in the browser.

Javascript has a standard called ES (ECMAScript). Before 2015, Javascript looked like this:

```
var x = 5;
var y = 6;

function addNumbers (numA, numB) {
    return numA + numB;
}

var result = addNumbers(x, y);

console.log(result); // 11
```

As of 2015, ES6 came out (today, we're at ES10 or ES11, I can't remember for sure).

ES6 allows us to write Javascript code in a different format. It looks like this:

```
const x = 5; // or you could use 'let' instead of 'const'
const y = 6;

const addNumbers = (numA, numB) => {
    return numA + numB;
}

// or you could get rid of the 'return' word and the curly braces (these -> '{}')
// const addNumbers = (numA, numB) => numbA + numB;

const result = addNumbers(x, y);

console.log(result); // 11
```

Javascript also has the keyword 'this'. By default, 'this' will always refer to the window object.

Go to Chrome and open up the console tab in dev tools (you can get there quickly by clicking F12).

Then, type this in:

```
console.log(this);
```

The 'window' object will print in your console.

Now type this in and hit enter:

```
console.log(this.location.href);
```

Or maybe you just want the pathname:

```
console.log(this.location.pathname);
```

Note, that the window object is a global object. Which means if you do this and click enter:

```
someVariable = 'lol get rekt'
```

Then you can do this:

```
console.log(this.someVariable)
```

Because 'window' is global, you can replace 'this' with 'window'. So like:

```
console.log(window.location.href);
```

Like I said, 'this' refers to 'window' only by default, because 'this' refers to the object that it is wrapped in.

For example, if I do this:

```
const myObjectWithALongAndCoolName = {
  myValue: 42,
  myFunction: function() {
    return this.myValue;
  },
};

console.log(myObjectWithALongAndCoolName.myFunction()); // prints 42, because the 'this' in 'myFunction' refers to 'myObjectWithALongAndCoolName'.
```

With arrow functions however ('=>'), the word 'this' is obsolete, meaning if you were to do something like,

```
const getThis = () => {
    return this;
}

// or just,
// const getThis = () => this;
```

Then, it would just print the global window object. There is no 'this' with ES6+;

---

OOP (object oriented programming) is a type of programming 'paradigm'. There are several, but this one is most popular.

There are 3 principles to OOP -- inheritance, encapsulation and polymorphism. But, because everything in Javascript is PROTOTYPE based, it's not ACTUALLY and object oriented language.

HOWEVER, ES6+ allows us to write Javascript i an OOP format (object oriented programming):

```
// Here we have a general "car" class
class Car {
    // A constructor is a function that every class has.
    constructor(brand) {
        // In the constructor, you do some initial actions.
        // In this case, we are giving this "Car" object a brand name
        this.carname = brand;
    }
    present() {
        return 'I have a ' + this.carname; // This would return 'I have a Ford' -- (explained below)
    }
}

// Notice, how we are creating a new class that extends (or "branches off") the class "Car".
// What this means, is that this class (Model) is also a Car model.
class Model extends Car {
    // Again, every class has a constructor
    constructor(brand, mod) {
        // Every class that "extends" a different class will have a function called "super".
        // What "super" does is call the "constructor" function of its parent class.
        // So in this case, the function "super" is calling the constructor of Car.
        // If you recall, the constructor of Car gives the object a brand name.
        super(brand);
        this.model = mod;
    }
    show() {
        return this.present() + ', it is a ' + this.model; // This would return 'I have a Ford, it is a Mustang' -- (explained below)
    }
}
```

Now that we've defined our classes, we can do this:

```
const myCar = new Model("Ford", "Mustang");
```

So, we are creating a variable called 'myCar' (we could have used `var myCar`, but that would be using the old Javascript).

Then, we said that this new variable is an 'instance' of the Model class and then we passed in two parameters, ('Ford' and 'Mustang').

At this point, if we were to do this:

```
console.log(myCar.show());
```

Then, we will see 'I have a Ford, it is a Mustang'. Why? Because if you notice, we said `myCar` is an instance of "Model". And because "Model" extends the class "Car", it has access to the Car's method "present" (method is another word for function). If you scroll up, you'll see that in Car, the function "present" returns 'I have a Ford'. The function "show" of the class "Model" adds onto that and says, "it is a Mustang".

Answer the following questions:

1. Can I do this? Why or why not.

```
myCar.present();
```

2. What is the '+' doing here?

```
. . .
    present() {
        return 'I have a ' + this.carname;
    }
. . .
```

3. Evaluate this expression:

```
. . .
    show() {
        return this.present() + ', it is a ' + this.model;
//             ^^^^^^^^^^^^^^                  ^^^^^^^^^^
//             What is this equal to?          How about this?
    }
. . .
```

4. Similar to the Car and Model idea, finish the below:

```
class Animal {
    constructor(animalType, animalColor) {
        this.animal = animalType;
        this.color = animalColor;
    }

    sayAnimal() {
        // TODO
    }
}

class AirbornAnimal extends Animal {
    constructor(animalType, animalColor) {
        // TODO
    }

    sayAirbornAnimal() {
        // TODO
    }
}

class LandAnimal extends Animal {
    constructor() {
        // TODO
    }

    sayLandAnimal() {
        // TODO
    }
}

const myAirbornAnimal = new AirbornAnimal('Bee', 'yellow');
console.log(myAirbornAnimal.sayAirbornAnimal());
// expected output: "I am a yellow Bee and I can fly!"

const myLandAnimal = new LandAnimal('Bear', 'brown');
console.log(myLandAnimal.sayLandAnimal());
// expected output: "I am a brown Bear and I'm too fat to fly!"
```
