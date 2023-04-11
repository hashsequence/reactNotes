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
    * The children, in React, refer to the generic box whose contents are unknown until they're passed from the parent component. What does this mean? It simply means that the component will display whatever is included in between the opening and closing tags while invoking the component.

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

## 41. A Closer Look At JSX

```jsx
    return (
        <div>
        <h2>Let's get started! M/h2>
        <Expenses items={expenses}/>
        </div>
    )
```

* In the past every component js file need a 
```jsx
import React from 'react'
```

* we can replace the above code with 
```jsx
//argumments, tag, attributes, content between opening and closing tags
    return React.createElement('div', {}, 
    React.createElement('h2',{}, 'Let\'s get started'),
    React.createElement(Expenses, {items: expenses}));
```

* we need to always return one thing so thats why we have a div wrapper

## 42. Organizing Component Files

* we can organize components into subfolders, but we need to use relative paths eg. (../subfolder/sourceFile)

## 43. An Alternative Function syntax

* we can use arrow functions

```js
const App = () => {
    //whatever the contents are
}
```

# Section 4: React State & Working With Events

## 46. Listening to Events & Working with Event Handlers

* button 

* In this example when we click the button, we have an event handler via the clickHandler function we implement

* by convention it is recommened to name handler functions with Handler suffix

```jsx
const ExpenseItem = (props) => {
  // function clickHandler() {}
  const [title, setTitle] = useState(props.title);
  console.log('ExpenseItem evaluated by React');
  
  const clickHandler = () => {
    setTitle('Updated!');
    console.log(title);
  };

  return (
    <Card className='expense-item'>
      <ExpenseDate date={props.date} />
      <div className='expense-item__description'>
        <h2>{title}</h2>
        <div className='expense-item__price'>${props.amount}</div>
      </div>
      <button onClick={clickHandler}>Change Title</button>
    </Card>
  );
}
```

## 47. How Component Functions Are Executed

* react components are only created once so we need state

## 48. Working with "State"

* for reevaluation at runtime we use state
* for example if we want to change title on the button

```jsx
const [title, setTitle] = useState(props.title);
```

* the useState function takes the variable and creates a hook to title

* the setTitle method can be used to change the state of title, and the component will update

```jsx
const ExpenseItem = (props) => {
  // function clickHandler() {}
  const [title, setTitle] = useState(props.title);
  console.log('ExpenseItem evaluated by React');
  
  const clickHandler = () => {
    setTitle('Updated!');
    //no in this console log, the title will be the old one because reacts scheules the change to the component and is not immediate
    console.log(title);
  };

  return (
    <Card className='expense-item'>
      <ExpenseDate date={props.date} />
      <div className='expense-item__description'>
        <h2>{title}</h2>
        <div className='expense-item__price'>${props.amount}</div>
      </div>
      <button onClick={clickHandler}>Change Title</button>
    </Card>
  );
}

```

## 49. A Closer Look at the "useState" Hook

* why are we using const here

```jsx
 const [title, setTitle] = useState(props.title);
 ```

 * we are not technically reassigning it, the useState 
 tells react that it will be handled somewhere else

 ## 51. Adding Form Inputs

 * lets make a NewExpense Component

* NewExpense.js
```jsx
import React from 'react'

import './NewExpense.css;

const NewExpense = () => {
  return <div className="new-expense">

  </div>
};

export default NewExpense
```

* ExpenseForm.js

```jsx
import React from 'react'

const ExpenseForm = () => {
  return <form>
    <div className='new-expense__controls'>
      <div className='new-expense__control'>
        <label>Title</label>
        <input type='text' />
      </div>
      <div className='new-expense__control'>
            <label>Date</label>
            <input
              type='date'
              min='2019-01-01'
              max='2022-12-31'
            />
        </div>
      </div>
      <div className='new-expense__actions'>
        <button type='submit'>Add Expense</button>
      </div>
  </form>
}
```

## 52. Listening to User Input

* We need to add listeners
* we can acesss the target.value from the input
```jsx
const ExpenseForm = () => {
  const [enteredTitle, setEnteredTitle] = useState('');
  const [enteredAmount, setEnteredAmount] = useState('');
  const [enteredDate, setEnteredDate] = useState('');

  const titleChangeHandler = (event) => {
    setEnteredTitle(event.target.value);
  };

  const amountChangeHandler = (event) => {
    setEnteredAmount(event.target.value);
  };

  const dateChangeHandler = (event) => {
    setEnteredDate(event.target.value);
  };

  return (
    <form>
      <div className='new-expense__controls'>
        <div className='new-expense__control'>
          <label>Title</label>
          <input type='text' onChange={titleChangeHandler} />
        </div>
        <div className='new-expense__control'>
          <label>Amount</label>
          <input
            type='number'
            min='0.01'
            step='0.01'
            onChange={amountChangeHandler}
          />
        </div>
        <div className='new-expense__control'>
          <label>Date</label>
          <input
            type='date'
            min='2019-01-01'
            max='2022-12-31'
            onChange={dateChangeHandler}
          />
        </div>
      </div>
      <div className='new-expense__actions'>
        <button type='submit'>Add Expense</button>
      </div>
    </form>
  );
};
```

## 53. Working with Multiple States

```jsx
  const [enteredTitle, setEnteredTitle] = useState('');
  const [enteredAmount, setEnteredAmount] = useState('');
  const [enteredDate, setEnteredDate] = useState('');

  const titleChangeHandler = (event) => {
    setEnteredTitle(event.target.value);
  };

  const amountChangeHandler = (event) => {
    setEnteredAmount(event.target.value);
  };

  const dateChangeHandler = (event) => {
    setEnteredDate(event.target.value);
  };
```

## 54. Using One State Instead (And What's Better)

```jsx

const ExpenseForm = () => {
  /*
  //instead of this 
  const [enteredTitle, setEnteredTitle] = useState('');
  const [enteredAmount, setEnteredAmount] = useState('');
  const [enteredDate, setEnteredDate] = useState('');
  */
 // we do this
  const [userInput, setUserInput] = useState({
    enteredTitle,
    enteredAmount,
    enteredDate
  })
}
```

* the cons of this that we when we replace an object with another one it will replace the other one so basically you need to do 

```jsx
setUserInput({
  ...userInput,
  //new stuff...
});
```

## 55. Updating State that depends on previous state

* basically this

```jsx
setUserInput((prev) =>{
  return {
  ...prev,
  //new stuff...
  }
})

```

* onChange with useState example
```jsx
import React, {useState} from 'react';

import './styles.css';

// don't change the Component name "App"
export default function App() {
    
    const [isValid, setIsValid] = useState({message: <p>"Invalid message"</p>});
    
    const validFunc = (e) => {
        if (typeof e.target.value === 'undefined' || e.target.value.length < 3) {
            setIsValid({
                message: <p>"Invalid message"</p>
            });
        }
        setIsValid({
            message:  <p>"Valid message"</p>
        });
    }
    
    return (
        <form>
            <label>Your message</label>
            <input type="text" onChange={validFunc}/>
            {isValid.message}
        </form>
    );
}
```
* onClick with useState with prev example
```jsx
import React, {useState} from 'react';

import './styles.css';

// don't change the Component name "App"
export default function App() {
    const [count, inc] = useState(0);
    const increment = (e) => {
        inc((prev) => {
            return prev + 1;
        });
    }
    return (
      <div>
        <p id="counter">{count}</p>
        <button onClick={increment}></button>
      </div>
    );
}

```

## 56 Handling Form Submission

* onSubmit
* event.preventDefault();
  * used because onSubmit because it will automatically send a request to the server hosting the page

```jsx

const handleSubmit = (e) => {
  e.preventDefault();
  //DO STUFF....
}
<form onSubmit={handleSubmit}></form>
```

## 57 Handling Two-Way Binding

* for inputs we just don't listen to inputs we also set inputs

```jsx
const submitHandler = (e) => {
  e.preventDefault();
  titleChangedHandler({
    enteredTitle : "something"
  })
}
<form onSubmit={submitHandler}>
  <input type="text" value={enteredTitle} onChange={titleChangedHandler}></input>
</form>
```

* now when we press submit we can submit the values and clear the inputs
* two-way binding is useful in forms because we gather user input and then change it

## 58 Child-to-Parent Component Communication (Bottom-up)

```jsx
const ChildComponent = (props) => {

  const doSomething = () => {
    props.parentSetterFunc({
      //...something new
    })
  }
  return <div></div>
}
const ParentComponent = () => {
  const [parentState, setParentState] => useState({
    //...something
  })

  return (
    <ChildComponent parentSetterFunc={setParentState}/>
  )
}

```

## 59. Lifting The State Up

* how sibling components can communicate to each other
  * tldr: have parent pass a useState method to both child and children can communicate setting the state of parent useState

```jsx
const ChildComponent = (props) => {

  const doSomething = () => {
    props.parentSetterFunc({
      //...something new
    })
  }
  return <div></div>
}
const ChildComponentTwo = (props) => {

  const doSomething = () => {
    props.parentSetterFunc({
      //...something new
    })
  }
  return <div></div>
}

const ParentComponent = () => {
   const [parentState, setParentState] => useState({
    //...something
  })

  eturn (
    <ChildComponent parentSetterFunc={setParentState}/>
    <ChildComponentTwo parentState={parentState}/>
  )
}
```

## 60. Controlled vs Uncontrolled Components  & Stateless vs Stateful Components

* Controlled Components - parent components handles states and setterStates

* unControlled Components - not controlled by parent

* stateful components manages state

* stateless components doesn't have internal state, just there to output data


## 63. Rendering Lists of Data

```jsx
const Item = (props) => {
  return <p>{props.children}</p>
}

<ListComponent items={[/*List of stuff*/]}/>
const ListComponent = (props) => {
  return {props.items.map((someStringSample) => {
    <Item>{someStringSample}</Item>
  })}
}
```

* Rendering List of data Example:
  * App.js
  ```jsx

  import React from 'react';

  import Todo from './Todo';
  import './styles.css';

  const DUMMY_TODOS = [
      'Learn React',
      'Practice React',
      'Profit!'
  ];

  // don't change the Component name "App"
  export default function App() {
      return (
        //don't usually use index, because indices can remap when adding or deleting from list, have self made id's 
          DUMMY_TODOS.map((value, index) => {
              return <Todo key={index} text={value}></Todo>
          })
      );
  }


  ```
  * Todo.js
  ```jsx
  import React from 'react';

  export default function Todo(props) {
      return <li>{props.text}</li>;
  }
  ```

  ## 64. Using Stateful Lists

  ```jsx

  INIT_expenses = [/*list of expense objects*/]

  const App = () => {
    const [expense, setExpenses] = useState(INIT_expenses)
    const addExpenseHandler = (prev) => {
      return [expense, ...prev]
    }
  /*
  Note:
  //These two are equivalent
    function App1() {
      return <Greeting firstName="Ben" lastName="Hector" />;
    }

    function App2() {
      const props = {firstName: 'Ben', lastName: 'Hector'};
      return <Greeting {...props} />;
    }
  */
    return (
      <div>
        {props.items.map((expenses) => {
          <ExpenseItem
            {...expenses}
          />
        })}
      </div>
    )
  }

  ```

  ## 65. Understanding "Keys"

  * React have a special concept when rendering a list of data
  * if you don't pass key when rendering a list and add a new item to list then it will rerender the entire list instead of just rendering that new item added
  * you can use an id of the list of objects or something like that
  * always add key when mapping list, just to make sure you don't run against the problem listed above

## 66. Outputing Conditional Content

* we can use javascript ternary expression syntax 
```js
condition ? a : b
```

* we can also do this 

```jsx
condition && <Component {...props}/>
```
* javascript will return value of last term in expression

* if you don't want to inline the conditions in return, then write the logic before the return in the function component like 

```jsx
let value = "default"
if(condition) {
  value = "something"
} else {
  value = "somethingelse"
}

return (
  <div>
    {value}
  </div>
)
```