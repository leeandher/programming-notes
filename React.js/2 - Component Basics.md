## Component Basics

### Types of Components
A component is a function or a class which optionally accepts input, and returns a React element. There are two basic types of components, __Functional Components__ and __Class-based components__. The difference between the two depends on the _state_ and the _usage_ of the created component. _Component States_ are covered more in depth in the next note, but for now lets see how they're declared.
```javascript
//Functional component declaration
function NewComponent(props) {
  return <div></div>
}

//Class-based component declaration
class NewComponent extends React.Component {
  render() {
    return <div></div>;
  }
}
```
In terms of when to use which, in most cases, class-based components are the way to go, but if you have a static component which doesn't and won't ever have any state, or functions attached to it which need to be assessed outside of itself then it's clearer to use a functional component. Essentially, a functional component is sufficient if your class-based component only contains a render method.

### Component Class
Every component that we render to the document  is part of a _component class_. As per convention, __component classes always start with a capital letter__.
To create a 'Hello World' component, we'd use the following:
```javascript
class TestComponentClass extends React.Component {
  render() {
    return <h1>Hello World!</h1>;
  }
}
```
### Rendering Components
In order to actually see the 'Hello World' component we previously created, we'd have to use the `ReactDOM.render()` function. To render an instance of our component, we call it similarly to an HTML tag, except it's crticial to note; __components must be self-closing (ex. `<TestComp />`)__.
```javascript
//ReactDOM.render( component , location );
ReactDOM.render(
  <TestComponentClass />,
  document.getElementById('main')
);
```
In the `TestComponentClass` declaration, the actual 'Hello World' text is inside a render method. This is because the component class is a set of instructions, and when we call the `ReactDOM.render()` function, we are actually we are creating an _instance_ of our class, and following the instructions contained in the class' render method.

### Component Logic
React components are quite versatile as well. They allow for the use of variables, multiline JSX, events, functions, and can even reference themselves. Here is a summarized list:
 - __MultiLine JSX__
```javascript
class TestComponentClass extends React.Component {
  render() {
    return(
      <div className="wrapper">
        <h1 id="title">Title Text</h1>
        <p id="content">Content Filler Text</p>
      </div>
    );
  }
}
```
 - __Variable Attribution__
```javascript
const user = {
  handle: 'tester',
  bio: 'test profile description',
  avatar: 'img/tester-avatar.png'
};
class TestComponentClass extends React.Component {
  render() {
    return(
      <div className="wrapper">
        <h1 id="username">{user.handle}</h1>
        <p id="userBio">{user.bio}</p>
        <img src={user.avatar} alt="User Photo" />
      </div>
    );
  }
}
```
 - __Render Logic__
```javascript
class TestComponentClass extends React.Component {
  //Declaration cannot be outside the render function for it to work properly
  render() {
    //Declaration must be in the render function
    const n = Math.floor(Math.random * 10 + 1);
    return <h1>The random number is {n}!</h1>
  }
}
```
 - ___this_ Usage__
```javascript
class TestComponentClass extends React.Component {
  //favColour 'getter' method
  get favColour() { return 'orange'; }

  render() {
    return <h1>The favourite colour is {this.favColour}!</h1>
  }
}
```
* _this_ refers to the particular instance of the `TestComponentClass` component. It calls upon the favColour 'getter' method which is why it is refered to as `this.favColour`, not `this.favColour()`.
 - __Event Listeners__
```javascript
class TestComponentClass extends React.Component {
  userAlert() { alert('User prompt!'); }
  render() {
    return <button onClick={this.userAlert}>Tester Button!</button>
  }
}
```

### Crossing Components
Components look like self-closing HTML tags because they can be used as such. They are compatible in JSX which allows you to create components which create instances of other components. Take this for example:
```javascript
class Navbar extends React.Component {
  render {
    return (
      <nav>
        <ul>
          <li>Test</li>
          <li>Test</li>
          <li>Test</li>
        </ul>
      </nav>
    );
  }
}

class Header extends React.Component {
  render {
    return(
      <div className="wrapper">
        <h1>My Test Page</h1>
        <Navbar />
        <h3>My Page Head</h3>
      </div>
    );
  }
}

ReactDOM.render(<Header />, document.getElementById('main'));
```
If we were to render an instance of the `Header` component, we would be creating an instance of the `Navbar` component as well, and both would show up in the final document render. This can also be done by importing and exporting from different `.js` files. If we were to render the same thing, but the `Navbar` component was stored elsewhere, it would look like this:


__Exporting__
```javascript
import React from 'react';
import ReactDOM from 'react-dom';

export class Navbar extends React.Component {
  render {
    return (
      <nav>
        <ul>
          <li>Test</li>
          <li>Test</li>
          <li>Test</li>
        </ul>
      </nav>
    );
  }
}
```
__Importing__
```javascript
import React from 'react';
import ReactDOM from 'react-dom';
import {NavItem} from '../nav.js';

class Header extends React.Component {
  render {
    return(
      <div className="wrapper">
        <h1>My Test Page</h1>
        <Navbar />
        <h3>My Page Head</h3>
      </div>
    );
  }
}

ReactDOM.render(<Header />, document.getElementById('main'));
```
