## JSX

JSX stands for JavaScript and XML which is a syntax exension to produce elements in React. JSX looks nearly identical to normmal HTML with a few minor exceptions.

#### Declarations
JSX uses variables, and constants to store HTML element information. Every element can also store attribute information as well.

```javascript
const test = <h1 className="main" id="my-title">Hello World!</h1>;
```
    
JSX declarations can only contain a single outer element, but does allow for nesting, so declaration can extend across lines with the following syntax:

```javascript
const test = (
  <div>
    <h1>Hello World!</h1>
    <p>This how we handle <b>multiline</b> syntax</p>
  </div>
);
```
#### JSX-Specific Rules
 - __Self-closing Tags__
 
JSX requires closed self-closing tags. `<br>` is not valid, `<br />` is the only valid option.

 - __class vs. className__
 
JSX uses `className` as an attribute for element classes, since `class` is a reserved word in JS.


#### Inserting JS

JavaScript can be inserted into JSX by way of curly bracket syntax:
```javascript
var myName = 'leander';
const test = <p>My name is {myName}</p>;

function returnName() {
  return myName.toUpperCase();
}
const test = <p>My name is {returnName()}</p>;
```

 - __if Statements__
 
 JSX does not compile if statemnts in line. Instead, alternate declarations of the JSX expression.
 
 ```javascript
 var num = 2;
 
 const test = (
   <h1>Hello {
   if (num < 2) {
     return 'Friend';
   } else {
     return 'World';
   }
   }!</h1>
 ); //This will not compile
 ```
 ```javascript
 var num = 2;
 
 if (num < 2) {
   myText = 'Friend';
 } else {
   myText 'World';
 }
 const test = <h1>Hello { myText }!</h1>; //This will compile
 ```
 - __Ternary Operator__
 Rather than use if/else statements, ternary operators do work inline, and provide an easy alternative.
 ```javascript
 var num = 2;
 const test = <h1>Hello { num < 2 ? 'Friend' : 'World' }!</h1>;
 ```
 - __&& Operator__
    
#### Importing
After properly sourcing react with the script tags, `React` and `ReactDOM` must be imported for practical use.

```javascript
import React from 'react';
import ReactDOM from 'react-dom';
```

To render JSX we declared earlier, we call the `ReactDOM.render()` function, where the first argument is a JSX expression and the second expression is the container element.

```javascript
//ReactDOM.render( JSX, location );
ReactDOM.render( test, document.querySelector('body') );
```

#### Virtual DOM
'Rendering' JSX is React's way of saying that it's compiling the JSX and applying it to the Document Object Model (DOM).
The reason why React is so widely used is because of how effective and efficient it is at updating the DOM. Usually, when JavaScript makes changes to the DOM, it has to rebuild the entire model, even though maybe only one element is being changed. The Virtual DOM is a representation of the DOM, which isn't visible to any user. React notes the changes that come from a `ReactDOM.render()` call, and updates the Virtual DOM. The Virtual DOM is then compared to the actual DOM (this is called _diffing_) and __only changes the necessary specific objects on the real DOM__. Doing this avoids a lot of unnecessary DOM updating, and lets React run quicker and more efficiently.
