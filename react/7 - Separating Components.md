## Separating Components
It's very easy for a React component to get complicated and overcrowded. It may contain a constructor, along with many functions, variables and logic, all while rendering JSX as well. That is why React programmers generally follow a convention: If a component already has logic, functions, a state and decision-making, it shouldn't _also_ have to render JSX. This is how we seperate complex components into __Presentational__ and __Container__ components.

### Container Components
Even though the name suggests a simple wrapper, these components contain most of logic when it comes to the app. They will contain the state, function set, constructor method and maybe even variables/constants. They do contain a `render()` method, but not a complex one, usually only one other component instance. Here's an example.
```js
class Container extends React.Component {
  constructor(props) {...}
  calculateSomething() {...};
  computeAverageTime() {...};
  if (something) {this.setState(...)}
  render() { return <Presentational value={this.state.x} />; }
}
```
These are also the components which may include rendering to the DOM, meaning, __they will occur inside: `ReactDOM.render( ... )__`

### Presentational Components
_Presentational_ components are the components which render the JSX, usually contained within the larger _container_ components. Recall that to _render_ JSX, does not always mean to display on the DOM, and actually for presentational components it means the opposite. These will be rendered into the parent component, so if contained on a seperate file, __they will not contain the following:__
```js
import ReactDOM from 'react-dom';
ReactDOM.render( ... );
```
Instead, a presentational component will contain the HTML-like JSX, like in this example:
```js
function Presentational(props) {
  return(
    <div>
      <h1>Some Title</h1>
      <h2>Here's a value</h2>
      <h3>{props.value}</h3>
    </div>
  );
}
```
### Presentational Component Notation
We use the function notation since There is only a render method in this type of component. These are often referred to as _stateless functional components (SFCs)_. Keep in mind as we move on, and take note that the notation will change as per React development convention. Rather than a function declaration we can use _assignment_ to alter/perform operations on our components.
```js
//Outdated function SFC declaration
function PresCompName(props) {
  return <div></div>;
}
//Assignment SFC declaration
var PresCompName = function(props) {
  return <div></div>;
}
//ES6 Assignment SFC declaration
const PresCompName = (props) => {
  return <div></div>;
}
//Note: these are still components, so they can also be exported and imported
```
