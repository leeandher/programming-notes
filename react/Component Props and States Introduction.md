## Component Props

### Basics
Props is short for _properties_ and refers to the specific named values passed when creating an instance of a component. That is a complicated statement to process but it really isn't terrible difficult to understand. See this example:
```javascript
var exampleAge = 45;
ReactDOM.render( 
  <ExampleComponent message="This is top secret!" towns={["Mississauga", "Kanata"]} age={exampleAge} isLeaked={false} />,
  document.getElementById('main')
);
```
We've passed a bunch of information to the component on render, but we need to have an existing way to handle that information in our component declaration. This is done using the `props` object.
```javascript
class ExampleComponent extends React.Component {
  render() {
    
    console.log( JSON.stringify(this.props);
    /*
   'message' : 'This is top secret!',
   'towns' : ['Mississauga', 'Kanata'],
   'age' : 45,
   'isLeaked': false
    */
    
    return(
      <div className="wrapper">
        <h1>{this.props.message}</h1>
        <h2>We are located in {this.props.towns[0]}.</h2>
        <h3>I am {this.props.age} years old!</h3>
        <h3>I am {this.props.isLeaked ? 'hiding from the enemy' : 'in the clear'}.</h3>
      </div>
    );
  }
}
```
### Logic
Props can be used (just as most constants,) in conditionals, calculations, etc.
```javascript
...
render() {
  var heightInCm = this.props.heightInFeet * 30.48;
  if (this.props.isNice) {
    return <h1>You are {heightInCm} cm tall and a great person!</h1>;
  } else {
    return <h1>You are {heightInCm} cm tall and I do not like you at all!</h1>;
  }
}
...
```
### Event Handling
Event handling can be managed using the `props` object as well. See the example first:
```javascript
class CustomButton extends React.Component {
  render() {return <button onClick = {this.props.onClick}> Click Me! </button>
}
class Exploder extends React.Component {
  handleClick() {
    alert("I've exploded!");
  }
  render() {
    return <CustomButton onClick = { this.handleClick } />
  }
}
```
This may seem confusing at first but if we trace what's going on, it's not too bad.

When we render an `<Exploder />` component, we create a `<CustomButton />` instance with the property `onClick` set to our function (`handleClick`). When we click on the `<CustomButton />`  we are clicking on the actual `<button>` element rendered within it, and that element has an Event Listener for `onClick` set to read `<CustomButton />`'s property of `onClick`!

### Children
The `props` object also has access to the children of an instance of a component. Up until now components have always been self closing, but that isn't mandatory, just usual. If a component isn't self closing (`<Example />` vs. `<Example></Example>`), it's children can be accessed using `this.props.children`. It is an array of JSX entitites.
```javascript
class ExampleWrapper extends React.Component {
  render() {
    return (
      <div>
        <Example type='libraries'>
          <li>React</li>
          <li>Angular</li>
          <li>Vue</li>
        </Example>
        <Example type='colours'>
          <li>Blue</li>
          <li>Grey</li>
        </Example>
      </div>
    );
  }
}

class Example extends React.Component { 
  render() {
    return (
      <div>
        <h1>A list of {this.props.type}!</h1>
        <ul>{this.props.children}</ul>
      </div>
    );
  }
}
```
Let's explain this code. So in our `ExampleWrapper` component, we have two `Example` components with a bunch of children and `type` properties. In our `Example` component, we see that it generates a title based on the `type` property then creates an unordered list. Since all of the `children` of the `Example` components we have (contained in `ExampleWrapper`) are `li` tags the code renders an unordered list of those children. 

If we did not have the unordered list, the `li` children would not be rendered. They are contained within the `Example` component, which didn't render them, so they will not display.


### Default Props
Sometimes, we'd like to have certain properties be the default unless specified by the user. We do so by using the following: 
```javascript
class Example extends React.Component {
  render() {
    return <button>{this.props.msg}</button>
  }
}

Example.defaultProps = {
  msg: 'I am a button.';
}

/*
  Rendering <Example /> will have a msg value of 'I am a button.'
  Rendering <Example msg='' /> will have a msg value of ''
*/
```

## Component States

### Initial States
Components in React also have a special object known as the `state`. The `state` object represents the current `state` of any component instance. It requires a constructor method.
```javascript
class Example extends React.Component {
  constructor(props) {
    super(props);
    this.state = {title: 'An example'};
  }
  render() {
    return <h1>{this.state.title}</h1>;
  }
}
```
Since our component `Example` is a subclass of `React.Component`, we call the `constructor` and the `super()` function to inherit properties and call the constructor of the parents. Inheritance and class based programming information can be found here: http://exploringjs.com/es6/ch_classes.html.

### Changing States
A component doesn't only read it's own state, it can change it's state, using the function `this.setState()`. Take a look at this:
```javascript
//Let's say this was the initial state
{
  mood:   'great',
  hungry: false
}
//We can change the initial states by the following
this.setState( { hungry: true } );
//Now if we were to call the 'state' object...
{
  mood: 'great',
  hungry: true
}
```

### Changing States from Another Function
In order to allow a function to change the state of a component instance, we first need to `bind` it. That means that we insert a line in the constructor which links the function's operation to that specific instance, rather than every rendered instance of that component. Here's an example:
```javascript
  constructor(props) {
    super(props);
    this.state = {state: stateValue};
    this.function = this.function.bind(this); //Now the function will only operate on this instance
  }
```
If we invoke a state change, it needs to be done in a seperate function for clarity. Take a look:
```javascript
class Toggle extends React.Component {
  constructor(props) {
    super(props);
    this.state = {color: '#FDFDFD'};
    this.changeColour = this.changeColor.bind(this);
  }
  changeColor() {
    this.setState(color: this.state.color === '#FDFDFD' ? '#4DCCB0' : '#FDFDFD');
  }
  render() {
    return (
      <button
        style={{background: this.state.color}} 
        onClick={this.changeColor}>
        Change Color
      </button>
    );
  }
}
```
If we were to render this `Toggle` component, every time the button element is clicked, it's background would change color, even though we aren't re-rendering it, we are just changing the state value. This is because __`this.setState()` automatically invokes the `render()` function after completing the change__.
