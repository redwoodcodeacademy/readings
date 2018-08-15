# Objects #

## Why do I need objects? ##

In JavaScript, objects can be confusing because they can represent two
somewhat different ideas, whereas in other languages there might be a 
clearer separation. 

The first idea is the map or dictionary. Most languages will call it either of
the two names, JavaScript calls it an object.

### The Dictionary Use ###

The question of when and why the map/dictionary use of the object is useful is 
best answered by looking at where the array struggles.

```javascript
// I want to store a bunch of pokemons and their attack points

var pokemons = ["squirtle", "bulbosaur", "charmander", "pikachu", "onix"];

// this correspond              // returns 23s to each pokemon in our pokemons array; ex: squirtle's attack point is 23
var attackPoints = [23, 34, 25, 30, 15];

// Now let's say I want to look up what bulbosaur's attack point is.
var bulbosaurIndex = pokemons.indexOf("bulbosaur");                 // equals 1
var bulbosaurAP = attackPoints[bulbosaurIndex];                     // equals 23
```

That wasn't too bad, but you might see that it could get more and more complicated if I were
to add an array for defense points or who their trainers are. Arrays are best when the data is
relatively simple and not relational (such as the array doesn't have to correspond to another).

Here is where the object shines (when used like a map/dictionary):
```javascript
var pokemons = {
    squirtle: 23,
    bulbosaur: 34,
    charmander: 25,
    pikachu: 30,
    onix: 15
};

// let's see how I could get onix's attack points
pokemons.onix;      // returns 15
// or you can write it like this (note the quotes required)
pokemons["onix"];   // also returns 15


// let's say I want to add more things to my pokemon field like defense points and owner
var pokemons = {
    squirtle: {
        attackPoints: 23,
        defensePoints: 10,
        owner: "Misty"
    },
    bulbosaur: {
        attackPoints: 34,
        defensePoints: 10,
        owner: "Gary"
    },
    charmander: {
        attackPoints: 25,
        defensePoints: 10,
        owner: "Ash"
    },
    pikachu: {
        attackPoints: 23,
        defensePoints: 10,
        owner: "Ash"
    },
    onix: {
        attackPoints: 15,
        defensePoints: 20,
        owner: "Brock"
    }
};

// You can nest objects in objects! This makes things very extendable. 
// let's see how you get attack points again and also defense points.
pokemons.squirtle.attackPoints;             // returns 23
pokemons.squirtle.defensePoints;            // returns 10

// Likewise you can still use bracket notations; still note the quotes around the keys
pokemons["squirtle"]["attackPoints"]; 
pokemons["squirtle"]["defensePoints"];
```


### The Class Use ###

Remember how I mentioned JavaScript has two ideas for their objects? The second is
called the class object. This is not crazy different, but it has some subtle differences.

Let's stick with our pokemon example. Notice how all of our pokemons seemed to have the same
characteristics? Attack points, defense points, and an owner field. What if I could create that
in a general and repeatable manner?

```javascript
// this is called a constructor function, it constructs Pokemon objects
function Pokemon(attackPoints, defensePoints, owner) {
    this.attackPoints = attackPoints;           // hmm... this "this" keyword looks funky
    this.defensePoints = defensePoints;
    this.owner = owner;
}
/* 
    What the "this" keyword is saying is that we are creating an object and "this" object has 
    attackPoints, defensePoints, and an owner field based on the parameters I gave it.
*/

// Let's make a pokemon now!
var pikachu = new Pokemon(23, 10, "Ash");       // we need to use the special keyword "new" to use our Pokemon constructor
pikachu;                                        // looks like this: {attackPoints: 23, defensePoints: 10, owner: "Ash"}

// how do we get pikachu's attack points?
pikachu.attackPoints;           // returns 23
// or 
pikachu["attackPoints"];        // also returns 23
// notice how this is identical to calling our objects earlier?

// Let's build what we had earlier in our map/dictionary example with our new constructor
var pokemons = {
    squirtle: new Pokemon(23, 10, "Misty"),
    bulbosaur: new Pokemon(34, 10, "Ash"),
    charmander: new Pokemon(25, 10, "Ash"),
    pikachu: new Pokemon(23, 10, "Ash"),
    onix: new Pokemon(15, 20, "Brock")
};

pokemons.onix.attackPoints;             // still works; returns 15
pokemons["onix"]["attackPoints"];       // still works as well; remember that the keys must be strings! (keys: onix, attackPoints)
```

In this example, I combined both the map/dictionary with our new fancy class constructor. 

Note that they 
do exactly the same thing in my examples.
However, the class constructor seemed to remove a lot of visual
space. 

Sometimes you'll want to do this because it makes sense to group your data as a class such as "Pokemon".
Sometimes it will make a lot more sense to just keep it as a plain object like in my first example.

The main takeaway from this is that you can use objects as powerful abstractions to let organize and
retrieve your data fast and cleanly. It will save you a lot of headache sifting through your arrays 
(i.e. maps/dictionaries, when appropriate), and you can represent very cool things as objects as well 
(i.e. Pokemons, Animals, etc.). 
