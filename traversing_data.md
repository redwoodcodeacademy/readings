# Traversing Data #

Let's take a look at traversing a mixture of data types that store data (objects, arrays, variables)

```javascript

var haystack = {
    anotherHaystack: [null, null, "needle"]
}

// How can I get the "needle"?
var oneLevelDeep = haystack.anotherHaystack;
oneLevelDeep;       // gives me the array [null, null, "needle"]

// Let's store the "needle" in a needle variable
var needleIFound = oneLevelDeep[2];
needleIFound;       // returns "needle"

// Let's see how we could have accessed this in one line
var needle = haystack.anotherHaystack[2];
// haystack.anotherHaystack is equivalent to [null, null, "needle"]

/* 
    This works because "haystack" is an object which lets us access "anotherHaystack".
    "anotherHaystack" is an array so I can access it by bracket notation with my desired
    index.
*/

```

Let's take a look at accessing variables.

```javascript

var son = "Bart";
var daughter = "Lisa";

var myChildren = [son, daughter];

// What does "myChildren" look like?

// To be clear, "myChildren" looks like this:
// ["Bart", "Lisa"]

myChildren[0] === "Bart";       // true
myChildren[1] === "Lisa";       // true

```

That was pretty simple. Let's take a look at variables in an object.

```javascript

var son = "Bart";
var daughter = "Lisa";

var homer = {
    son: son,
    daughter: daughter
}

// What does homer.son give me?
// it looks up in the global scope the variable son ("Bart") and then returns it by the keyword "son"
homer.son;          // returns "Bart"
homer["daughter"]   // returns "Lisa"

```

Let's traverse a more awkward nesting now.

```javascript

var son = "Bart";
var daughter = "Lisa";

var family = {
    son: son,
    daughter: daughter
}

var homer = {
    name: "homer",
    family: family
}

// How can I get the names of "homer"'s kids through the "homer" object

homer.family.son;       // returns "Bart"
homer.family.daughter;  // returns "Lisa"

```

Key Takeaways:
- Follow the thread. If something is in a variable, access it. See what the "address" is of the data you want.
- The "address" of your data is the variable name or data structure (objects & arrays) that stores it.