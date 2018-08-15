# An Intro to Reading Different Data Types #


Let's start with looking at functions and their inputs.

```javascript
var namesArray = ["CJ", "Daniel", "Evan", "Jack", "John", "John", "Johnny", "Mamma", "Michael", "Nikki", "Philip"];

var namesObject = {
    student0: "CJ", 
    student1: "Daniel",
    student2: "Evan",
    student3: "Jack",
    student4: "John",
    student5: "John",
    student6: "Johnny",
    student7: "Mamma",
    student8: "Michael",
    student9: "Nikki",
    student10: "Philip"
};

function giveIntroduction(name) {
    return "Hi, my name is " + name + ". I look forward to working with all of you folks."
}

// let's compare a few inputs into our function
giveIntroduction("CJ");              // returns "Hi, my name is CJ. I look forward to working with all of you folks."

giveIntroduction(namesArray[0]);            // returns the same thing
giveIntroduction(namesObject.student0);     // returns the same thing; object dot notation
giveIntroduction(namesObject["student0"]);  // returns the same thing; object bracket notation


// Why do these all give the same result? Because arrays,objects, and variables are just ways to store basic types like strings.

names[0] === "CJ";              // returns true
names.student0 === "CJ"         // true as well
names.student0 === names[0]     // true
```

Some more examples of how variables and functions evaluate to basic types:

```javascript
function multiply(x, y) {
    return x * y;
}

var product = multiply(4, 25);
product;        // returns 100

// you can also plug in the results of functions into parameters
var sameProduct = multiply(4, multiply(5, 5));
sameProduct;    // returns 100

// notice again how each function call gets evaluated before it gets
// put into the other function
// thus this ends up looking just like this: multiply(4, 25);
var letsDoMore = multiply(multiple(2, 2), multiply(5, 5));
letsDoMore;     // returns 100


// simplify this into a statement like "multiply(x, y)" with only 2 numbers in the parameter call
var whatDoesThisGiveMe = multiply(multiply(2, 3), multiply(7, multiply(multiply(5, 3), 10)));
whatDoesThisGiveMe;     // what does this return us?
```

Let's look at data types not playing well together, and then how we can fix them.
```javascript
function remainder(x, y) {
    return x % y;
} 

var myObject = {
    str: "3",
    num: 3
}

remainder(10, 3);               // returns 1
remainder(21, myObject.num);    // returns 0
remainder(34, myObject.str);    // Uh-oh; it returns NaN; which means not a number

// Why did that happen? Well what we did looks like this:
remainder(34, "3");     // This isn't right, how do you get a remainder of a number and string

// just to be clear: "3" does not equal to 3
"3" === 3;      // returns false

// How can we make this work though?
remainder(34, parseInt(myObject.str));      // returns 1; 
//parseInt converts strings of numbers into actual numbers; parseInt("3") + 3 === 6

```