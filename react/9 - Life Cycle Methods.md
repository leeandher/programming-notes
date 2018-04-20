## Life Cycle Methods
React has certain methods that are called in response to certain times in a components _life cycle_. These methods are automatically bound to the component and simply need to be declared to be used. They can be split into three categories, __mounting__, __updating__ and __unmounting__ life cycle methods. They all follow the same process, so one unified example will be at the bottom of this note.

### Mounting LCMs
These methods are invoked when the given component is being _mounted_ or _unmounted_. React uses the term 'mount' to describe the act of initalizing the component into the DOM. That being said, mounting != rendering! __These functions will not be called every render, only when being added/removed from the DOM__.Here are the methods:
 - __componentWillMount()__ : Called just before the component has rendered 
 
 _NOTE_: Calling `this.setState()` in the `componentWillMount()` method will __NOT__ trigger a re-render
 
 - __componentDidMount()__ : Called immediately after the component has rendered
 
### Updating LCMs
These methods are invoked during the updating process (or re-rendering) of the given component. The method names are fairly self explanatory, but they operate slightly differently than the mounting LCMs. You can use these with regards to __whenever a component's state and/or props are changed__. Some of these methods also accept objects containing the the properties/state of the next render (`nextProps`, `nextState`), or the previous render (`prevProps`, `prevState`). The methods are as follows:
 - __componentWillReceiveProps( _nextProps_ )__ : Called ___ only if___ a component is receiving different props.
 - __shouldComponentUpdate()__ : Called just before the new `render()` to determine if `this` component should re-render
 
 _NOTE_: `shouldComponentUpdate()` __must__ return a boolean if declared. If `true`, `this` component will re-render and the opposite if `false`. 
 
 - __componentWillUpdate( _nextProps_ , _nextState_ )__ : Called if a component is about to update (re-rendered)
 - __componentDidUpdate( _prevProps_ , _prevState_ )__ : Called after a component has updated (re-rendered)
 
 ### Unmounting LCMs
 There's only one method here, and it's invoked during the _unmounting_ process. Simply stated, this is just __when the component is being removed from the DOM__, AKA the opposite of mounting.
 - __componentWillUnmount()__ : Called just before a component has been removed/_unmounted_

### Example

```js
class App extends React.Component {
  constructor(props) {
    
  }
}
```
