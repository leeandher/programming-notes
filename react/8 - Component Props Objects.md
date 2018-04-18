## Component Props Objects
While we learned earlier that `props` cannot be modified, we can customize the ways in which we get our `props` to our component. There are certain objects which we can attach after we've built our component which can help us use `props` properly.


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

### Prop Types
The more React Components we use and create, the easier it is to forget what type of value it needs. This kind of thing can get mixed up easily depending on the amount of people working with your code. That's why we use the `propTypes` object to prevent any bad input from affecting our components. Take a look at this example.
```js
const SoftwareStatus = (props) => {
  return (
    <div>
      <h1>{props.program}</h1>
      <h2>{props.isUpdated ? 'Uptodate ' + props.versionNumber : 'Requires Update'}</h2>
      <img src={props.thumbnail} alt={props.program + ' thumbnail'}>
    </div>
  );
}
```
Here we have a SFC which is completely dependent on having `props` in order to display properly. In order to insure it is passed the correct and required information, we do the following: 
```js
SoftwareStatus.propTypes = {
  program         = React.PropTypes.string.isRequired,
  isUpdated       = React.PropTypes.bool.isRequired,
  versionNumber   = React.PropTypes.number,  
  thumbnail       = React.PropTypes.string.isRequired
}
```
Taking a look at the `propTypes` object, we can see we put requirements on every instance of a `SoftwareStatus` component. Using `React.PropTypes.*` allows us to force certain data types when we create this component, and `.isRequired` requires that every instance possesses the attached `prop`. Here are some examples:
```js
//INVALID - isUpdated requires a boolean, versionNumber requires a number
<SoftwareStatus program="Game.exe" isUpdated="true" versionNumber="1.2" thumbnail="img/game.png"/>
//INVALID - program is a required field
<SoftwareStatus isUpdated={true} versionNumber={3.2} thumbnail="img/test_image.png">
//VALID
<SoftwareStatus program="Atom.exe" isUpdated={false} thumbnail="img/atom.jpeg"/>
```

### Component Control
Any given component can be considered a _controlled_ component, or an _uncontrolled_ component. __In a quick explanation, A controlled component does not maintain aninternal state, while a uncontrolled component does__. In other words, an uncontrolled component is _uncontrollable_ and vice versa. 99% of the time, components are controlled, because React works best with these. Let's take a look at an example:
```js
import React from 'react';
import ReactDOM from 'react-dom';

class Display extends React.Component {
  constructor(props) {
    super(props);
    this.state = { userInput: '' };
    this.handleUserInput = this.handleUserInput.bind(this);
  }
  handleUserInput(e) {
    this.setState({
      userInput = e.target.value;
    });
  }
  render() {
    return(
      <div>
        <input type="text" onChange={this.handleUserInput} value={this.state.userInput}/>
        <h1>This is your input: {this.state.userInput}</h1>
      </div>
    );
  }
}

ReactDOM.render(<Display />, document.getElementById('app'));
```
For a quick TL;DR of this code, we type `x` into `<input />`, `<Display />`'s state `userInput` is set to `x`, it renders `this.state.userInput`. Simple enough.

But actually theres something going on behind the scene. `<input />` is normally an _uncontrolled_ component. This is because if we ever query for input's value (ex. `document.querySelector('input[type="text"]').value`), we would get it's value without having to consult `<Display />`'s state. By forcing the prop `value={this.state.userInput}` onto the `<input />` tag, we convert it to a _controlled_ element!
