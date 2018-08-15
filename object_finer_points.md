# Objects and Classes in JavaScript : A More Detailed Look

<!-- objects can store functions -->

**Note**: I will be using the words *method* and *function* interchangeably throughout this guide.

### Plain Objects ###

Let's take a look at how to add functions in basic objects.

You can either declare them when you first declare your object, or you can declare them afterwards.

```javascript
// declaring function in object declaration
var karim = {
    identifies: ["male", "new yorker"],
    talk: function () {
        console.log("You call this New York pizza!?");
    }
}
/* 
    example:
    > karim.talk();
    <- You call this New York pizza!? 
*/

// adding a function to an object after it was declared
var anotherKarimExample = {
    name: "Karim",
    workplace: "Redwood Code Academy"
}

// now let's add a function for our object to say his name and workplace
anotherKarimExample.greeting = function () {
    console.log("Hi, my name is " + this.name + ", and I work at " + this.workplace + ".");
}

// you can also declare this as:
// anotherKarimExample["greeting"] = function () { ... }

/* 
    example:
    > anotherKarimExample.greeting();
    <- Hi, my name is Karim, and I work at Redwood Code Academy.

    You can also call it by bracket notation:
    > anotherKarimExample["greeting"]();
    <- Hi, my name is Karim, and I work at Redwood Code Academy. 
*/

```

### Classes ###

Let's take a quick detour to how to create classes in JavaScript.
We're going to go over the older ES5 style and the newer ES6 style.

```javascript
// ES5 Classes

function Person(name, age) {
    this.name = name;
    this.age = age;
}

var Karim = new Person("Karim", 39);
Karim.name;     // returns "Karim"
Karim["age"];      // returns 39


// ES6 Classes
class Person {
    constructor(weight, height) {
        // weight = lbs; height = inches
        this.weight = weight;
        this.height = height;
    }
}

var randomPerson = new Person(180, 72);
randomPerson["weight"];     // returns 180
randomPerson.height;        // 72
```

### Class Methods ###

Now let's look at how to add methods to our objects created from Classes.

I'll be showing the ES5 method and ES6 method.

```javascript
// ES5 Class
function Person(weight, height) {
    this.weight = weight;
    this.height = height;
}

// Add method to class at declaration
function Person(weight, height) {
    this.weight = weight;
    this.height = height;
    this.getBMI = function () {
        return ((this.weight / this.height) / this.height) * 703;
    }
}

// add method after declaring constructor
Person.prototype.getBMI = function () {
    return ((this.weight / this.height) / this.height) * 703;
}

// example
var child = new Person(37, 40);
child.getBMI();         // returns 16.256875

// ES6 Class
// Add method to class at declaration
class Person {
    constructor(weight, height) {
        // weight = lbs; height = inches
        this.weight = weight;
        this.height = height;
    }

    // note you do not need the "function" keyword in ES6 when declaring
    // a function in a class
    getBMI() {
        return ((this.weight / this.height) / this.height) * 703;
    }
}

// From here on is identical to ES5
var adult = new Person(180, 72);
adult.getBMI();         // returns 24.409722222222225


// If you want to declare a class method after writing your constructor,
// it's the same as ES5
Person.prototype.tellMeYourWeight = function () {
    return "My Weight is " + this.weight + " lb.";
}

adult.tellMeYourWeight();       // returns "My Weight is 180 lb."

```
### What should I do? ###

**Why would you want to add methods at class construction or after the fact?**

- The design choice is up to you. Ideally, you should declare all your functions in
the class constructor since it makes it clear to readers what your objects can do.

- However, you might find yourself coding quickly and want to add in a feature on the fly,
rather than modify your constructor.

**Should I use ES5 or ES5?**

- At least, you should use whatever feels comfortable and intuitive to you.
- Eventually, you'll want to use ES6 as your main syntax style since it is becoming (or is) the
the industry standard. 


There you have it! Now you should have all the tools to build objects with functions any way that you would like. 
