## Create a Simple JSX Element
React uses a syntax extension of JavaScript called JSX that allows you to write HTML directly within JavaScript. Write JavaScript directly in JSX with curly braces:

`const JSX = <h1>{'This text will be outputted'}</h1>;`

---
## Create a Complex JSX Element
Nested JSX must return a single element. 

```
<div>
  <p>This</p>
  <p>Works</p>
</div>


 <p>This</p>
 <p>Does not work</p>
 ```

---
## Add Comments in JSX

```
const JSX = (
  <div>
    <h1>This is a block of JSX</h1>
    {/* Comment out like this */}
  </div>
);
```

---
## Render HTML Elements to the DOM
Render this JSX directly to the HTML DOM using React's rendering API known as ReactDOM.

```
const componentToRender = (
  <div>
    <h1>Hello World</h1>
    <p>Lets render this to the DOM</p>
  </div>
);
let targetNodeToRenderTo = document.getElementById('challenge-node') 
ReactDOM.render(componentToRender, targetNodeToRenderTo)
```
The first argument is the React element or component that you want to render, and the second argument is the DOM node that you want to render the component to.

---
## Define an HTML Class in JSX
Class is a reserved word in JavaScript so it won't work with JSX. Otherwise everything is in camelCase
use `className=` instead of `class=`
use `onClick=` instead of `onclick`
use `onChange=` instead of `onchange`

```
const JSX = (
  <div className="myDiv">
    <h1>Add a class to this div</h1>
  </div>
);
```

---
## Self-Closing JSX Tags
```const JSX = (
  <div>
    <h2>See the self closing br</h2> <br />
  </div>
  <div />
);
```

---
## Stateless Functional Component
Everything in React is a component. *Create component with a function.* Component must be capitalized.

```
const MyComponent = function() { 
  return ( 
  <div>
    'string'
  </div>
  )
}
```

---
## Class Component
Everything in React is a component. *Create component with class syntax.* Component must be capitalized.

This creates an ES6 class MyComponent which extends the React.Component class. So the MyComponent class now has access to many useful React features, such as local state and lifecycle hooks. 

Also notice the MyComponent class has a constructor defined within it that calls super(). It uses super() to call the constructor of the parent class, in this case React.Component. The constructor is a special method used during the initialization of objects that are created with the class keyword. It is best practice to call a component's constructor with super, and pass props to both. This makes sure the component is initialized properly.

```
class MyComponent extends React.Component {
  constructor(props) {
    super(props);
  }
  render() {
    return (
      <div>
        <h1>
          Hello React!
        </h1>
      </div>
    )
  }
};
```
---
## Create a Component with Composition
Compose multiple React components together. Pass in the child component with `<CustomTag />` syntax
```
const ChildComponent = () => {
  return (
    <div>
      <p>I am the child</p>
    </div>
  );
};

class ParentComponent extends React.Component {
  constructor(props) {
    super(props);
  }
  render() {
    return (
      <div>
        <h1>I am the parent</h1>
        <ChildComponent />
      </div>
    );
  }
};
```
---
## Render a Class Component to the DOM
ReactDOM.render(componentToRender, targetNode). The first argument is the React component that you want to render. The second argument is the DOM node that you want to render that component within.

```
class TypesOfFood extends React.Component {
  constructor(props) {
    super(props);
  }
  render() {
    return (
      <div>
        <h1>Types of Food:</h1>
        <Fruits />
        <Vegetables />
      </div>
    );
  }
};
ReactDOM.render(<TypesOfFood/>, document.getElementById('challenge-node'))
```
