## Pass Props to a Stateless Functional Component
You can pass props, or properties, to child components.
```
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

```
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
```
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

## Override Default Props
Override default props by explicitly setting the prop values for a component.
```
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
## Use PropTypes to Define the Props You Expect
PropTypes is imported independently from React, like this: import PropTypes from 'prop-types';
Set propTypes on your component to require the data to be of a type (array, etc).

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

## Access Props Using this.props
ES6 class component uses the this keyword.
```
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
```
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

## Create a Stateful Component
Create state in a React component by declaring a state property on the component class in its constructor. 
This initializes the component with state when it is created. 

```
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