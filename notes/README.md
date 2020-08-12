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

# Basic Features

## create react app

```sh
$ create-react-app <name of proj>
$ cd <name of proj> 
$ npm start
```

## folder structure

in the project folder we have package.json

```json
{
  "name": "react-complete-guide",
  "version": "0.1.0",
  "private": true,
  "dependencies": {
    "react": "^16.13.1",
    "react-dom": "^16.13.1",
    "react-scripts": "1.1.5"
  },
  "scripts": {
    "start": "react-scripts start",
    "build": "react-scripts build",
    "test": "react-scripts test --env=jsdom",
    "eject": "react-scripts eject"
  }


```

node modules folder has all the dependencies and subdependencies 
and is generated automatically via nmp install in your project folder


we also get a index.html in the public folder which gives us the defualy index
html page


in the src folder there is the index.js and the app.js, which has the default react component


## react component basics

app.js

```jsx
import React, { component } from 'react'
import './App.css';
class App extends Component {
    render() {
        (
        <div className="App">
            <h1> Hi! </h1>
        </div>
        );
    }
}

export default App
```

index.js

```jsx

ReactDOM.render(<App />, document.getElementById('root'));

```
all components must have render to render html


## understanding jsx

jsx is syntatic sugar for js when using the React library

we can use react.CreateElement for pure js to create the html instead of Render

app.js

```jsx
import React, { component } from 'react'
import './App.css';
class App extends Component {
    return React.CreateElement('div',{className: 'App'}, React.createElement('h1', null,'Hi!'));
}

```

but obviously jsx looks better and is more easibly readable than pure js 


## JSX restriction

* jsx expression must have one root element
* we cant use the term class in html in jsx because class is 
already a reserved in js


## Creating a Functional Component 

*simplest form: a component returns html

Person.js
```jsx

function person {
    return <h2>
}

//es6

const person = () => {
    return <p> Im a person </p>
}


export default person

```

in App.js

```jsx
import Person from './Person' //make sure to use capital to not intefere with native keywords in jsx


class App extends Component {
     render() {
        (
        <div className="App">
            <Person/>
        </div>
        );
     }
}

```

When creating components there is two different ways:

* functional components 

we have a function like 

```jsx

const cmp = () => {return <div> whatever </div> }
```

* class based component 

```jsx

class cmp extends Component {
    render <div> whatever </div>
}
```

## Outputting Dynamic Components

want to put some js into the rendered html

```jsx
import React from 'react';

const person = () => {
    return <p> Yo, I'm {Math.floor(Math.random())} years old! </p>
};
```

## Working With Props

now how do we make our Components take parameters?


```jsx

import React from 'react';

const person = (props) => {
    //theoretically we dont need to call the paramters props, but makes it readable 
    return <p> Yo, I'm {props.name} and {props.years} years old! </p>
};

export default person;
```

how do we call it:


Person.js
```jsx
import Person from './Person
    <Person name="Max" age="26"> whatever text </Person>
```


## Understanding the "Children" Prop

Person.js

```jsx

import React from 'react';

const person = (props) => {
    //theoretically we dont need to call the paramters props, but makes it readable 
    return (
        <p> Yo, I'm {props.name} and {props.years} years old! </p>
        <p> {props.children} </p> //children is a reserved word in jsx
    )
};

export default person;
```

App.js

```jsx
<Person name = "Max" age="26"> Put Children here, could be another component can be html or straight up text </Person>

```

## Understanding State


* state : can only be done in component class and is a keyword in react

```jsx
class App extends Component {
    state = {
            persons: [
                {name: 'Max', age: 28},
                {name: 'Step', age: 26}
            ]

        }
        //should be used consertively 

    render() {
        (
            <Person name={this.state.persons[0].name} age={this.state.persons[0].age}> whatever </Person>
        )
    }
}
```

states can be changed, and if it changes it would make react re-render your dom

## props and states

props allows a parent component to pass to a child component


state is used to hange the component from within, and changes
to state triggers ui update


```jsx
//... in class component
switchNameHandler = () => {
    console.log("button was clicked")
}
render() {
    <button onClick={}>Switch Name</button>
}
```

there are also other event names besides onClick:

onChange, onInput, onInvalid, onSubmit

## manipulating state

```jsx
//... in class component
state = {
            persons: [
                {name: 'Max', age: 28},
                {name: 'Step', age: 26}
            ]

        }
        
switchNameHandler = () => {
        //DONT DO THIS: this.state.persons[0].name = 'Maxy';
        this.setState({persons: 
                {name: 'Max', age: 235},
                {name: 'Step', age: 245}
            ]
        });
    }
render() {
    <button onClick={this.switchHandler}>Switch Name</button>
     <Person name={this.state.persons[0].name} age={this.state.persons[0].age}> whatever </Person>
}
```

now when state changes the persons array changes and the props changes in Person
and will rerender

* remember when make function Components capitalize name of function for 
good practice