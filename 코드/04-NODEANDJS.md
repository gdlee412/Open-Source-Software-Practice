 # Node and Javascript

Moving on to learning Javascript + HTML + CSS

CSS = portal / 포털
HTML = structure / 구조
Javascript = code...? / 동적

## Why Javascript
Pros
    Versatile in multi-cross platforms
    Useful for prototyping user interfaces
    No 1 programming language (PL) in GitHub
    Visibility of results
    natively working with the server-and-client architecture
Cons
    Not for computing-intensive applications
        such as multicore computing and gpu acceleration
    abstract
        not good for learning the low level working of computers
    easy to learn but hard to master
        functions, promises, asynchronous statements,...
        inconsistent operators, ever-changing specs,..
        
## Runtime
software designed to support the execution of computer programs
    Runtime needed to run javascript code
multiple runtimes are possible for the same PL
C++ program built on VS needs an installed runtime

## Node.js
the javascript runtime built on Chrome's V8 Javascript engine

### Hello World
console.log("Hello, World!");
- in terminal of file location
    node main.js
VScode
Terminal -> New Terminal (Ctrl + SHift + `)

## "let"
instead of defining specific variable types, javascript uses 'let'
let x = 3;
let y = 0.2;
let str = "abcd";
let arr = [1, 2, 3, 4];
let t = true;
let arr2 = [1, true, "abcd", [1, 2]];
*all of the above are allowed in javascript

## "const"
constant variable, it cannot be assigned again
const y = 1;
y = 5; //Error!

## Five Primitive Types:
Number: 1, -2, 3.141592653589793
String: "Hello come in" (single quotes(') and double quote(") both define strings)
Boolean: true or false
undefined
null

There are more: BigInt and Symbol

## Primitive types are immutable
the variable values can change, but the specifics within each variable cannot be altered
str = "abc";
str = "def"; //this is fine
str[0] = "q"; //error it does not change

must get a new String and replace the strings there with <replaceAll>

let str = "abc";
let str2 = str.replaceAll("a", "c");

console.log(str2); //"cbc" 
consolde.log(str); //"aba"

## Operators
almost all the operators in C
arithmetic: +, -, *, /, %,/ ++, --
assignment: =, +=, -=, *=, /=, %=
comparision: ===, !==, >, <, >=, <=, ? (not ==, !=)
logical: &&, ||, !
Bitwise: &, |, , ^, <<, >>
type: typeof (gives the type using string)

## type conversion
operators can be applied between two variables of diferent types
"abc" + 1 = "abc1"

## if and for statements
almost the same as c except:
let, console.log, ===, i (there are no %d)
everything else is more or less the same as C

## Arrays
can have values of different types
can be altered
typeof array; // "object" not "array"
use Array.isArray(variable); //true

## Object Data Structures
like dictionaries, it can contain keys and values
    initialized with an object literal, {}
    {key: value, key2: value2};
//these all work
let obj = {};
obj.x = 10;
obj[y] = 10; // "" not needed
obj["z"] = 11;

## Complex Data Structures
let IDCLab = {
    director: {
        name: "Jaemin Jo"
    },
    students: [
        {name: "John", id: 111},
        {name: "Zoey", id: 112},
        {name: "Chen", id: 113, graduated: true},
    ]
}

## Functions
a function abstracts logic
in js:
    no parameter types
    no return type (no void)
    can be called with an arbitrary numver of arguments

function sum(a, b){
    return a + b;
}
let ret = sum(5,3); //8
let x = sum(5, 3, 2); //8
let y = sum(5); //NaN (Not a Number)

functions are just objects which can be called through a call operator, ()
a function can be assigned to a variable
it can have properties as objects do

function sum(a, b){
    return a + b;
}

let add = sum;
add(2, 3); //5
sum.property = "abc";
console.log(sum.property); //"abc"

## Anonymous Function
Function name can be ommited
just assign it to a variable

let sum = function (a, b){
    return a + b;
};

let ret = sum(5, 3); //8

useful in assigning several functions to one variable

let opType = "add", opFunc;

if (opType === "add")
    opFunc = function(a, b){
        return a + b;
    };
else if (opType === "sub")
    opFunc = function(a, b){
        return a - b;
    };

let ret = opFunc(5, 3);

## Arrow functions
the <function> keyword can be omitted as well using arrow functions
(args) => {body}
arrow functions are anonymous

let print = (x) => {
    if (x % 2) console.log(x, "is odd.");
    else console.log(x, "is even,");
}

let sum = (a, b) => {
    return a + b;
};

let sum2 = (a, b) =>  a + b; //shortest form

## Array Methods
array.push(x)  //adds value x to array
array.findIndex(x) // find index of x in array
array.includes(x) //boolean and checks if x is in array
array.slice(x, y) // creates an array from the main array which includes the values of the given indices
array.concat([x, y]) // adds the values to to the main arrays

## Destructive and Non Destructive methods
Destructive methods destroy the format of the main array, changes the array
Non destructive methods will create a new array and wont alter the original array

Destructive methods: 
    array.push(x): append x to array
    array.pop(): remove last element
    array.unshift(x): prepend x to array
    array.shift(): remove the first element
    array.splice(): replace the content (not array.slice())
    array.sort(): sort array
rest are non destructive

## Array Methods Continued
collective operation on arrays

array.map(x => function) -> usually to do an arithmetic to all the elements of array (creates new array with values)
array.fiter(x => condition  ) -> filter out given a condition
(also non destructive)
array.forEach(f) => iterate over each element in array return value of this is undefined

Method chaining can occur
arr = [1, 2, 3, 4, 5]
arr.map((ele) => ele * 2)
.filter((ele) => ele > 5);

## Summary
- Five Primitive types: number, string, boolean, null, and undefined
- weakly-typed: the let keyword
- if, for, and while statements have similar syntax to C
- functions are just callable objects
    function name(a,b) {return a + b;}
    let name = function (a, b) {return a + b;} <anonymous function>
    let name = (a, b) => {return a + b;} <arrow function>
    let name = (a, b) => a + b; (short form)
- Array methods and method chaining
    map, filter, and forEach