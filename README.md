ECMAScript 2015 (previously ES6) is the newest version of the ECMAScript standard. It is a significant update to the language, and the first major update to the language since ES5 was standardized in 2009. Implementation of these features in major JavaScript engines is underway now. Though, currently no web browsers support ES6 directly, but there are a lot of transpilers (eg Babel) that does the conversation for the browser excellently. Here are some new features that will come in handy while coding 

'let' is the new 'var'
---------------------- 

So what do you think this block of code will print after executed?

...
var name = "JOSIM";

if(true) { 
  var name = "Sodrul"; 
  console.log(name); 
};

console.log(name);
...

In general logic, it should've printed "Sodrul" and "JOSIM", right? As, we declared name to be "JOSIM" outside the if block, we'd expect it won't change after whatever we do inside another block, right?

Wrong. This is one of the weired features of JS (after all, the language was written in just 2 weeks, #BRANDENISBOSS)

When executed this code behaves like,

...
var name = "JOSIM";

if(true) { 
  name = "Sodrul"; 
  console.log(name); 
};

console.log(name);
...

and prints "Sodrul", "Sodrul" as output.

The 'let' keyword is going to fix this issue.'let' allows you to declare variables limited in scope to the block, statement or expression on which its being used. It's slightly different from the 'var' keyword, which defines variables globally (or locally to an entire function regardless of block scope).

So, this code should behave exactly as you thought,

...
let name = "JOSIM";

if(true) { 
  let name = "Sodrul"; 
  console.log(name); 
};

console.log(name);
...

and print "Sodrul", "JOSIM"

https://babeljs.io/repl/#?evaluate=true&presets=es2015%2Creact%2Cstage-2&code=let%20name%20%3D%20%22JOSIM%22%3B%0A%0Aif(true)%20%7B%20%0A%20%20let%20name%20%3D%20%22Sodrul%22%3B%20%0A%20%20console.log(name)%3B%20%0A%7D%3B%0A%0Aconsole.log(name)%3B

One thing to remember though, unlike var, 'let' does not create a property on the global object.

...
var x = 'Salekin';
let y = 'Salekin';
console.log(this.x); // Salekin
console.log(this.y); // Undefined
...

https://babeljs.io/repl/#?evaluate=true&presets=es2015%2Creact%2Cstage-2&code=var%20x%20%3D%20'Salekin'%3B%0Alet%20y%20%3D%20'Salekin'%3B%0Aconsole.log(this.x)%3B%20%2F%2F%20Salekin%0Aconsole.log(this.y)%3B%20%2F%2F%20Undefined

Also, redeclaring the same variable within the same function or block scope will raise SyntaxError.

...
if(true) {
  let x;
  let x; // SyntaxError thrown, Duplicate declaration "x"
}
...

https://babeljs.io/repl/#?evaluate=true&presets=es2015%2Creact%2Cstage-2&code=if(true)%20%7B%0A%20%20let%20x%3B%0A%20%20let%20x%3B%20%2F%2F%20SyntaxError%20thrown%0A%7D

For indepth discussion read https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/let


Constants
---------

This might sound funny, but the concept of constant is new in javascript.
`const` means that the variable can’t be reassigned. (Not to be confused with immutable values. Unlike true immutable datatypes such as those produced by Immutable.js and Mori, a `const` object can have properties mutated.)

const PI = Math.PI;

This declaration creates a constant that can be either global or local to the function in which it is declared. An initializer for a constant is required; that is, you must specify its value in the same statement in which it's declared (which makes sense, given that it can't be changed later).

const PI = Math.PI;Strings in JavaScript was kind of limited, lacking the capabilities one might expect coming from Ruby. 
ES6 Template Literals, fundamentally change that. They can be used for:

1. String Interpolation
2. Embeded expressions
3. Multiline Strings (without any hacks)
4. String formatting
5. String tagging for safe HTML escaping, logalization etc.

Here's an example of String interpolation:

...
var greet = function(name) {
 console.log(`Hello ${name}`);  // just like ruby #{}
}

greet("josim"); // prints "Hello josim"
...

https://babeljs.io/repl/#?evaluate=true&presets=es2015%2Creact%2Cstage-2&code=var%20greet%20%3D%20function%28name%29%20{%0A%20console.log%28%60Hello%20%24{name}%60%29%3B%0A}%0A%0Agreet%28%22josim%22%29%3B

Example of multiline strings:

...
let x = `string text line 1
string text line 2`;

console.log(x);
...

will actually produce the code:

...
var x = "string text line 1\nstring text line 2";
console.log(x);
...

and output:

...
string text line 1 
string text line 2
...

https://babeljs.io/repl/#?evaluate=true&presets=es2015%2Creact%2Cstage-2&code=let%20x%20%3D%20%60string%20text%20line%201%0Astring%20text%20line%202%60%3B%0A%0Aconsole.log%28x%29%3B

For detail explanation, read this article by Addy Osmani
https://developers.google.com/web/updates/2015/01/ES6-Template-Strings?hl=en

...
PI = 100; // will raise error, "PI" is read-only
...

https://babeljs.io/repl/#?evaluate=true&presets=es2015%2Creact%2Cstage-2&code=const%20PI%20%3D%20Math.PI%3B%0Aconst%20PI%20%3D%20100%3B%0Aconsole.log%28PI%29%3B

Constants are block-scoped, much like variables defined using the let statement. The value of a constant cannot change through re-assignment, and it can't be redeclared.

...
const PI = Math.PI;
const PI = 1010101; // will raile error, Duplicate declaration "PI"
...

https://babeljs.io/repl/#?evaluate=true&presets=es2015%2Creact%2Cstage-2&code=const%20PI%20%3D%20Math.PI%3B%0Aconst%20PI%20%3D%20100%3B%0Aconsole.log(PI)%3B

Template Literals
-----------------

Strings in JavaScript was kind of limited, lacking the capabilities one might expect coming from Ruby. 
ES6 Template Literals, fundamentally change that. They can be used for:

1. String Interpolation
2. Embeded expressions
3. Multiline Strings (without any hacks)
4. String formatting
5. String tagging for safe HTML escaping, logalization etc.

Here's an example of String interpolation:

...
var greet = function(name) {
 console.log(`Hello ${name}`);  // just like ruby #{}
}

greet("josim"); // prints "Hello josim"
...

https://babeljs.io/repl/#?evaluate=true&presets=es2015%2Creact%2Cstage-2&code=var%20greet%20%3D%20function%28name%29%20{%0A%20console.log%28%60Hello%20%24{name}%60%29%3B%0A}%0A%0Agreet%28%22josim%22%29%3B

Example of multiline strings:

...
let x = `string text line 1
string text line 2`;

console.log(x);
...

will actually produce the code:

...
var x = "string text line 1\nstring text line 2";
console.log(x);
...

and output:

...
string text line 1 
string text line 2
...

https://babeljs.io/repl/#?evaluate=true&presets=es2015%2Creact%2Cstage-2&code=let%20x%20%3D%20%60string%20text%20line%201%0Astring%20text%20line%202%60%3B%0A%0Aconsole.log%28x%29%3B

For detail explanation, read this article by Addy Osmani
https://developers.google.com/web/updates/2015/01/ES6-Template-Strings?hl=en

Extended Parameter Values
-------------------------
In ES6 you can declare default values of your parameters very easily.

...
function f (x, y = 2, z = 3) { 
  return x + y + z 
}; 

f(1) // 6  (1 + 2 + 3)
...

which was a bit tedious in previous JS versions,

...
function f (x, y, z) { 
  if (y === undefined) { 
    y = 7; 
  }
  if (z === undefined) {
    z = 42; 
  }
  return x + y + z; 
};
...

https://babeljs.io/repl/#?evaluate=true&presets=es2015%2Creact%2Cstage-2&code=function%20f%20%28x%2C%20y%20%3D%202%2C%20z%20%3D%203%29%20{%20%0A%20%20return%20x%20%2B%20y%20%2B%20z%20%0A}%3B%20%0A%0Aconsole.log%28f%281%29%29%3B

Binary and Octal literals
-------------------------
You now have direct support for safe binary and octal literals in ES6

...
0b10 //  2 (binary)
0o12 // 10 (octal)
...

which is pretty and more consice than what you needed to do in previous versions:

...
parseInt("10", 2) //  2
parseInt("12", 8) // 10
...

Arrow
-----

The most fun feature of ES6 yet is the arrow function. An arrow function expression has a shorter syntax compared to function expressions.

...
let numbers = [1,2,3,4,5,6,7];
let squared = numbers.map(v => v*v); // [1,4,9,16,25,36,49]
...

which makes the code concise and elegant. Trying to achieve the same with previous language version whould be like, 
The most fun feature of ES6 yet is the arrow function. An arrow function expression has a shorter syntax compared to function expressions.

...
let numbers = [1,2,3,4,5,6,7];
let squared = numbers.map(v => v*v); // [1,4,9,16,25,36,49]
...

which makes the code concise and elegant. Trying to achieve the same with previous language version whould be like, 

...
var numbers = [1, 2, 3, 4, 5, 6, 7];
var squared = numbers.map(function (v) {
  return v * v;
});
...

https://babeljs.io/repl/#?evaluate=true&presets=es2015%2Creact%2Cstage-2&code=let%20numbers%20%3D%20[1%2C2%2C3%2C4%2C5%2C6%2C7]%3B%0A%0Alet%20squared%20%3D%20numbers.map%28v%20%3D%3E%20v*v%20%29%3B%0A%0Aconsole.log%28squared%29%3B

If a function has multiple parameters, it can be written as

...
var multiply = (x, y) => x*y;
multiply(2,3); // 6
...

https://babeljs.io/repl/#?evaluate=true&presets=es2015%2Creact%2Cstage-2&code=var%20multiply%20%3D%20%28x%2C%20y%29%20%3D%3E%20x*y%3B%0Aconsole.log%28multiply%282%2C3%29%29%3B

Also, consider this example, which returns a JSON object after given the appropriate inputs.

...
let setNameIdsEs6 = (id, name) => ({ id: id, name: name }); 
...

which would look like this if tried in language prior ES6 

...
var setNameIdsEs6 = function setNameIdsEs6(id, name) {
  return { 
    id: id, 
    name: name 
  };
};
...

https://babeljs.io/repl/#?evaluate=true&presets=es2015%2Creact%2Cstage-2&code=let%20setNameIdsEs6%20%3D%20%28id%2C%20name%29%20%3D%3E%20%28{%20id%3A%20id%2C%20name%3A%20name%20}%29%3B%20%0A%0Aconsole.log%28setNameIdsEs6%20%284%2C%20%22Kyle%22%29%29%3B


One thing to note though, Arrow functions will always be anonymous.

To read more about them please visit, 
https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Functions/Arrow_functions

...
var numbers = [1, 2, 3, 4, 5, 6, 7];
var squared = numbers.map(function (v) {
  return v * v;
});
...

https://babeljs.io/repl/#?evaluate=true&presets=es2015%2Creact%2Cstage-2&code=let%20numbers%20%3D%20[1%2C2%2C3%2C4%2C5%2C6%2C7]%3B%0A%0Alet%20squared%20%3D%20numbers.map%28v%20%3D%3E%20v*v%20%29%3B%0A%0Aconsole.log%28squared%29%3B

If a function has multiple parameters, it can be written as

...
var multiply = (x, y) => x*y;
multiply(2,3); // 6
...

https://babeljs.io/repl/#?evaluate=true&presets=es2015%2Creact%2Cstage-2&code=var%20multiply%20%3D%20%28x%2C%20y%29%20%3D%3E%20x*y%3B%0Aconsole.log%28multiply%282%2C3%29%29%3B

Also, consider this example, which returns a JSON object after given the appropriate inputs.

...
let setNameIdsEs6 = (id, name) => ({ id: id, name: name }); 
...

which would look like this if tried in language prior ES6 

...
var setNameIdsEs6 = function setNameIdsEs6(id, name) {
  return { 
    id: id, 
    name: name 
  };
};
...

https://babeljs.io/repl/#?evaluate=true&presets=es2015%2Creact%2Cstage-2&code=let%20setNameIdsEs6%20%3D%20%28id%2C%20name%29%20%3D%3E%20%28{%20id%3A%20id%2C%20name%3A%20name%20}%29%3B%20%0A%0Aconsole.log%28setNameIdsEs6%20%284%2C%20%22Kyle%22%29%29%3B


One thing to note though, Arrow functions will always be anonymous.

To read more about them please visit, 
https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Functions/Arrow_functions
