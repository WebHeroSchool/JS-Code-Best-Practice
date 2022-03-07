# JS-Code-Best-Practice

### 1. Naming

Names of your variables and functions sholud be easy to understand, short and readable. Otherwise it will be very difficult for a reader to keep up with the flow of your code logic.

#### Good
``` js
function isLegalDrinkingAge() {
...
}
```
#### Bad
``` js
function age() {
...
}
```

### 2. Avoid globals

If you have global variables or functions in your code, scripts included after yours that contain the same variable and function names will overwrite your functions/variables.
Use local functions/variables and closures instead.

#### Good
``` js
var DudeNameSpace = {
    name : 'Jeffrey',
    lastName : 'Way',
    doSomething : function() {...}
 }
 console.log(DudeNameSpace.name); // Jeffrey
```
#### Bad
``` js
var name = 'Jeffrey';
 var lastName = 'Way';
 function doSomething() {...}
 console.log(name); // Jeffrey -- or window.name
```
### 3. Pay attention to (the lack of) hoisting when using classes

Unlike functions, classes are not hoisted. You always need to declare a class before you call it, otherwise you’ll get an uncaught reference error.
Example:
``` js
// uncaught reference error
const hat = new Product("red hat", 1000);
hat.displayInfo();
class Product { … }

// good order - the class is declared first
class Product { … }
const hat = new Product("red hat", 1000);
hat.displayInfo();
```

### 4. Comments

Comment your code, especially functions, classes, objects, and interfaces, but only include key information. To keep your comments concise and easy to read, use tags such as `@constructor`, `@param`, `@version`, `@return`, and others. Overly long and verbose comments are unnecessary because they’ll take extra time to read through and understand.
Example:
``` js
/**
* Represents a book.
* @constructor
* @param {string} title - The title of the book.
* @param {string} author - The author of the book.
*/
function Book(title, author) { … }
```

### 5. Avoid using JavaScript to add styling

Technically, JavaScript allows you to directly change the CSS code using the `style` property. However, to make debugging easier and improve code maintainability, it’s best to avoid it.
As an alternative, you can add and remove classes using the ClassList API as follows (then add the style rules with CSS):
``` js
// selects the first p tag on the page
let p = document.querySelector("p");
// dynamically adds classes
p.classList.add("class-1", "class-2");
// dynamically removes classes
p.classList.remove("class-3", "class-4");
// based on the presence of the class, it’s either added or removed
p.classList.toggle("class-5");
```

### 6. Eval()

`eval` lets us pass in a string with JavaScript code and run it. This is dangerous because it can potentially let anyone run JavaScript code that we didn’t write. It can open up your program to several kinds of injection attacks.

### 7. Beware of Automatic Type Conversions

Because JavaScript is loosely typed, a variable can contain different data types. Also, a variable can change its data type. We can simply do this:
``` js
var text = "Hello";
text = 5;
```
With the second statement variable text is converted from type string to a number.

### 8. Use Template Literals

Template literals make working with strings much easier than before. Use them instead of long string concatenation.

### 9. `debugger` statements in the code

The `debugger` statement can be used to force a browser breakpoint during manual testing. This can aid developers in quickly locating bugs, but it will cause optimization build failures if left in the code. Its better to locate the desired code location and manually set breakpoint using browser tools.

### 10. Never use hyphens in variable names

These can get confused with subtraction attempts.
Example:
``` js
let hello-world = "Hi there";
```
Results in an attempt to subtract 'world' from 'hello', throwing errors.
