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

* in react you build a component tree
    * so you have <App /> then under that you have other components like <Header /> or <task />

* for example lets make an ExpenseItem

* ExpenseItem.js:

```jsx

function ExpenseItem() {
  return (
    <div>
      <div>March 28th 2021</div>
      <div>
        <h2>Car Insurance</h2>
        <div>$294.67</div>
      </div>
    </div>
  );
}

export default ExpenseItem;

```

* now that we made the component lets incorporate it into the app:

* App.js:

```jsx
// the ExpenseItem.js is int the components folder
/*
working folder tree:
C:.
▒   App.js
▒   index.css
▒   index.js
▒
▒▒▒▒components
        ExpenseItem.js

*/
import ExpenseItem from './components/ExpenseItem';

function App() {
  return (
    <div>
      <h2>Let's get started! changed by avery
      </h2>
      <ExpenseItem></ExpenseItem>
    </div>
  );
}

export default App;

```

## 33. Writing More Complex JSX Code

* modifying ExpenseItem so that a different number appears everytime the page reloads:

```jsx

const RandomMoney = () => {
    return (Math.random() * 1000).toLocaleString(
                undefined, // leave undefined to use the visitor's browser 
                            // locale or a string like 'en-US' to override it.
                { minimumFractionDigits: 2 })
}

function ExpenseItem() {
  return (
    <div>
      <div>March 28th 2021</div>
      <div>
        <h2>Car Insurance</h2>
        <div>${RandomMoney()}</div>
      </div>
    </div>
  );
}

export default ExpenseItem;
```

## 34. Adding Basic CSS Styling

 * make a css file called ExpenseItem.css
    * C:.
        ▒   App.js
        ▒   index.css
        ▒   index.js
        ▒
        ▒▒▒▒components
                ExpenseItem.css
                ExpenseItem.js



```css
.expense-item {
    display: flex;
    justify-content: space-between;
    align-items: center;
    box-shadow: 0 2px 8px rgba(0, 0, 0, 0.25);
    padding: 0.5rem;
    margin: 1rem 0;
    border-radius: 12px;
    background-color: #6F01FE;
  }
  
  .expense-item__description {
    display: flex;
    flex-direction: column;
    gap: 1rem;
    align-items: flex-end;
    flex-flow: column-reverse;
    justify-content: flex-start;
    flex: 1;
  }
  
  .expense-item h2 {
    color: #3a3a3a;
    font-size: 1rem;
    flex: 1;
    margin: 0 1rem;
    color: white;
  }
  
  .expense-item__price {
    font-size: 1rem;
    font-weight: bold;
    color: white;
    background-color: #40005d;
    border: 1px solid white;
    padding: 0.5rem;
    border-radius: 12px;
  }
  
  @media (min-width: 580px) {
    .expense-item__description {
      flex-direction: row;
      align-items: center;
      justify-content: flex-start;
      flex: 1;
    }
  
    .expense-item__description h2 {
      font-size: 1.25rem;
    }
  
    .expense-item__price {
      font-size: 1.25rem;
      padding: 0.5rem 1.5rem;
    }
  }
```

now add the className to the ExpenseItem.js:

```jsx
//class is a protected word in jsx so use ClassName
//Note: . is Class and # is id in css selectors
function ExpenseItem() {
  return (
    <div className="expense-item">
      <div>March 28th 2021</div>
      <div>
        <h2>Car Insurance Random</h2>
         <div className="expense-item__price">${RandomMoney()}</div>
      </div>
    </div>
  );
}
```

## 35. Outputting Dynamic Data & Working with Expressions in JSX

* using variables expressions in ExpenseItem.js:

```jsx

import './ExpenseItem.css';
const RandomMoney = () => {
    return (Math.random() * 1000).toLocaleString(
                undefined, // leave undefined to use the visitor's browser 
                            // locale or a string like 'en-US' to override it.
                { minimumFractionDigits: 2 })
}

function ExpenseItem() {

    const expenseDate = new Date(2021, 2, 28);
    const expenseTitle = 'Car Insurance';
    const expenseAmount = RandomMoney();

  return (
    <div className="expense-item">
      <div>{expenseDate.toISOString()}</div>
      <div>
        <h2>{expenseTitle}</h2>
         <div className="expense-item__price">First Way: ${RandomMoney()}</div>
         <div className="expense-item__price">Second Way: ${expenseAmount}</div>
      </div>
    </div>
  );
}

export default ExpenseItem;

```

## 36. Passing Data via "props"

* what if we have different expenses and we want to pass these as parameters to the ExpenseItem Component

* App.js:
```jsx
import ExpenseItem from './components/ExpenseItem';

function App() {

    const expenses = [
        {
            id: 'e1',
            title: 'Toilet Paper',
            amount: 94.12,
            date: new Date(2020, 7, 14),
        },
        {
            id: 'e2',
            title: 'tissues',
            amount: 1093.62,
            date: new Date(2020, 9, 9),
        },
        {
            id: 'e2',
            title: 'groceries',
            amount: 10910.62,
            date: new Date(2020, 10, 9),
        },
    ];
    //parameters are like attributes to component tag
  return (
      <div>
        <h2>Let's get started! changed by avery
        </h2>
        <ExpenseItem
          title={expenses[0].title}
          amount={expenses[0].amount}
          date={expenses[0].date}
        ></ExpenseItem>
        <ExpenseItem
          title={expenses[1].title}
          amount={expenses[1].amount}
          date={expenses[1].date}
        ></ExpenseItem>
        <ExpenseItem
          title={expenses[2].title}
          amount={expenses[2].amount}
          date={expenses[2].date}
        ></ExpenseItem>
      </div>
    );
}

export default App;

```
* ExpenseItem.js

```jsx

import './ExpenseItem.css';
const RandomMoney = () => {
    return (Math.random() * 1000).toLocaleString(
                undefined, // leave undefined to use the visitor's browser 
                            // locale or a string like 'en-US' to override it.
                { minimumFractionDigits: 2 })
}

//parameters is passed as an object, props doesn't have to be props, but to be consistent lets just use props
function ExpenseItem(props) {

    const expenseDate = props.date;
    const expenseTitle = props.title;
    const expenseAmount = props.amount;

  return (
    <div className="expense-item">
      <div>{expenseDate.toISOString()}</div>
      <div>
        <h2>{expenseTitle}</h2>
         <div className="expense-item__price">First Way: ${RandomMoney()}</div>
         <div className="expense-item__price">Second Way: ${expenseAmount}</div>
      </div>
    </div>
  );
}

export default ExpenseItem;

```

## 37. Adding "normal" JavaScript Logic to Components

* we are just going to format the date using javascript functions

* ExpenseItem.js

```jsx

import './ExpenseItem.css';
const RandomMoney = () => {
    return (Math.random() * 1000).toLocaleString(
                undefined, // leave undefined to use the visitor's browser 
                            // locale or a string like 'en-US' to override it.
                { minimumFractionDigits: 2 })
}

function ExpenseItem(props) {

    const month = props.date.toLocaleString('en-US', { month : 'long' });
    const day = props.date.toLocaleString('en-US', { day : '2-digit' });
    const year = props.date.getFullYear();

    const expenseTitle = props.title;
    const expenseAmount = props.amount;

  return (
    <div className="expense-item">
      <div>
        <div>{month} {day}, {year}</div>
      </div>
      <div>
        <h2>{expenseTitle}</h2>
         <div className="expense-item__price">First Way: ${RandomMoney()}</div>
         <div className="expense-item__price">Second Way: ${expenseAmount}</div>
      </div>
    </div>
  );
}

```
## 38. Splitting Components Into Multiple Components

* Lets split out the ExpenseDate From ExpenseItem to its own component

* ExpenseData.js

```jsx
function ExpenseDate(props) {
    const month = props.date.toLocaleString('en-US', { month : 'long' });
    const day = props.date.toLocaleString('en-US', { day : '2-digit' });
    const year = props.date.getFullYear();

    return  <div>{month} {day}, {year}</div>
}

export default ExpenseDate
```

* ExpenseItem.js

```jsx

import './ExpenseItem.css';
//importing new ExpenseDate Component
import ExpenseDate from  './ExpenseDate';
const RandomMoney = () => {
    return (Math.random() * 1000).toLocaleString(
                undefined, // leave undefined to use the visitor's browser 
                            // locale or a string like 'en-US' to override it.
                { minimumFractionDigits: 2 })
}

function ExpenseItem(props) {

  const month = props.date.toLocaleString('en-US', { month : 'long' });
  const day = props.date.toLocaleString('en-US', { day : '2-digit' });
  const year = props.date.getFullYear();

  const expenseTitle = props.title;
  const expenseAmount = props.amount;

//using ExpenseDate now
return (
  <div className="expense-item">
  //using 
   <ExpenseDate date={props.date}></ExpenseDate>
    <div>
      <h2>{expenseTitle}</h2>
       <div className="expense-item__price">First Way: ${RandomMoney()}</div>
       <div className="expense-item__price">Second Way: ${expenseAmount}</div>
    </div>
  </div>
);
}
export default ExpenseItem;

```

* now adding css

* ExpenseDate.css

```css
.expense-item {
    display: flex;
    justify-content: space-between;
    align-items: center;
    box-shadow: 0 2px 8px rgba(0, 0, 0, 0.25);
    padding: 0.5rem;
    margin: 1rem 0;
    border-radius: 12px;
    background-color: #6F01FE;
  }
  
  .expense-item__description {
    display: flex;
    flex-direction: column;
    gap: 1rem;
    align-items: flex-end;
    flex-flow: column-reverse;
    justify-content: flex-start;
    flex: 1;
  }
  
  .expense-item h2 {
    color: #3a3a3a;
    font-size: 1rem;
    flex: 1;
    margin: 0 1rem;
    color: white;
  }
  
  .expense-item__price {
    font-size: 1rem;
    font-weight: bold;
    color: white;
    background-color: #40005d;
    border: 1px solid white;
    padding: 0.5rem;
    border-radius: 12px;
  }
  
  @media (min-width: 580px) {
    .expense-item__description {
      flex-direction: row;
      align-items: center;
      justify-content: flex-start;
      flex: 1;
    }
  
    .expense-item__description h2 {
      font-size: 1.25rem;
    }
  
    .expense-item__price {
      font-size: 1.25rem;
      padding: 0.5rem 1.5rem;
    }
  }
```

* ExpenseDate.js

```jsx

import './ExpenseDate.css';

function ExpenseDate(props) {
    const month = props.date.toLocaleString('en-US', { month : 'long' });
    const day = props.date.toLocaleString('en-US', { day : '2-digit' });
    const year = props.date.getFullYear();

    return  (
        <div className='expense-date'>
            <div className='expense-date__month'>{month}</div>
            <div className='expense-date__year'>{year}</div>
            <div className='expense-date__day'>{day}</div>
        </div>
    );
}

export default ExpenseDate

```

### Assignment 1: Time to Practice: React & Component Basics


* Expenses.CSS

```css
.expenses {
    padding: 1rem;
    background-color: rgb(31, 31, 31);
    margin: 2rem auto;
    width: 50rem;
    max-width: 95%;
    border-radius: 12px;
    box-shadow: 0 1px 8px rgba(0, 0, 0, 0.25);
  }
```

* Expenses.js
```jsx
import './Expenses.css'
import ExpenseItem from './ExpenseItem';

function Expenses(props) {
    let expenses = props.expenses;
    //dynamic way

    return (
        <div className="expenses">
            <h2>dynamic way!</h2>
            {
                expenses.map(item =>
                <ExpenseItem
                    title={item.title}
                    amount={item.amount}
                    date={item.date}
                ></ExpenseItem> 
            )
            }
        </div>
    )
    //static way
    /*
    return (
        <div className="expenses">
            <h2>static way!</h2>
            <ExpenseItem
                title={expenses[0].title}
                amount={expenses[0].amount}
                date={expenses[0].date}
            ></ExpenseItem>
            <ExpenseItem
                title={expenses[1].title}
                amount={expenses[1].amount}
                date={expenses[1].date}
            ></ExpenseItem>
            <ExpenseItem
                title={expenses[2].title}
                amount={expenses[2].amount}
                date={expenses[2].date}
            ></ExpenseItem>
        </div>
       )
       */
}

export default Expenses
```

* App.js

```jsx
import Expenses from './components/Expenses';

function App() {

    const expenses = [
        {
            id: 'e1',
            title: 'Toilet Paper',
            amount: 94.12,
            date: new Date(2020, 7, 14),
        },
        {
            id: 'e2',
            title: 'tissues',
            amount: 1093.62,
            date: new Date(2020, 9, 9),
        },
        {
            id: 'e3',
            title: 'groceries',
            amount: 10910.62,
            date: new Date(2020, 10, 9),
        },
        {
          id: 'e4',
          title: 'computer',
          amount: 1500.78,
          date: new Date(2020, 3, 9),
        },
    ];

    return (
      <div>
        <h2>Let's get started! changed by avery
        </h2>
        <Expenses
          expenses={expenses}
        >
        </Expenses>
      </div>
    );
}

export default App;
```

## 39. The Concept of "Composition" ("children props")


* props.children is a reserved word

* lets make a wrapper component card:

* I take out some stuff from Expenses.css and put it in card.css

* Card.css

```css
.card {
    border-radius: 12px;
    box-shadow: 0 1px 8px rgba(0, 0, 0, 0.25);
  }
```

* Card.js

```jsx
function Card(props) {
    const classes = 'card ' + props.className
    return <div className={classes}>{props.children}</div>
}

export default Card
```

* modify ExpenseItem.js to use Card
```jsx

import './ExpenseItem.css';
import ExpenseDate from  './ExpenseDate';
import Card from './Card'

const RandomMoney = () => {
    return (Math.random() * 1000).toLocaleString(
                undefined, // leave undefined to use the visitor's browser 
                            // locale or a string like 'en-US' to override it.
                { minimumFractionDigits: 2 })
}

function ExpenseItem(props) {

  const month = props.date.toLocaleString('en-US', { month : 'long' });
  const day = props.date.toLocaleString('en-US', { day : '2-digit' });
  const year = props.date.getFullYear();

  const expenseTitle = props.title;
  const expenseAmount = props.amount;

return (
  <Card className="expense-item">
   <ExpenseDate date={props.date}></ExpenseDate>
    <div>
      <h2>{expenseTitle}</h2>
       <div className="expense-item__price">First Way: ${RandomMoney()}</div>
       <div className="expense-item__price">Second Way: ${expenseAmount}</div>
    </div>
  </Card>
);
}
export default ExpenseItem;

```

* also modify Expense.js to use Card

```jsx
import './Expenses.css'
import ExpenseItem from './ExpenseItem';
import Card from './Card'
function Expenses(props) {
    let expenses = props.expenses;
    //dynamic way
    let output = (
        <div className="expenses">
            <h2>dynamic way!</h2>
            {
                expenses.map((item) => (
                
                <ExpenseItem
                    title={item.title}
                    amount={item.amount}
                    date={item.date}
                ></ExpenseItem> 
                )
            )
            }
        </div>
    )

    return (
        <Card className="expenses">
            <h2>dynamic way!</h2>
            {
                expenses.map((item) => (
                <ExpenseItem
                    title={item.title}
                    amount={item.amount}
                    date={item.date}
                ></ExpenseItem> 
                )
            )
            }
        </Card>
    )
    //static way
    /*
    return (
        <div className="Expenses">
            <h2>static way!</h2>
            <ExpenseItem
                title={expenses[0].title}
                amount={expenses[0].amount}
                date={expenses[0].date}
            ></ExpenseItem>
            <ExpenseItem
                title={expenses[1].title}
                amount={expenses[1].amount}
                date={expenses[1].date}
            ></ExpenseItem>
            <ExpenseItem
                title={expenses[2].title}
                amount={expenses[2].amount}
                date={expenses[2].date}
            ></ExpenseItem>
        </div>
       )
       */
}

export default Expenses
```