## Re-Renders with shouldComponentUpdate
React provides the  lifecycle method shouldComponentUpdate() you can call when child components receive new state or props, and declare specifically if the components should update or not.

shouldComponentUpdate() must return a boolean value. Use it by comparing current (this.props) to next props (nextProps)

```javascript
class OnlyEvens extends React.Component {
  constructor(props) {
    super(props);
  }
  shouldComponentUpdate(nextProps, nextState) {
    console.log('Should I update?');
    return (nextProps.value % 2 === 0) //only updates when value of prop is even
  }
  componentDidUpdate() {
    console.log('Component re-rendered.');
  }
  render() {
    return <h1>{this.props.value}</h1>;
  }
}

class Controller extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      value: 0
    };
    this.addValue = this.addValue.bind(this);
  }
  //all this does is increment numbers by 1
  addValue() {
    this.setState(state => ({
      value: state.value + 1
    }));
  }
  render() {
    return (
      <div>
        <button onClick={this.addValue}>Add</button>
        <OnlyEvens value={this.state.value} />
      </div>
    );
  }
}

```
---
## Inline Styles
Apply styling by importing from a stylesheet and adding a class using the className attribute.
Or, apply styles inline like this
```javascript
class Colorful extends React.Component {
  render() {
    return (
      <div style={{color: "red", fontSize: 72}}>Big Red</div>
    );
  }
};
```