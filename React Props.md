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