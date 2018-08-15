# A Short Guide to Cleaning Code #

Here's a code block we will be working on today:

```javascript
var attendanceRecord = ["here", "absent", "absent", "here", "here", "here", "here", "late"];

// this function will take in our variable attendanceRecord
function roleCall(record) {
    var daysHere = 0;
    var daysAbsent = 0;

    for (var i = 0; i < record.length; i++) {
        if (record[i] === "here") {
            daysHere++;
        } else if (record[i] === "absent") {
            daysAbsent++;
        } else if (record[i] === "late") {
            daysAbsent++;
        }
    }

    // returns an array where the first index is the amount of days here 
    // and the second index is the days absent
    return [daysHere, daysAbsent];
}
```

Now what is wrong with this function. It works alright, but it is very ambiguous what it does.

"roleCall" seems to be pretty unclear on offering us any help to figure out what the function
should do. Also note how we are organizing our return value, it's an array with some sort of 
symbolic representation. That is the first index represents the days at school and the second represents
days not at school. However, it's not super clear to us and perhaps others who have never seen our
code what it is supposed to do. 

Let's try a few ways of cleaning up this code block.

### Method 1 : Offer more context ###

Let's rename our function into something more meaningful.

```javascript
var attendanceRecord = ["here", "absent", "absent", "here", "here", "here", "here", "late"];

// even this name might not be perfect; are we gettting all sorts of details?
// this may or may not require further refinement depending on how we use this function
function getAttendanceDetails(record) {
    var daysHere = 0;
    var daysAbsent = 0;

    for (var i = 0; i < record.length; i++) {
        if (record[i] === "here") {
            daysHere++;
        } else if (record[i] === "absent" || record[i] === "late") {    
            // notice how we can remove an extra conditional block because
            // they did the same thing
            daysAbsent++;
        }
    }

    return [daysHere, daysAbsent];
}
```

Let's keep going and see how we can add a few more changes.

```javascript
var attendanceRecord = ["here", "absent", "absent", "here", "here", "here", "here", "late"];

function getAttendanceDetails(record) {
    var daysHere = 0;
    var daysAbsentOrLate = 0;       // note that I clarify in my variable naming that it can 
                                    // represent both being absent and being late

    for (var i = 0; i < record.length; i++) {
        if (record[i] === "here") {
            daysHere++;
        } else {
            // notice how in this case we are basically doing a binary calculation
            // either you are here or you are not; thus you can simplify it to an 
            // if-else case.
            daysAbsentOrLate++;
        }
    }

    // here i am returning an object to hold my information
    // I am using the keys to provide more context to myself or 
    // anyone else who is reading my code that these numbers represent
    // days here and days absent or late.
    return {
        daysHere: daysHere, 
        daysAbsentOrLate: daysAbsentOrLate
    };
}
```

That was a pretty good clean up of our code. It gave more context to ourselves and anyone who
might be working on our code. 

In the case of the if-else vs the if-else-if block, this is a choice up to you. Having multiple
exposed conditionals like multiple if statements or if-else-if statements can be clearer to the
reader than just an if-else. However, this is dependant on a lot of choice you make, 
one very important choice being how you named your variables.

## Method 2 : Break it up! ##

Many times you can speed along your coding process and reduce potential for bugs by simply
breaking up your functions into smaller, simpler functions.

To remind you what we are working with, here is our original cluttered code:

```javascript
var attendanceRecord = ["here", "absent", "absent", "here", "here", "here", "here", "late"];

function roleCall(record) {
    var daysHere = 0;
    var daysAbsent = 0;

    for (var i = 0; i < record.length; i++) {
        if (record[i] === "here") {
            daysHere++;
        } else if (record[i] === "absent") {
            daysAbsent++;
        } else if (record[i] === "late") {
            daysAbsent++;
        }
    }

    // returns an array where the first index is the amount of days here 
    // and the second index is the days absent
    return [daysHere, daysAbsent];
}
```

Note how this function is really doing two things, giving you a number for days here and a number
for days absent/late. What if we separated those things?

```javascript
var attendanceRecord = ["here", "absent", "absent", "here", "here", "here", "here", "late"];

function getDaysHere(record) {
    var daysHere = 0;
    for (var i = 0; i < record.length; i++) {
        if (record[i] === "here") {
            daysHere++;
        } 
    }
    return daysHere;
}
```

Look how simple this function is. I think you can see how doing this made naming your function
easier as well. 

Here's what the other function would look like:

```javascript
function getDaysAbsentOrLate(record) {
    var daysAbsentOrLate = 0;
    for (var i = 0; i < record.length; i++) {
        if (record[i] !== "here") {             // note how i can just do the reverse of checking for "here"
            daysAbsentOrLate++;
        } 
    }
    return daysAbsentOrLate;
}

// another way following the logic that to be absent must be to not be here
function getDaysAbsentOrLate(record) {
    // the amount of days i am not here (aka absent or late) must be the total
    // days i have on record minus the days i am here
    return record.length - getDaysHere(record);
}
```

Building smaller functions give us the benefit of creating functions that are easier 
to test, name, and write. These functions are also more reusable, which means that
you can avoid writing the same logic over and over again. 

## In Summary ##

Keeping in mind a few things, you can be a highly effective programmer and refactorer (which is probably essential to being a good programmer).

Here are some key takeaways:
- Use meaningful names
- Keep it simple
- Look for repeated code