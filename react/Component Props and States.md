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
    return <h1>You're {heightInCm} cm tall and a great person!</h1>;
  } else {
    return <h1>You're {heightInCm} cm tall and I don't like you at all!</h1>;
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
    alert('I've exploded!');
  }
  render() {
    return <CustomButton onClick = { this.handleClick } />
  }
}
```
This may seem confusing at first but if we trace what's going on, it's not too bad.

When we render an `<Exploder />` component, we create a `<CustomButton />` instance with the property `onClick` set to our function (`handleClick`).When we click on the `<CustomButton />`  we are clicking on the actual `<button>` element rendered within it, and that element has an eventListner for `onClick` set to read `<CustomButton />`'s property of `onClick`!

Therefore, from button click, the event listener on `<button>` class the `onClick` `prop` of `<CustomButton />`. That prop is declared in `<Exploder />` and is tied to `<Exploder />`'s own 'getter' function `handleClick`.

#HERE

## Component States

