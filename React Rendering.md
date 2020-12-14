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
---
## Inline Style Syntax
Use camel case, as hyphenated words like `font-size` are invalid syntax for JavaScript object properties

* invalid: `font-size`  
* valid: `fontSize`  
* height, width, fontSize are defaulted to px. 
* Can use em with quotes: `{fontSize: "4em"}`  

Assigning a style object to a constant to keep code organized:

```javascript
const styles = {
  color: 'purple',
  fontSize: 40,
  border: "2px solid purple",
};

class Colorful extends React.Component {
  render() {
    return (
      <div style={styles}>Style Me!</div>
    );
  }
};
```
---
## Use Advanced JavaScript in React Render Method
Can also write JavaScript directly in your render methods, before the return statement, without inserting it inside of curly braces, because it is not yet within the JSX code. To do this place the variable name inside curly braces.  

```javascript
const inputStyle = {
  width: 235,
  margin: 5
};

class MagicEightBall extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      userInput: '',
      randomIndex: ''
    };
    this.ask = this.ask.bind(this);
    this.handleChange = this.handleChange.bind(this);
  }
  ask() {
    if (this.state.userInput) {
      this.setState({
        randomIndex: Math.floor(Math.random() * 20),
        userInput: ''
      });
    }
  }
  handleChange(event) {
    this.setState({
      userInput: event.target.value
    });
  }
  render() {
    const possibleAnswers = [
      'It is certain',
      'It is decidedly so',
      'Without a doubt',
      'Yes, definitely',
      'You may rely on it',
      'As I see it, yes',
      'Outlook good',
      'Yes',
      'Signs point to yes',
      'Reply hazy try again',
      'Ask again later',
      'Better not tell you now',
      'Cannot predict now',
      'Concentrate and ask again',
      "Don't count on it",
      'My reply is no',
      'My sources say no',
      'Most likely',
      'Outlook not so good',
      'Very doubtful'
    ];
    // here. This can also be text, etc
    const answer = possibleAnswers[this.state.randomIndex];
    // here
    return (
      <div>
        <input
          type='text'
          value={this.state.userInput}
          onChange={this.handleChange}
          style={inputStyle}
        />
        <br />
        <button onClick={this.ask}>Ask the Magic Eight Ball!</button>
        <br />
        <h3>Answer:</h3>
        <p>
        <!--here-->
          {answer}
        <!--here-->
        </p>
      </div>
    );
  }
}
```
---
## Render With an if-else Condition
if/else statements have to be used outside the return statement.  

```javascript
class MyComponent extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      display: true
    }
    this.toggleDisplay = this.toggleDisplay.bind(this);
  }
  toggleDisplay() {
    this.setState((state) => ({
      display: !state.display
    }));
  }
  render() {
    // here: if true
    if(this.state.display) {
      return (
        <div>
          <button onClick={this.toggleDisplay}>Toggle Display</button>
          <h1>Displayed!</h1>
        </div>
      );
    // here: else if not true
    } else {
      return (
        <div>
          <button onClick={this.toggleDisplay}>Toggle Display</button>
        </div>
      );
    }
  }
};
```
---
## Rendering With && Conditional
Include multiple statements directly in your JSX and string multiple conditions together by writing && after each one.
```javascript
class MyComponent extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      display: true
    }
    this.toggleDisplay = this.toggleDisplay.bind(this);
  }
  toggleDisplay() {
    this.setState(state => ({
      display: !state.display
    }));
  }
  render() {
    return (
       <div>
         <button onClick={this.toggleDisplay}>Toggle Display</button>
         <!-- here -->
         {this.state.display && <h1>Displayed!</h1>}
       </div>
    );
  }
};
```
---
## Rendering With Ternary Expression
```javascript
const inputStyle = {
  width: 235,
  margin: 5
}

class CheckUserAge extends React.Component {
  constructor(props) {
    super(props);
    // here
    this.state = {
      userAge: '',
      input: ''
    }
    this.submit = this.submit.bind(this);
    this.handleChange = this.handleChange.bind(this);
  }
  handleChange(e) {
    this.setState({
      input: e.target.value,
      userAge: ''
    });
  }
  submit() {
    this.setState(state => ({
      userAge: state.input
    }));
  }
  render() {
    const buttonOne = <button onClick={this.submit}>Submit</button>;
    const buttonTwo = <button>You May Enter</button>;
    const buttonThree = <button>You Shall Not Pass</button>;
    return (
      <div>
        <h3>Enter Your Age to Continue</h3>
        <input
          style={inputStyle}
          type="number"
          value={this.state.input}
          onChange={this.handleChange} /><br />
          <!-- here -->
          {
          this.state.userAge === ''
            ? buttonOne
            : this.state.userAge >= 18
              ? buttonTwo
              : buttonThree
          }
      </div>
    );
  }
};
```
---
## Rendering Conditionally from Props

```javascript
class Results extends React.Component {
  constructor(props) {
    super(props);
  }
  render() {
    return (
      // ternary expression to render the h1 element with the text "You Win!" or "You Lose!" based on the fiftyFifty true/false prop that's being passed in from GameOfChance
      <h1>
      {this.props.fiftyFifty ? "You Win!" : "You Lose!"}
      </h1>
    )
  };
};

class GameOfChance extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      counter: 1
    }
    this.handleClick = this.handleClick.bind(this);
  }
  handleClick() {
    this.setState({
      counter: this.state.counter + 1 // Counter adds by one
    });
  }
  render() {
    const expression = Math.random() >= 0.5 ? true : false // randomly returns a true false by use of random values
    return (
      <div>
        <button onClick={this.handleClick}>Play Again</button>
        { /* Rendering results componenet as a child of GameOfChance, and pass in expression as a prop called fiftyFifty */ }
        <Results fiftyFifty={expression} />
        <p>{'Turn: ' + this.state.counter}</p>
      </div>
    );
  }
};
```
---
## Change Inline CSS Conditionally Based on Component State
Render CSS conditionally based on the state of a React component.  
```javascript
class GateKeeper extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      input: ''
    };
    this.handleChange = this.handleChange.bind(this);
  }
  handleChange(event) {
    this.setState({ input: event.target.value })
  }
  render() {
    let inputStyle = {
      border: '1px solid black'
    };
    // here
      if (this.state.input.length > 15) { 
        inputStyle = { 
          border: '3px solid red' };
      }
      // can also do this:
      // if (this.state.input.length > 15) {
      //   inputStyle.border = '3px solid red';
      // }

    return (
      <div>
        <h3>Don't Type Too Much:</h3>
        <input
          type="text"
          style={inputStyle}
          value={this.state.input}
          onChange={this.handleChange} />
      </div>
    );
  }
};
```
---
## Use Array.map() to Dynamically Render Elements
Using components to render an unknown number of elements. 

```javascript
const textAreaStyles = {
  width: 235,
  margin: 5
};

class MyToDoList extends React.Component {
  constructor(props) {
    super(props);
    // here
    this.state = {
      userInput: '',
      toDoList: []
    }
    this.handleSubmit = this.handleSubmit.bind(this);
    this.handleChange = this.handleChange.bind(this);
  }
  handleSubmit() {
    const itemsArray = this.state.userInput.split(',');
    this.setState({
      toDoList: itemsArray
    });
  }
  handleChange(e) {
    this.setState({
      userInput: e.target.value
    });
  }
  render() {
    // here, must include the unique key
    const items = this.state.toDoList.map(i => <li key={i+1}>{i}</li>); 
    return (
      <div>
        <textarea
          onChange={this.handleChange}
          value={this.state.userInput}
          style={textAreaStyles}
          placeholder="Separate Items With Commas" /><br />
        <button onClick={this.handleSubmit}>Create List</button>
        <h1>My "To Do" List:</h1>
        <ul>
          {items}
        </ul>
      </div>
    );
  }
};
```
---
## Sibling Elements Need a Unique Key Attribute
React uses these keys to keep track of which items are added, changed, or removed.  

```javascript
const frontEndFrameworks = [
  'React',
  'Angular',
  'Ember',
  'Knockout',
  'Backbone',
  'Vue'
];

function Frameworks() {
  // Here, must include the unique key
  const renderFrameworks = frontEndFrameworks.map((i) => <li key={i+1}>{i}</li>)
  return (
    <div>
      <h1>Popular Front End JavaScript Frameworks</h1>
      <ul>
        {renderFrameworks}
      </ul>
    </div>
  );
};
```
---
## Use Array.filter() to Dynamically Filter an Array
Filter the contents of an array based on a condition, then returns a new array. 
```javascript
class MyComponent extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      users: [
        {
          username: 'Jeff',
          online: true
        },
        {
          username: 'Alan',
          online: false
        },
        {
          username: 'Mary',
          online: true
        },
        {
          username: 'Jim',
          online: false
        },
        {
          username: 'Sara',
          online: true
        },
        {
          username: 'Laura',
          online: true
        }
      ]
    };
  }
  render() {
    // filter to return a new array containing only the users whose online property is true
    const usersOnline = this.state.users.filter((u) => {
      return u.online == true
    })
    // map over the filtered array and return a li element with usernames
    const renderOnline = usersOnline.map((u) => {
      return <li key={u.username+1}>{u.username}</li>
    })

    return (
      <div>
        <h1>Current Online Users:</h1>
        <ul>{renderOnline}</ul>
      </div>
    );
  }
}
```
## Render React on the Server with renderToString
renderToString:  
There are two key reasons why rendering on the server may be used in a real world app.  
* First, without doing this, your React apps would consist of a relatively empty HTML file and a large bundle of JavaScript when it's initially loaded to the browser.
* Second, this creates a faster initial page load experience because the rendered HTML is smaller than the JavaScript code of the entire app.  

```javascript
class App extends React.Component {
  constructor(props) {
    super(props);
  }
  render() {
    return <div/>
  }
};

ReactDOMServer.renderToString(< App />)
```