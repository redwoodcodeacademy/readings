# Arrays and Loops #

## What's the history of the array? Why do we need it? ##

Long, long time ago, there were no ways of storing a lot of information at once.
In fact, some programmers would resort to clever naming tricks. They would declare
unique variable names until they reached their byte limits of the characters.

Here's an example of what that would have looked like:
```javascript
// life before the array
var a = 1;
var b = 3;
var c = 2;
var d = 5;
var e = 6;
var f = 3;
var g = 1;
// ...
var aa = 3;
var ab = 3;
var ac = 3;
var ad = 3;
//..
var zz = 3;
```

This seems awfully redundant, slow to type, and a waste of variable namespace. 
Ideally, we want all of our variables to have meaningful use and names rather 
than simply to store a bunch of data. Thus, the array was created.

```javascript
// life with the array
var myArray = [1, 2, 3, 4, 5, 6, 7, 8, 9];
```

Now we can do a lot of useful things with our array, such as sorting them, using their
length, and performing operations on them.

```javascript
// A class of students
var students = ["lisa", "bart", "ralph", "nelson"];

// How many students do I have?
var numberOfStudents = students.length;         // 4

// How can I sort my students alphabetically?
students.sort();
students;                                       // students is now ["bart", "lisa", "nelson", "ralph"]

// Who is first on my role call?
students[0];                                    // "bart"
```


## Loops - Specifically the for-loop ##

There were other loops before the for-loop (do-while and while loop), but the 
for-loop is perhaps the most common and built specifically for going through an 
array.

What was life before the for-loop like?

```javascript
var superheroes = ["superman", "batman", "wolverine", "flash", "spiderman", "iron man"];

// I want to display all of my superheroes
console.log(superheroes[0]);
console.log(superheroes[1]);
console.log(superheroes[2]);
console.log(superheroes[3]);
console.log(superheroes[4]);
console.log(superheroes[5]);                // this seems pretty redundant...


// let's try a while loop
var i = 0;
while (i < superheroes.length) {
    console.log(superheroes[i]);
    i++;
}                                           // not bad, but i'm not a fan of declaring i and then incrementing it at the bottom of my block
```

Now let's see what the for-loop does for our problem of logging all of our superheroes.

```javascript
var superheroes = ["superman", "batman", "wolverine", "flash", "spiderman", "iron man"];

for (var i = 0; i < superheroes.length; i++) {          // all declaration and incrementing goes in one line now
    console.log(superheroes);
}
```

## So what's the big deal? ##
You might be thinking this especially if the while-loop seems to solve our problem already.

However, that variable declaration of "i" outside of our loop block, along with the incrementing line 
can make our intentions less clear by crowding our code.

Instead, with the for-loop, the only thing that goes into our loop block is the logic that we want to
implement. No more having to manage "i" in our loop block. Nice, clean, and concise.