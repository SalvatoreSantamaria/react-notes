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

```const JSX = (
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