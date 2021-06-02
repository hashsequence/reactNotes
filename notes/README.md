# Refreshing Modern es6 Javascript

## Let And Const


use let to replace to var
const is constant

```js
function myFnc() {


}

const myFnc = () => {

}


```

this in an arrow function it will always keep its context

this in function it refers to the function itself 


## Export & Imports (Modules)


* person.js
```js
const person = {
    name : 'Max'
}

export defualt person
```

* utility.js
```js
export const clean = () => {...}
export const baseData = 10
```

* app.js

```js
    import person from './person.js'
    import prs from './person.js'

    import { baseData } from './utlity.js'
    import { clean } from './utility.js'
```

default export 

```js
import {smth} from './utility.js'
import {smith as smth} from './utility.js'
import * as bundled from './utility.js'
```

## Classes

```js
class Person {
    name = 'max'
    call = {} => {...}
}

const myPerson = new Person{}
myPerson.call()
console.log(myPerson.name)

//inheritance 
class Person extends Master
```


example:

```js
class Human {
    consstructor() {
        this.gender = 'male'
    }

    printGender() {
        console.log(this.gender);
    }
}
class Person extends Human { //needs extends to inherit
    constructor() {
        super(); //need this to inherit
        this.name = 'Max'

    }

    PrintMyName() {
        console.log(this.name);
    }
}

const person = new Person();
person.printMyName();
person.printGender();

```

```js
//es6
constructor() {
    this.myProperty = 'value'
}

myMethod() {
    ...
}

//es7

myProperty = 'value'

myMethod = () => {...}
```

## spread & rest operators ...


* spread - used to split up array lements or object properties
```js
const newArray = [...oldArray, 1, 2] 
const newObject = {...oldObject, newProp:5}
```

*rest - used to merge a list of function arguments into an array
```js
function sortArgs(...args) {
    return args.sort()
}
```

## destructuring 

* extract array elements or object properties and store them in variables 
* different from rest since you can extranct single elements

```js
[a,b] = ['Hello','Max']
console.log(a) //hello

{name} = {name : 'Max', age : 28}

console.log(name) //Max
conosole.log(age) //undefined 

```

## reference and primitive types refresher

```js
const number = 1; //this is a primitive
const num2 = number; //copies the value of number

const person = {
    name: 'Max'
}

const secondPerson = person; //this is a reference, creates a pointer to person

const thirdPerson = {
    ...person //using spread operator spreads the properties and thirdPerson is own object
}
```


## basic array functions 

google them but here is an example of map
```js
const numbers = [1,2,3];
const doubNumArray = numbers.map((num) => {
    return num * 2;
}); //[2, 4, 6]
```

* filter, reduce, findIndex, concat, slice, splice are some other ones

# Section 3: React Basics & Working With Components

## 25. What Are Components? And Why Is React All About Them?

* all user interfaces are made of components

* what are components?
    * components are combination is a combination of css, html, and javascript

* why components?
    * reusability 
    * seperation of concerns
    * done repeat yourself
    * dont do too many things in one and the same place (function)

## 26. React Code Is Written In A "Declarative Way"!

* React uses a declarative approach meaning with that we define the desired target states
and let react figure out the actual javascript DOM instructions

## 27. Creating a new React Project

* we need to download node for npm and npx: https://nodejs.org/en/

*creating react skeleton app
```js
npx create-react-app my-app
cd my-app
npm start
```

* this installs the node modules
```js
npm install
```

## 29. Analyzing a Standard React Project

* index.js:
```jsx
import React from 'react';
import ReactDOM from 'react-dom';
import './index.css';
import App from './App';

//render element takes in too arguments
//second argument is the default javascript api 
//the first argument is a html tag
ReactDOM.render(
  <React.StrictMode>
    <App />
  </React.StrictMode>,
  document.getElementById('root')
);

```
* the render will render the App / in place of the root
```html
    <noscript>You need to enable JavaScript to run this app.</noscript>
    <div id="root"></div>
```

* App.js:

```jsx
import ExpenseItem from './components/ExpenseItem';

function App() {
  return (
    <div>
      <h2>Let's get started!</h2>
      <ExpenseItem></ExpenseItem>
    </div>
  );
}

export default App;

```

## 30. Introducing JSX

* App.js:
    * basic App component 
```jsx

function App() {
  return (
    <div>
      <h2>Let's get started!</h2>
    </div>
  );
}

export default App;

```
## 31. Introducing JSX

* App.js
    * will add another tag and it will show up
```jsx

function App() {
    /*
    this is the pure javascript version of the below jsx
    const para = doument.createElement('p');
    para.textContenet = "this is visible";
    document.getElementBID('root').append(para);
    */
  return (
    <div>
      <h2>Let's get started!</h2>
      <p>This is also visible</p>
    </div>
  );
}

export default App;

```

## 32. Building a First Custom Component

