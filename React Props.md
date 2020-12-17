## Pass Props to a Stateless Functional Component
You can pass props, or properties, to child components.
```javascript
const CurrentDate = (props) => {
  return (
    <div>
      { /* Access *createdPropertyDate* like this*/ }
      <p>The current date is: {props.createdPropertyDate} </p>
    </div>
  );
};

class Calendar extends React.Component {
  constructor(props) {
    super(props);
  }
  render() {
    return (
      <div>
        <h3>What date is it?</h3>
        { /* The created property *createdPropertyDate* is getting passed into props */ }
        <CurrentDate createdPropertyDate={Date()}/>
      </div>
    );
  }
};
```
---
## Pass an Array as Props
To pass an array to a JSX element, it must be treated as JavaScript and wrapped in curly braces.

```javascript
const List = (props) => {
  return <p>{props.arr.join(", ")}</p>;
};

class ToDo extends React.Component {
  constructor(props) {
    super(props);
  }
  render() {
    return (
      <div>
        <h1>The below will output in separate lines but with commas</h1>
        <List arr={["One", "Two", "Three"]} /> 
        <List arr={["Four", "Five", "Six"]} />
      </div>
    );
  }
};
```
---
## Use Default Props
Assign default props to a component as a property on the component itself and React assigns the default prop if no value is passed in.
```javascript
const ShoppingCart = (props) => {
  return (
    <div>
      <h1>Shopping Cart Component</h1>
    </div>
  )
};
// Use this syntax:
ShoppingCart.defaultProps = {items: 0}
```
---
## Override Default Props
Override default props by explicitly setting the prop values for a component.
```javascript
const Items = (props) => {
  return <h1>Current Quantity of Items in Cart: {props.quantity}</h1>
}

Items.defaultProps = { //here are the default props
  quantity: 0
}

class ShoppingCart extends React.Component {
  constructor(props) {
    super(props);
  }
  render() {
    return <Items quantity={10}/> //quanity is overriding default prop values here.
  }
};

```
---
## Use PropTypes to Define the Props You Expect
PropTypes is imported independently from React, like this: import PropTypes from 'prop-types';  
Set propTypes on your component to require the data to be of a type (array, etc).
```javascript
const Items = (props) => {
  return <h1>Current Quantity of Items in Cart: {props.quantity}</h1>
};

Items.propTypes = { quantity: PropTypes.number.isRequired }
also: PropTypes.func.isRequired, PropTypes.bool.isRequired... object, string, symbol, element... see https://reactjs.org/docs/typechecking-with-proptypes.html

Items.defaultProps = {
  quantity: 0
};

class ShoppingCart extends React.Component {
  constructor(props) {
    super(props);
  }
  render() {
    return <Items />
  }
};
```
---

## Access Props Using this.props
ES6 class component uses the this keyword.
```javascript
class PassAlongText extends React.Component {
  constructor(props) {
    super(props);

  }
  render() {
    return (
        <div>
            <p>The text that is passed along needs to: <strong>{this.props.thisIsTheProp}</strong></p>
        </div>
    );
  }
};

class ResetPassword extends React.Component {
  constructor(props) {
    super(props);

  }
  render() {
    return (
        <div>
            <PassAlongText thisIsTheProp={'use this.props with an ES6 class'}/>
        </div>
    );
  }
};
```
---
## Review Using Props with Stateless Functional Components
```javascript
class CampSite extends React.Component {
  constructor(props) {
    super(props);
  }
  render() {
    return (
      <div>
        <Camper/>
      </div>
    );
  }
};

const Camper = (props) => <p>{props.name}</p>;


Camper.defaultProps = {
  name: "CamperBot"
};

Camper.propTypes = {
  name: PropTypes.string.isRequired
};
```
---
## Create a Stateful Component
Create state in a React component by declaring a state property on the component class in its constructor.  
This initializes the component with state when it is created. 

```javascript
class StatefulComponent extends React.Component {
  constructor(props) {
    super(props);
      this.state = {
        name: 'This text is accessed through the state!'
      }
  }
  render() {
    return (
      <div>
        <h1>{this.state.name}</h1>
      </div>
    );
  }
};
```
---
## Render State in the User Interface
When state data updates, it triggers a re-render of the components using that data.  
A components state is completely encapsulated, or local to that component, unless you pass state data to a child component as props.

```javascript
class MyComponent extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      text: 'this will get passed through'
    }
  }
  render() {
    return (
      <div>
          <h1>{this.state.text}</h1>
      </div>
    );
  }
};
```
### Render State in the User Interface Another Way
```javascript
class MyComponent extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      name: 'this will get passed through'
    }
  }
  render() {
      const name = this.state.name
    return (
      <div>
          <h1>{name}</h1>
      </div>
    );
  }
};
```
---
## Set State with this.setState
this.setState() changes a components state.  
Keys are state properties.  
Values are updated state data.  
```javascript
class MyComponent extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      name: 'Initial State'
    };
    // A class method typically needs to use the this keyword so it can access properties on the class (such as state and props) inside the scope of the method.  
    // this becomes bound to the class methods when the component is initialized
    this.handleClick = this.handleClick.bind(this);
  }

  handleClick() { //class method needs to be bound
    this.setState({ 
      // update with key value pairs
      // key is name 
      // value is 'Updated State data when clicked!'
      name: 'Updated State data when clicked!'
    })
  }
  render() {
    return (
      <div>
        <button onClick={this.handleClick}>Click Me</button>
        <h1>{this.state.name}</h1>
      </div>
    );
  }
};
```
## Use State to Toggle an Element
Pass setState a function that allows you to access state and props.  
Using a function with setState guarantees you are working with the most current values of state and props.
```javascript
class MyComponent extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      visibility: false
    };
    this.toggleVisibility = this.toggleVisibility.bind(this);
   }
  toggleVisibility() {
    this.setState(state => ({
      visibility: !state.visibility //set it to whatever it is not
    }));
  }
  render() {
    if (this.state.visibility) {
      return (
        <div>
          <button onClick = {this.toggleVisibility}>Click Me</button>
          <h1>Now you see me!</h1>
        </div>
      );
    } else {
      return (
        <div>
          <button onClick = {this.toggleVisibility}>Click Me</button>
        </div>
      );
    }
  }
};
```
---
## Write a Simple Counter
```javascript
class Counter extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      count: 0
    };

    this.increment = this.increment.bind(this)
    this.decrement = this.decrement.bind(this)
    this.reset = this.reset.bind(this)

  }

  reset() {
    this.setState(state => ({
      count: 0
    }))
  }

  decrement() {
    this.setState(state => ({
      count: state.count - 1
    }));
  }

  increment() {
    this.setState(state => ({
      count: state.count + 1 //set it to whatever it is not
    }));
  }
  render() {
    return (
      <div>
        <button className='inc' onClick={this.increment}>Increment!</button>
        <button className='dec' onClick={this.decrement}>Decrement!</button>
        <button className='reset' onClick={this.reset}>Reset</button>
        <h1>Current Count: {this.state.count}</h1>
      </div>
    );
  }
};
```
---

## Create a controlled input
Form control elements for text input, such as input and textarea, maintain their own state in the DOM as the user types.  
With React, you can move this mutable state into a React component's state.  
The user's input becomes part of the application state, so React controls the value of that input field.  
Typically, if you have React components with input fields the user can type into, it will be a controlled input form.  
```javascript
class ControlledInput extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      input: ''
    };
    this.handleChange = this.handleChange.bind(this)
  }

  handleChange(event) {
    this.setState({
      input: event.target.value
    })
  }

  render() {
    return (
      <div>
        <input value = {this.state.input} onChange = {this.handleChange.bind(this)}>
        <h4>Controlled Input:</h4>
        <p>{this.state.input}</p>
      </div>
    );
  }
};
```
---

## Create a controlled form
```javascript
class MyForm extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      input: '',
      submit: ''
    };
    this.handleChange = this.handleChange.bind(this);
    this.handleSubmit = this.handleSubmit.bind(this);
  }
  handleChange(event) {
    this.setState({
      input: event.target.value
    });
  }
  handleSubmit(event) {
    event.preventDefault()
    this.setState({
      submit: this.state.input
    });
  }
  render() {
    return (
      <div>
        <form onSubmit={this.handleSubmit}>
          <input
            value={this.state.input}
            onChange={this.handleChange} />
          <button type='submit'>Submit!</button>
        </form>
        <h1>{this.state.submit}</h1>
      </div>
    );
  }
};
```
---
## Pass State as Props to Child Components
A stateful component containing the state then renders child components.  
These components to have access to some pieces of that state, which are passed in as props.  

```javascript
class MyApp extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      name: 'CamperBot'
    }
  }
  render() {
    return (
       <div>
         <Navbar name={this.state.name}/>
       </div>
    );
  }
};

class Navbar extends React.Component {
  constructor(props) {
    super(props);
  }
  render() {
    return (
    <div>
      <h1>Hello, my name is: {this.props.name}</h1> //pass piece of state into Navbar via props
    </div>
    );
  }
};
```
---

## Pass a Callback as Props
Pass handler functions or any method that's defined on a React component to a child component.  
This is how you allow child components to interact with their parent components.  
You pass methods to a child just like a regular prop.  
It's assigned a name and you have access to that method name under this.props in the child component.  
```javascript
class MyApp extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      inputValue: ''
    }
    this.handleChange = this.handleChange.bind(this);
  }
  handleChange(event) {
    this.setState({
      inputValue: event.target.value
    });
  }
  render() {
    return (
       <div>
          <GetInput input={this.state.inputValue} handleChange={this.handleChange}/> //prop called input  is assign inputValue from the MyApp state.
          //prop called handleChange is getting input handler handleChange passed to it
          <RenderInput input={this.state.inputValue}/>
       </div>
    );
  }
};

class GetInput extends React.Component {
  constructor(props) {
    super(props);
  }
  render() {
    return (
      <div>
        <h3>Get Input:</h3>
        <input
          value={this.props.input}
          onChange={this.props.handleChange}/>
      </div>
    );
  }
};

class RenderInput extends React.Component {
  constructor(props) {
    super(props);
  }
  render() {
    return (
      <div>
        <h3>Input Render:</h3>
        <p>{this.props.input}</p>
      </div>
    );
  }
};
```
---
## Lifecycle Methods 
Lifecycle hooks aka lifecycle methods, allow you to catch components at certain points in time: before rendering, updating, receiving props, etc.  
Main lifecycle methods:  
componentWillMount() componentDidMount() shouldComponentUpdate() componentDidUpdate() componentWillUnmount()  

---
## Lifecycle Method componentWillMount

```javascript
class MyComponent extends React.Component {
  constructor(props) {
    super(props);
  }
  componentWillMount() {
    console.log('The componentWillMount() method is called before the render() method when a component is being mounted to the DOM')
  }
  render() {
    return <div />
  }
};
```
---

## Lifecycle Method componentDidMount
Call an API endpoint to retrieve data. 
The best practice with React is to place API calls or any calls to your server in the lifecycle method componentDidMount().    
This method is called after a component is mounted to the DOM.  
Any calls to setState() here will trigger a re-rendering of your component.  
When you call an API in this method, and set your state with the data that the API returns, it will automatically trigger an update once you receive the data.  
```javascript
class MyComponent extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      activeUsers: null
    };
  }
  //mockApi call to simulate calling server to retrieve data after 2500 ms
  componentDidMount() {
    setTimeout(() => {
      this.setState({
        activeUsers: 1273
      });
    }, 2500);
  }
  render() {
    return (
      <div>
        <h1>Active Users: {this.state.activeUsers}</h1>
      </div>
    );
  }
}
```
---
## Add Event Listeners
The componentDidMount() method is also the best place to attach any event listeners you need to add for specific functionality.  
```javascript
class MyComponent extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      message: ''
    };
    this.handleEnter = this.handleEnter.bind(this);
    this.handleKeyPress = this.handleKeyPress.bind(this);
  }
  
  componentDidMount() {
    document.addEventListener("keydown", this.handleKeyPress);
  }
  componentWillUnmount() {
    document.removeEventListener("keydown", this.handleKeyPress);
  }

  handleEnter() {
    this.setState((state) => ({
      message: state.message + 'You pressed the enter key! '
    }));
  }
  handleKeyPress(event) {
    if (event.keyCode === 13) {
      this.handleEnter();
    }
  }
  render() {
    return (
      <div>
        <h1>{this.state.message}</h1>
      </div>
    );
  }
};
```


