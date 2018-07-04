<img src="https://devmounta.in/img/logowhiteblue.png" width="250" align="right">

# Project Summary

This is a working project that currently only utilizes state and props to pass its data. Before getting started, try to get familiar with the code and see how props is being passed through to different components. In particular, take a look at `src/App.js`. You'll notice that `src/App.js` is currently very large. With the use of `redux`, we'll be able to turn `src/App.js` into a small, 27 line, file. 

During this project, we'll be improving on a web application that walks users through filling out a home loan application. We'll be modifying components that have already been built to use `redux`. This allows us to keep track of data and pass it to the correct components via routing. We'll be making changes to all files in the `src/components` folder, except for `src/components/Finish/Finish.js`, to modify them to work with `redux`. We'll also make changes to `src/router.js`, `src/index.js` and `src/App.js`.

# Live Example

<a href="https://devmountain.github.io/react-5-afternoon/">Click Me!</a>

## Setup

* `fork` and `clone` this repository.
* `cd` into the project directory.
* Run `npm i` to install current dependencies.
* Run `npm i react-redux redux react-router-dom`
* Run `npm start` ( The app should intentionally not compile correctly ).

## Step 1

### Summary

In this step, we will create our `store`. 
When using redux, the store holds the entire state of our application. So it's important we set this up first.

### Instructions

* Create a new file in your `src` folder called `store.js`
* Open `src/store.js`.
* Import `createStore` from `redux`.
* Import `reducer.js` from `src/ducks/reducer.js`.
* Export `createStore` by default and pass it reducer as it's argument

<details>

<summary> Detailed Instructions </summary>

<br />

In redux, components need to connect to a store. Let's create this store. Create a file in the `src` folder called `store.js`. We'll only be needing one thing from `redux`: `createStore`. `createStore` will allows us to export the creation of our store. 

```js
import { createStore } from "redux";
```

In order to create our store, we'll also need our reducer. So let's import that as well. Our reducer is located in `src/ducks`.

```js
import { createStore } from "redux";

import reducer from "./ducks/reducer";
```

Now that we have everything we need to import, let's export by default the creation of our store. 

```js
import { createStore } from "redux";

import reducer from "./ducks/reducer";

export default createStore( reducer );
```

</details>

### Solution

<details>

<summary> <code> src/store.js </code> </summary>

```js
import { createStore } from "redux";

import reducer from "./ducks/reducer";

export default createStore( reducer );
```

</details>

## Step 2

### Summary

In this step, we will take our store created from the previous step and hook it up in `src/index.js`. We will also make use of `HashRouter` to allow routing in the application. After this step, our app should compile correctly.

### Instructions

* Open `src/index.js`.
* Import `HashRouter` from `react-router-dom`.
* Wrap the `App` component in `<HashRouter>` tags.
* Import `Provider` from `react-redux`.
* Import `store` from `src/store.js`.
* Wrap the `HashRouter` component tags with the `Provider` component:
  * The `Provider` component should have a `store` prop that equals `store` (remember how we call variables in jsx). 

<details>

<summary> Detailed Instructions </summary>

<br />

Open `src/index.js`. Since we're using routing we'll be needing to import `HashRouter` from `react-router-dom` and wrap the `App` component.

```js
import React from 'react';
import ReactDOM from 'react-dom';
import App from './App';
import registerServiceWorker from './registerServiceWorker';
import './index.css';
import { HashRouter } from 'react-router-dom';

ReactDOM.render(
  <HashRouter>
    <App />
  </HashRouter>
, document.getElementById('root'));
registerServiceWorker();
```

Since our store has been created, we can hook it up to our App in `src/index.js`. This will allow our App to have access to the store and the reducers and will also allow our App to compile correctly. We'll need to import `Provider` from `react-redux` and `store` from `src/store.js`. 

```js
import store from './store'
import { Provider } from 'react-redux'
```

The `Provider` component will "provide" the store to our App. All we need to do is wrap the `HashRouter` component with the `Provider` component and give the `Proivder` component a `store` prop that equals `store`. 

```js
import React from 'react';
import ReactDOM from 'react-dom';
import App from './App';
import registerServiceWorker from './registerServiceWorker';
import './index.css';
import { HashRouter } from 'react-router-dom';
import { Provider } from 'react-redux'
import store from './store'

ReactDOM.render(
  <Provider store={store}>
    <HashRouter>
      <App />
    </HashRouter>
  </Provider>    
, document.getElementById('root'));
registerServiceWorker();
```

</details>

### Solution

<details>

<summary> <code> src/index.js </code> </summary>

```js
import React from 'react';
import ReactDOM from 'react-dom';
import App from './App';
import registerServiceWorker from './registerServiceWorker';
import './index.css';
import { HashRouter } from 'react-router-dom';
import { Provider } from 'react-redux';
import store from './store';

ReactDOM.render(
  <Provider store={store}>
    <HashRouter>
      <App />
    </HashRouter>
  </Provider>    
, document.getElementById('root'));
registerServiceWorker();
```
</details>

<img src="https://github.com/DevMountain/home-loan-wizard/blob/solution/readme-assets/1.png" />

## Step 3

### Summary

Because we needed to pass state down to our routes, we had to make our routing a function. Currently, we're exporting a function by default in our `router.js`, by making this a function, we were able to import it into our `App.js` and then pass it props through its arguments. 

In addition to our route component being a function, the way we're connecting our `Route` to the correct component is using a `render={()=> <Component prop={prop}/> path='/'}` instead of a `component={Component} path='/'`. The reason we needed to use render this way was so we could pass props down through the Components element. However, this results in messy looking code.

In this step, we are going to clean up the mess.

### Instructions

* Open `src/router.js`.
* Instead of exporting a function, let's remove the function and simply export the chunk of JSX that was returned by the function.
  * You will start getting errors coming from the props on the routes rendered elements once our routing is no longer a function, this is because they're no longer receiving information via parameters from the function and are now undefined.
* For each individual route, instead of using render, we will be using component. 
  * A route should look like the following: `<Route component={ theComponent }  path='/thePath'/>`

<br />

Now that we've changed our `router.js`, no data is going to be passed to our other components, you will also get an error that says `TypeError: __webpack_require__.i(...) is not a function`. This is because in our `App.js` router is still being treated as a function.

* Open `src/App.js`.
* Remove the invoking parenthesis from your `{router}` as well as the content inside of them.


<details>

<summary> Detailed Instructions </summary>

<br />

Let's begin by opening `src/router.js` and importing `HashRouter` from `react-router-dom`. We can replace `Switch` with `HashRouter` since we will no longer be using `Switch`.

```js
import { Switch, Route } from 'react-router-dom';
```

We can then copy and paste all the routes from the old export default statement into your new one. We'll also need to make modifications to each one so that it looks like: `<Route component={ theComponent } path="/thePath" />`. When finished you'll end up with:

```js
export default (
  <Switch>

      <Route component={NextBtn} exact path= '/'/>
      <Route component={WizardOne}  path='/wOne'/>
      <Route component={WizardTwo}  path="/wTwo"/>
      <Route component={WizardThree} path="/wThree"/>
      <Route component={WizardFour} path="/wFour"/>
      <Route component={WizardFive} path="/wFive"/>
      <Route component={WizardSix} path="/wSix"/>
      <Route component={WizardSeven} path="/wSeven"/>
      <Route component={WizardEight} path="/wEight"/>
      <Route component={WizardNine} path="/wNine"/>
      <Route component={WizardTen} path="/wTen"/>
      <Route component={WizardEleven} path="/wEleven"/>
      <Route component={Finish} path='/finish'/>

    </Switch>
)
```

Before you exit this file, delete the entire old `export default` statement.

If you noticed the app is no longer working, this is normal. We are restructuring the entire application. We can fix the errors by going into `src/App.js` and modifying how we are using `router`.

```js
  render() {
    return (
      <div>
    
        { router }

      </div>
    );
  }
```

The application should now render correctly again.

</details>

### Solution

<details>

<summary> <code> src/router.js </code> </summary>

```js
import React from 'react';
import WizardOne from './components/WizardOne/WizardOne';
import WizardTwo from './components/WizardTwo/WizardTwo';
import WizardThree from './components/WizardThree/WizardThree';
import WizardFour from './components/WizardFour/WizardFour';
import WizardFive from './components/WizardFive/WizardFive';
import WizardSix from './components/WizardSix/WizardSix';
import WizardSeven from './components/WizardSeven/WizardSeven';
import WizardEight from './components/WizardEight/WizardEight';
import WizardNine from './components/WizardNine/WizardNine';
import WizardTen from './components/WizardTen/WizardTen';
import WizardEleven from './components/WizardEleven/WizardEleven';
import Finish from './components/Finish/Finish';

import NextBtn from './components/NextBtn/NextBtn';
import { Switch, Route } from 'react-router-dom';

export default (
  <Switch>  

        <Route component={NextBtn} exact path= '/'/>
        <Route component={WizardOne}  path='/wOne'/>
        <Route component={WizardTwo}  path="/wTwo"/>
        <Route component={WizardThree} path="/wThree"/>
        <Route component={WizardFour} path="/wFour"/>
        <Route component={WizardFive} path="/wFive"/>
        <Route component={WizardSix} path="/wSix"/>
        <Route component={WizardSeven} path="/wSeven"/>
        <Route component={WizardEight} path="/wEight"/>
        <Route component={WizardNine} path="/wNine"/>
        <Route component={WizardTen} path="/wTen"/>
        <Route component={WizardEleven} path="/wEleven"/>
        <Route component={Finish} path='/finish'/>

      </Switch>
)
```
</details>

<details>
<summary><code> src/App.js</code></summary>

```js
import React, { Component } from 'react';
import './App.css';
import router from './router'


class App extends Component {
  constructor(){
    super()
    this.state = {
      loanType: 'Home Purchase',
      propertyType: 'Single Family Home',
      propToBeUsedOn: '',
      city: '',
      found: "false",
      realEstateAgent: "false",
      downPayment: 0,
      cost: 0,
      credit: '',
      history: '',
      addressOne: '',
      addressTwo: '',
      addressThree: '',
      firstName: '',
      lastName: '',
      email: ''
    }
     
    this.handleChangeLoanType = this.handleChangeLoanType.bind(this);
    this.handleChangePropertyType = this.handleChangePropertyType.bind(this);
    this.handleChangePropertyToBeUsedOn = this.handleChangePropertyToBeUsedOn.bind(this);
    this.handleChangeCity = this.handleChangeCity.bind(this);
    this.handleChangeFoundFalse = this.handleChangeFoundFalse.bind(this);
    this.handleChangeFoundTrue = this.handleChangeFoundTrue.bind(this);
    this.handleChangeRealEstateAgentTrue = this.handleChangeRealEstateAgentTrue.bind(this);
    this.handleChangeRealEstateAgentFalse = this.handleChangeRealEstateAgentFalse.bind(this);
    this.handleChangeUpdateDownPayment = this.handleChangeUpdateDownPayment.bind(this);
    this.handleChangeUpdateCost = this.handleChangeUpdateCost.bind(this);
    this.handleChangeCreditE = this.handleChangeCreditE.bind(this);
    this.handleChangeCreditG = this.handleChangeCreditG.bind(this);
    this.handleChangeCreditF = this.handleChangeCreditF.bind(this);
    this.handleChangeCreditP = this.handleChangeCreditP.bind(this);
    this.handleChangeUpdateHistory = this.handleChangeUpdateHistory.bind(this);
    this.handleChangeAddressOne = this.handleChangeAddressOne.bind(this);
    this.handleChangeAddressTwo = this.handleChangeAddressTwo.bind(this);
    this.handleChangeAddressThree = this.handleChangeAddressThree.bind(this);
    this.handleChangeFirstName = this.handleChangeFirstName.bind(this);
    this.handleChangeLastName = this.handleChangeLastName.bind(this);
    this.handleChangeEmail = this.handleChangeEmail.bind(this);
  }
    
    handleChangeLoanType(event) {
        this.setState({loanType : event.target.value});
    }
    handleChangePropertyType(event) {
        this.setState({propertyType : event.target.value});
    }
    handleChangePropertyToBeUsedOn(event){
        this.setState({propToBeUsedOn : event.target.value})
    }
    handleChangeCity(event){
        this.setState({city : event.target.value});
    }
    handleChangeFoundTrue(event){
        this.setState({found : "true"});
    }
    handleChangeFoundFalse(event){
        this.setState({found : "false"});
    }
    handleChangeRealEstateAgentTrue(){
        this.setState({realEstateAgent : "true"});
    }
    handleChangeRealEstateAgentFalse(){
        this.setState({realEstateAgent : "false"});
    }
    handleChangeUpdateDownPayment(event){
        this.setState({downPayment : event.target.value})
    }
    handleChangeUpdateCost(event){
      this.setState({cost: event.target.value});
    }
    handleChangeCreditE(){
      this.setState({credit: 'Excellent'})
    }
    handleChangeCreditG(){
      this.setState({credit: 'Good'})
    }
    handleChangeCreditF(){
      this.setState({credit: 'Fair'})
    }
    handleChangeCreditP(){
      this.setState({credit: 'Poor'})
    }
    handleChangeUpdateHistory(event){
      this.setState({history: event.target.value})
    }
    handleChangeAddressOne(event){
      this.setState({addressOne: event.target.value})
    }
    handleChangeAddressTwo(event){
      this.setState({addressTwo: event.target.value})
    }
    handleChangeAddressThree(event){
      this.setState({addressThree: event.target.value})
    }
    handleChangeFirstName(event){
      this.setState({firstName : event.target.value})
    }
    handleChangeLastName(event){
      this.setState({lastName: event.target.value})
    }
    handleChangeEmail(event){
      this.setState({email: event.target.value})
    }

  render() {
    return (
      <div>
        { router }
      </div>
    );
  }
}

export default App;
```
</details>

## Step 4

### Summary

In this step, we'll be removing the state and handler methods from `App.js`. That's because we no longer need either. Instead, all of our wizard steps (components) will connect to the redux store separately, and we don't need to track state in `App.js`, just for the sake of passing it down as props.

### Instructions

* Open `src/App.js`.
* In the App component, delete the constructor and state.
* Delete all the handler methods.
* In `render()`, delete everything but the `div` with the router.

### Solution

<details>

<summary> <code> src/App.js </code> </summary>

```js
import React, { Component } from 'react';
import './App.css';
import router from './router';

class App extends Component {
  render() {
    return (
      <div>
        { router }
      </div>
    );
  }
}

export default App;
```

</details>

## Step 5

### Summary

Let's begin connecting our views. We'll start with the Eleventh view. I chose the Eleventh view because as we start hooking our views up with `redux`, we'll be able to see the data getting to where it needs to end up.

### Instructions 

* Open `src/components/WizardEleven/WizardEleven.js`.
* Import `connect` from `react-redux`
* Connect the component to the `redux store`, just like we did for `src/App.js`.
  * Instead of `returning` the entire state in `mapStateToProps`, return only the properties the component needs:
    * <details>

      <summary> <code> Properties </code> </summary>
      
      ```
      loanType,
      propertyType,
      city,
      propToBeUsedOn,
      found,
      realEstateAgent,
      cost,
      downPayment,
      credit,
      history,
      addressOne,
      addressTwo,
      addressThree,
      firstName,
      lastName,
      email
      ```
      
      </details>
    * You may be scratching your head as to why we are using these exact propeties. When we setup the reducer later on, these will be the names of the properties the `redux` store will be managing. 

<details>

<summary> Detailed Instructions </summary>

<br />

Let's begin by opening `src/components/WizardEleven/WizardEleven.js` and importing `connect` from `react-redux`.

```js
import { connect } from 'react-redux'; 
```

Before we create our `connect` statement, let's make a `mapStateToProps` function just like we did in `src/App.js`. This time, instead of passing the entire state from the store, we are going to pick very specific properties. The list of properties we'll need are listed in the instructions above. 

```js
function mapStateToProps( state ) {
  return{ 
      loanType: state.loanType,
      propertyType: state.propertyType,
      city: state.city,
      propToBeUsedOn: state.propToBeUsedOn,
      found: state.found,
      realEstateAgent: state.realEstateAgent,
      cost: state.cost,
      downPayment: state.downPayment,
      credit: state.credit,
      history: state.history,
      addressOne: state.addressOne,
      addressTwo: state.addressTwo,
      addressThree: state.addressThree,
      firstName: state.firstName,
      lastName: state.lastName,
      email: state.email
  };
}

export default WizardEleven;
```

Now that we have the parts of state we want, we can create our `connect` statement.

```js

function mapStateToProps( state ) {
  return {
    loanType: state.loanType,
    propertyType: state.propertyType,
    city: state.city,
    propToBeUsedOn: state.propToBeUsedOn,
    found: state.found,
    realEstateAgent: state.realEstateAgent,
    cost: state.cost,
    downPayment: state.downPayment,
    credit: state.credit,
    history: state.history,
    addressOne: state.addressOne,
    addressTwo: state.addressTwo,
    addressThree: state.addressThree,
    firstName: state.firstName,
    lastName: state.lastName,
    email: state.email
  };
}

export default connect( mapStateToProps )( WizardEleven ); 
```

</details>

### Solution

<details>

<summary> <code> src/components/WizardEleven/WizardEleven.js </code> </summary>

```js
import React,  { Component } from 'react';
import { connect } from 'react-redux'; 
import { Link } from 'react-router-dom';

class WizardEleven extends Component {
  render(){
    return(
      <div className="parent-div">
        <div className="vert-align">
            <p>Here is an overview of your form:</p> 
            <div >
                <div className="overarching-div">
                    <div className="form" >Name: 
                        <p className="p2">
                            {this.props.firstName} {this.props.lastName}
                        </p>
                    </div> 
                </div>
                <div className="overarching-div">
                    <div className="form" >Email: 
                        <p className="p2">
                          {this.props.email}
                        </p>
                    </div> 
                </div>
                <div className="overarching-div">
                    <div className="form" >What type of loan will you be needing?: 
                        <p className="p2">
                            {this.props.loanType}
                        </p> 
                    </div>
                </div>
                <div className="overarching-div">
                    <div className="form" >What type of property are you purchasing?: 
                        <p className="p2">
                            {this.props.propertyType}
                        </p>
                    </div>
                </div>
                <div className="overarching-div">
                    <div className="form" >In what city will the property be located?: 
                        <p className="p2"> 
                            {this.props.city}
                        </p>
                    </div>
                </div>
                <div className="overarching-div">
                    <div className="form" >Type of property the loan is applied to:
                        <p className="p2">
                            {this.props.propToBeUsedOn}
                        </p> 
                    </div>
                </div>
                <div className="overarching-div">
                    <div className="form" >Have you already found your new home?: 
                        <p className="p2">
                            {this.props.found}
                        </p>
                    </div> 
                </div>
                <div className="overarching-div">
                    <div className="form" >Currently working with a real estate agent?: 
                        <p className="p2">
                            {this.props.realEstateAgent}
                        </p>
                    </div>
                </div>
                <div className="overarching-div">
                    <div className="form" >Estimated purchase price of the home: 
                        <p className="p2">
                            {this.props.cost}
                        </p>
                    </div> 
                </div>
                <div className="overarching-div">
                    <div className="form" >Down payment: 
                        <p className="p2">
                            {this.props.downPayment}
                        </p>
                    </div> 
                </div>
                <div className="overarching-div">
                    <div className="form" >Credit score: 
                        <p className="p2"> 
                            {this.props.credit}
                        </p>
                    </div>
                </div>
                <div className="overarching-div">
                    <div className="form" >Bankruptcy history: 
                        <p className="p2">
                            {this.props.history}
                        </p>
                    </div>
                </div>
                <div className="overarching-div">
                    <div className="form" >Current Address: 
                        <p className="p2">
                            {this.props.addressOne} <br />
                            {this.props.addressTwo} <br />
                            {this.props.addressThree}
                        </p>
                    </div>
                </div>
            </div>   
        </div>
        <div className="row">
            <Link to="/finish"> <button>Send</button></Link>
            <Link to="/"> <button>Start Again</button></Link>
        </div>
      </div>
    )
  }
}

function mapStateToProps( state ) {
  return { 
      loanType: state.loanType,
      propertyType: state.propertyType,
      city: state.city,
      propToBeUsedOn: state.propToBeUsedOn,
      found: state.found,
      realEstateAgent: state.realEstateAgent,
      cost: state.cost,
      downPayment: state.downPayment,
      credit: state.credit,
      history: state.history,
      addressOne: state.addressOne,
      addressTwo: state.addressTwo,
      addressThree: state.addressThree,
      firstName: state.firstName,
      lastName: state.lastName,
      email: state.email
  };
}

export default connect( mapStateToProps )( WizardEleven ); 
```

</details>

## Step 6

### Summary

Now let's take a look at our first view: `src/components/WizardOne/WizardOne.js`. It looks like we need to be able to update the `loanType` and `propertyType` items on state. In redux, in order to update something, we need to have a reducer and action creators.

In this step, we'll start creating our store's reducer and the action creators to update `loanType` and `propertyType`.

### Instructions

* Open `src/ducks/reducer.js`.
* Create an `initialState` object, at the very top of the file, with the following properties:
  * <details>
  
    <summary> <code> Initial State Properties </code> </summary>
    
    ```js
    loanType: 'Home Purchase',
    propertyType: 'Single Family Home',
    city: '',
    propToBeUsedOn: '',
    found: "false",
    realEstateAgent: "false",
    cost: 0,
    downPayment: 0,
    credit: '',
    history: '',
    addressOne: '',
    addressTwo: '',
    addressThree: '',
    firstName: '',
    lastName: '',
    email: ''
    ```
    
    </details>
* Modify the `reducer` function to have a state and action parameter. 
  * The `state` parameter should default to `initialState`.
* Create two action types in between `initialState` and the `reducer` function.
  * The first action type should equal: `"UPDATE_LOAN_TYPE"`.
  * The second action type should equal: `"UPDATE_PROPERTY_TYPE"`.
* Create two action creators in between the `reducer` function and the `export default` statement.
  * The first action creator should have a type of `UPDATE_LOAN_TYPE`.
    * This action creator should have a parameter called `loanType`.
    * This action creator should have a payload that equals `loanType`.
  * The second action creator should have a type of `UPDATE_PROPERTY_TYPE`.
    * This action creator should have a parameter called `property`.
    * This action creator should have a payload that equals `property`.
* Modify the `reducer` function to use a `switch` statement on the `action.type`.
  * Create a `case` for `UPDATE_LOAN_TYPE` and update state with the new loan type.
  * Create a `case` for `UPDATE_PROPERTY_TYPE` and update state with the new property type.
  * Create a `default case` that returns state.

<details>

<summary> Detailed Instructions </summary>

<br />

Let's begin by opening `src/ducks/reducer.js`. Our store will need an initial state when it loads for the first time. Let's create a constant variable called `initialState` that will have all of our state's initial values. The property list is listed above in the instructions.

```js
const initialState = {
  loanType: 'Home Purchase',
  propertyType: 'Single Family Home',
  city: '',
  propToBeUsedOn: '',
  found: false,
  realEstateAgent: "false",
  cost: 0,
  downPayment: 0,
  credit: '',
  history: '',
  addressOne: '',
  addressTwo: '',
  addressThree: '',
  firstName: '',
  lastName: '',
  email: ''
};
```

Now that we have an initial state we can update our `reducer` function to have a `state` and `action` parameter. Using `es6` default parameters we can default the `state` parameter to `initialState`. This will happen when the store is first created. 

```js
function reducer( state = initialState, action ) { 

}
```

Before we create the action creators our store needs to determine how to update state, we need to create our action types. We'll put these action types in between our `initialState` and `reducer` function. We'll need two types for this step. One type for updating the loan type and one type for updating the property type. 

```js
const UPDATE_LOAN_TYPE = "UPDATE_LOAN_TYPE";
const UPDATE_PROPERTY_TYPE = "UPDATE_PROPERTY_TYPE";
```

Now that we have our two action types we can create action creators that use them. All an action creator does is return an object with a `type` and `payload` property. The `payload` will equal the value of the parameter in this case. The action creator for loan type will have a `loanType` parameter and the action creator for property type will have a `property` parameter. We also export these action creators so other components can use them. Let's add them under the `reducer` function.

```js
export function updateLoanType( loanType ){
  return {
    type: UPDATE_LOAN_TYPE,
    payload: loanType
  }
}

export function updatePropertyType( property ) {
  return {
    type: UPDATE_PROPERTY_TYPE,
    payload: property
  }
}
```

The last thing we need to do is update the `reducer` function to use a `switch` statement on the `action.type`. This is how our `reducer` will determine which part of state to update. Since we need to keep state `immutable` we will make use of `Object.assign`. Let's start by adding a `switch` statement to our reducer. The `default case` for this switch should just return `state`.

```js
function reducer( state = initialState, action ) { 
  switch( action.type ) {

    default: return state;
  }
}
```

To add our action types to our reducer all we have to do is: `case actionTypeVariableGoesHere`. We'll then use `Object.assign` to get the previous value of state and update its `loanType` or `propertyType` property to the value on the payload.

```js
function reducer( state = initialState, action ) { 
  switch( action.type ) {
    case  UPDATE_LOAN_TYPE:
      return Object.assign( {}, state, { loanType: action.payload } );

    case UPDATE_PROPERTY_TYPE:
      return Object.assign( {}, state, { propertyType: action.payload } );

    default: return state;
  }
}
```
</details>

### Solution

<details>

<summary> <code> src/ducks/reducer.js </code> </summary>

```js
const initialState = {
   loanType: 'Home Purchase',
   propertyType: 'Single Family Home',
   city: '',
   propToBeUsedOn: '',
   found: false,
   realEstateAgent: "false",
   cost: 0,
   downPayment: 0,
   credit: '',
   history: '',
   addressOne: '',
   addressTwo: '',
   addressThree: '',
   firstName: 'aa',
   lastName: '',
   email: ''
}

const UPDATE_LOAN_TYPE = "UPDATE_LOAN_TYPE";
const UPDATE_PROPERTY_TYPE = 'UPDATE_PROPERTY_TYPE'; 

function reducer( state = initialState, action ){ 
    switch( action.type ){
      case UPDATE_LOAN_TYPE:
          return Object.assign( {}, state, { loanType: action.payload } );

      case UPDATE_PROPERTY_TYPE:
          return Object.assign( {}, state, { propertyType: action.payload } );

      default: return state;
    }
} 

export function updateLoanType( loanType ){
  return {
    type: UPDATE_LOAN_TYPE,
    payload: loanType
  }
}

export function updatePropertyType( property ) {
  return {
    type: UPDATE_PROPERTY_TYPE,
    payload: property
  }
}

export default reducer; 
```

</details>

## Step 7

### Summary

In this step, we will connect `src/components/WizardOne/WizardOne.js` to the store and configure the component to use the action creators we have created so far.

### Instructions

* Open `src/components/WizardOne/WizardOne.js`.
* Import `connect` from `react-redux`.
* Import the `updateLoanType` and `updatePropertyType` action creators from `src/ducks/reducer.js`.
  * Hint: Use destructuring.
* Modify the `export default` statement to use `connect`.
  * Use `mapStateToProps` to return the only two parts of `state` it will need.
  * Use a second parameter on the `connect` statement that passes in the action creators.
* Modify the two `onChange` events to use the action creators.
  * Hint: Both action creators need an argument.

<details>

<summary> Detailed Instructions </summary>

<br />

Let's begin by opening `src/components/WizardOne/WizardOne.js` and importing `connect` and the action creators we have created so far. 

```js
import { connect } from 'react-redux';
import { updateLoanType, updatePropertyType } from '../../ducks/reducer';
```

Now that we have these, we can modify the `export default` statement to `connect` to our store. In this case, we'll only need two properties from `state` and we'll also be passing in the action creators. When we pass in the action creators into our `connect` statement it wraps them in a `dispatch` function. This allows our component to just call the action creator. If we didn't do it this way, we would have to import `dispatch` and call `dispatch` with our action creator as an argument. 

Since this component has select statements for a loan type and property type, we will want the `loanType` and `propertyType` from `state`.

```js
function mapStateToProps( state ) {
  const { loanType, propertyType } = state;

  return {
    loanType,
    propertyType
  };
}

export default connect( mapStateToProps, { updateLoanType, updatePropertyType } )( WizardOne );
```

We can then destructure our action creators off of `props`. It is imperative that you call your action creators off of `props` otherwise the function call will never make it to the `store`.

```js
render() {
  const { updateLoanType, updatePropertyType } = this.props;
}
```

Now that our component is connected to the `store` and our action creators are destructured off of `props`, we can modify the `onChange` events to call the action creators. Remember that each action creator needs one argument. This argument will be the value that replaces the property's value on `state`. We can capture the event and pass in the event's target value as the argument.

```js
<select onChange={ ( e ) => updateLoanType( e.target.value ) }>
  <option type="text" value="Home Purchase" >Home Purchase</option>
  <option type="text" value="Refinance" >Refinance</option>
  <option type="text" value="Home Equity" >Home Equity loan/line</option>
</select> <br/>

<select onChange={ ( e ) => updatePropertyType( e.target.value ) }>
  <option value="Single Family Home">Single Family Home</option>
  <option value="Town Home">Townhome</option>
  <option value="Condo">Condo</option>
  <option value="Multi Family Home">Multi Family Dwelling</option>
  <option value="Mobile Home">Mobile Home</option>
</select>
```

</details>

### Solution

<details>

<summary> <code> src/components/WizardOne/WizardOne.js </code> </summary>

```js
import React,  { Component } from 'react';
import { Link } from 'react-router-dom';

import { connect } from 'react-redux';
import { updateLoanType, updatePropertyType } from '../../ducks/reducer';

class WizardOne extends Component {
  render(){
    const { updateLoanType, updatePropertyType } = this.props;

    return(
      <div className="parent-div">
        <div className="vert-align">
          <p>What type of loan will you be needing?</p> <br />
      
          <select onChange={ ( e ) => updateLoanType( e.target.value ) }>
            <option type="text" value="Home Purchase" >Home Purchase</option>
            <option type="text" value="Refinance" >Refinance</option>
            <option type="text" value="Home Equity" >Home Equity loan/line</option>
          </select> <br/>

          <p>What type of property are you purchasing?</p> <br />

          <select onChange={ ( e ) => updatePropertyType( e.target.value ) }>
            <option value="Single Family Home">Single Family Home</option>
            <option value="Town Home">Townhome</option>
            <option value="Condo">Condo</option>
            <option value="Multi Family Home">Multi Family Dwelling</option>
            <option value="Mobile Home">Mobile Home</option>
          </select>
          
          <Link to="/wTwo"><button className="margin-btn"> Next </button></Link>
        </div>
      </div>
    )
  }
}

function mapStateToProps( state ) {
  const { loanType, propertyType } = state;

  return {
    loanType,
    propertyType
  };
}

export default connect( mapStateToProps, { updateLoanType, updatePropertyType } )( WizardOne ); 
```

</details>

<br />

<img src="https://github.com/DevMountain/home-loan-wizard/blob/solution/readme-assets/1g.gif" />

## Step 8

### Summary

In this step, we will update the reducer to handle modifying the city on state. We will also configure the `src/components/WizardTwo/WizardTwo.js` to connect to the store and use an action creator to update the city on state.

### Instructions 

* Open `src/ducks/reducer.js`.
* Create an action type for `UPDATE_CITY`.
* Create an action creator called `updateCity`.
  * This action creator should use a parameter called `city`.
* Add an `UPDATE_CITY` case to the reducer that updates `city`.
  * Remember to keep state immutable. 
* Open `src/components/WizardTwo/WizardTwo.js`.
* Import `connect` from `react-redux`.
* Import `updateCity` from `src/ducks/reducer.js`.
* Modify the `export default` statement to use connect.
  * `mapStateToProps` should only return one property from state.
  * `updateCity` should be passed in as a second parameter.
* Modify the `onChange` event to call `updateCity`.
  * Remember this action creator has one parameter.

<details>

<summary> Detailed Instructions </summary>

<br />

Let's begin by opening `src/ducks/reducer.js` and creating an `UPDATE_CITY` action type. 

```js
const UPDATE_CITY = 'UPDATE_CITY';
```

Then we can create an `updateCity` action creator that uses `UPDATE_CITY` as its `type`. This action creator should have a parameter called `city`. We will use the value of `city` for the payload property.

```js
export function updateCity( city ) {
  return {
    type: UPDATE_CITY,
    payload: city
  }
}
```

Now let's add an `UPDATE_CITY` case to the reducer. In this case, the reducer should update the value of `city` on state using the value set on the action's payload. Remember that we need to keep state immutable, so we'll make use of `Object.assign`.

```js
case UPDATE_CITY:
  return Object.assign( {}, state, { city: action.payload } );
```

Our store now has everything it needs to update the `state`'s city. Let's now implement this into `src/components/WizardTwo/WizardTwo.js`. Open this file and import `connect` from `react-redux` and import `updateCity` from `src/ducks/reducer.js`.

```js
import { connect } from 'react-redux';
import { updateCity } from '../../ducks/reducer.js';
``` 

Before we modify our component to `connect` to the store, let's create a `mapStateToProps` function. Since the second screen of the wizard process only asks the user for their city, we only need city from the `store`'s state.

```js
function mapStateToProps( state ) {
  const { city } = state;

  return {
    city
  };
}

export default WizardTwo;
```

Now that we have a `mapStateToProps` function, let's modify the `export default` statement to use `connect`. Remember that we should also include `updateCity` as a second parameter. This will allow us to call `updateCity` off of props without having to worry about `dispatch`.

```js
export default connect( mapStateToProps, { updateCity } )( WizardTwo );
```

Now that our component is connected to the store, we can update the `onChange` event to call `updateCity` instead. You can either deconstruct `updateCity` off of props or call `this.props.updateCity`.

```js
<input placeholder="city name" type="text" onChange={ ( e ) => updateCity( e.target.value ) } />
```

</details>

### Solution

<details>

<summary> <code> src/ducks/reducer.js </code> </summary>

```js
const initialState = {
   loanType: 'Home Purchase',
   propertyType: 'Single Family Home',
   city: '',
   propToBeUsedOn: '',
   found: false,
   realEstateAgent: "false",
   cost: 0,
   downPayment: 0,
   credit: '',
   history: '',
   addressOne: '',
   addressTwo: '',
   addressThree: '',
   firstName: 'aa',
   lastName: '',
   email: ''
}

const UPDATE_LOAN_TYPE = "UPDATE_LOAN_TYPE";
const UPDATE_PROPERTY_TYPE = 'UPDATE_PROPERTY_TYPE';
const UPDATE_CITY = "UPDATE_CITY";

function reducer( state = initialState, action ) { 
    switch( action.type ){
      case UPDATE_LOAN_TYPE:
        return Object.assign( {}, state, { loanType: action.payload } );

      case UPDATE_PROPERTY_TYPE:
        return Object.assign( {}, state, { propertyType: action.payload } );

      case UPDATE_CITY:
        return Object.assign( {}, state, { city: action.payload } );

      default: return state;
    }
} 

export function updateLoanType( loanType ){
  return {
    type: UPDATE_LOAN_TYPE,
    payload: loanType
  };
}

export function updatePropertyType( property ) {
  return {
    type: UPDATE_PROPERTY_TYPE,
    payload: property
  };
}

export function updateCity( city ) {
  return {
    type: UPDATE_CITY,
    payload: city
  };
}

export default reducer; 
```

</details>

<details>

<summary> <code> src/components/WizardTwo/WizardTwo.js </code> </summary>

```js
import React,  { Component } from 'react';
import { Link } from 'react-router-dom';

import { connect } from "react-redux";
import { updateCity } from '../../ducks/reducer';

class WizardTwo extends Component {
  render() {
    const { updateCity } = this.props;

    return(
      <div className="parent-div">
        <div className="vert-align">
          <p>In what city will the property be located?</p><br />
            
          <input placeholder="city name" type="text" onChange={ ( e ) => updateCity( e.target.value ) } />
        
          <Link to="/wThree"><button className="wTwo-btn"> Next </button></Link>
        </div>
      </div>
    )
  }
}

function mapStateToProps( state ) {
  const { city } = state;

  return {
    city
  };
}

export default connect( mapStateToProps, { updateCity } )( WizardTwo );
```

</details>

<br />

<img src="https://github.com/DevMountain/home-loan-wizard/blob/solution/readme-assets/2-1g.gif" />

## Step 9

### Summary

In this step, we will update the reducer to handle modifying the `propToBeUsedOn` on state. We will also configure  `src/components/WizardThree/WizardThree.js` to connect to the store and use an action creator to update `propToBeUsedOn` on state.

### Instructions

* Open `src/ducks/reducer.js`.
* Create an action type for `UPDATE_PROP`.
* Create an action creator called `updateProp`.
  * This action creator should use a parameter called `prop`.
* Add an `UPDATE_PROP` case to the reducer that updates `propToBeUsedOn`.
  * Remember to keep state immutable. 
* Open `src/components/WizardThree/WizardThree.js`.
* Import `connect` from `react-redux`.
* Import `updateProp` from `src/ducks/reducer.js`.
* Modify the `export default` statement to use connect.
  * `mapStateToProps` should only return one property from state.
  * `updateProp` should be passed in as a second parameter.
* Modify the `onClick` events to call `updateProp`.
  * Remember this action creator has one parameter.

<details>

<summary> Detailed Instructions </summary>

<br />

Let's begin by opening `src/ducks/reducer.js` and creating an `UPDATE_PROP` action type. 

```js
const UPDATE_PROP = 'UPDATE_PROP';
```

Then we can create an `updateProp` action creator that uses `UPDATE_PROP` as its `type`. This action creator should have a parameter called `prop`. We will use the value of `prop` for the payload property.

```js
export function updateProp( prop ) {
  return {
    type: UPDATE_PROP,
    payload: prop
  }
}
```

Now let's add an `UPDATE_PROP` case to the reducer. In this case, the reducer should update the value of `propToBeUsedOn` on state using the value set on the action's payload. Remember that we need to keep state immutable, so we'll make use of `Object.assign`.

```js
case UPDATE_PROP:
  return Object.assign( {}, state, { propToBeUsedOn: action.payload } );
```

Our store now has everything it needs to update the `state`'s `propToBeUsedOn` property. Let's now implement this into `src/components/WizardThree/WizardThree.js`. Open this file and import `connect` from `react-redux` and import `updateProp` from `src/ducks/reducer.js`.

```js
import { connect } from 'react-redux';
import { updateProp } from '../../ducks/reducer.js';
``` 

Before we modify our component to `connect` to the store, let's create a `mapStateToProps` function. Since the third screen of the wizard process only asks the user for their property type, we only need `propToBeUsedOn` from the `store`'s state.

```js
function mapStateToProps( state ) {
  const { propToBeUsedOn } = state;

  return {
    propToBeUsedOn
  };
}

export default WizardThree;
```

Now that we have a `mapStateToProps` function, let's modify the `export default` statement to use `connect`. Remember that we should also include `updateProp` as a second parameter. This will allow us to call `updateProp` off of props without having to worry about `dispatch`.

```js
export default connect( mapStateToProps, { updateProp } )( WizardThree );
```

Now that our component is connected to the store, we can update the `onClick` events to call `updateProp` instead. You can either deconstruct `updateProp` off of props or call `this.props.updateProp`. Since the button elements have a value, you can capture the event and pass in the event's target value.

```js
<button value="primaryHome" onClick={ ( e ) => updateProp( e.target.value ) }>Primary Home</button>
<button value="rentalProperty" onClick={ ( e ) => updateProp( e.target.value ) }>Rental Property</button>
<button value="secondaryHome" onClick={ ( e ) => updateProp( e.target.value ) }>Secondary Home</button>
```

</details>

### Solution

<details>

<summary> <code> src/ducks/reducer.js </code> </summary>

```js
const initialState = {
   loanType: 'Home Purchase',
   propertyType: 'Single Family Home',
   city: '',
   propToBeUsedOn: '',
   found: false,
   realEstateAgent: "false",
   cost: 0,
   downPayment: 0,
   credit: '',
   history: '',
   addressOne: '',
   addressTwo: '',
   addressThree: '',
   firstName: 'aa',
   lastName: '',
   email: ''
}

const UPDATE_LOAN_TYPE = "UPDATE_LOAN_TYPE";
const UPDATE_PROPERTY_TYPE = 'UPDATE_PROPERTY_TYPE';
const UPDATE_CITY = "UPDATE_CITY";
const UPDATE_PROP = "UPDATE_PROP";

function reducer( state = initialState, action ) { 
    console.log('REDUCER HIT: Action ->', action );
    
    switch( action.type ){
      case UPDATE_LOAN_TYPE:
        return Object.assign( {}, state, { loanType: action.payload } );

      case UPDATE_PROPERTY_TYPE:
        return Object.assign( {}, state, { propertyType: action.payload } );

      case UPDATE_CITY:
        return Object.assign( {}, state, { city: action.payload } );

      case UPDATE_PROP:
        return Object.assign( {}, state, { propToBeUsedOn: action.payload } );

      default: return state;
    }
} 

export function updateLoanType( loanType ){
  return {
    type: UPDATE_LOAN_TYPE,
    payload: loanType
  };
}

export function updatePropertyType( property ) {
  return {
    type: UPDATE_PROPERTY_TYPE,
    payload: property
  };
}

export function updateCity( city ) {
  return {
    type: UPDATE_CITY,
    payload: city
  };
}

export function updateProp( prop ) {
  return {
    type: UPDATE_PROP,
    payload: prop
  };
}

export default reducer; 
```

</details>

<details>

<summary> <code> src/components/WizardThree/WizardThree.js </code> </summary>

```js
import React,  { Component } from 'react';
import { Link } from 'react-router-dom';

import { connect } from 'react-redux';
import { updateProp } from '../../ducks/reducer';

class WizardThree extends Component {
  render() {
    const { updateProp } = this.props;

    return (
      <div className="parent-div">
        <div className="vert-align">
          <p> What property are you looking to use the loan on? </p><br />
          <div className="row">
            <Link to="/wFour">
              <button value="primaryHome" onClick={ ( e ) => updateProp( e.target.value ) }>Primary Home</button>
            </Link>

            <Link to="/wFour">
              <button value="rentalProperty" onClick={ ( e ) => updateProp( e.target.value ) }>Rental Property</button>
            </Link>

            <Link to="/wFour">
              <button value="secondaryHome" onClick={ ( e ) => updateProp( e.target.value ) }>Secondary Home</button>
            </Link>
          </div>
        </div>
      </div>
    )
  }
}

function mapStateToProps( state ) {
  const { propToBeUsedOn } = state;

  return {
    propToBeUsedOn
  };
}

export default connect( mapStateToProps, { updateProp } )( WizardThree );
```

</details>

<br />

<img src="https://github.com/DevMountain/home-loan-wizard/blob/solution/readme-assets/3g.gif" />

## Step 10

### Summary

In this step, we will update the reducer to handle modifying the `found` on state. We will also configure  `src/components/WizardFour/WizardFour.js` to connect to the store and use an action creator to update `found` on state.

### Instructions 

* Open `src/ducks/reducer.js`.
* Create an action type for `UPDATE_FOUND`.
* Create an action creator called `updateFound`.
  * This action creator should use a parameter called `found`.
* Add an `UPDATE_FOUND` case to the reducer that updates `found`.
  * Remember to keep state immutable. 
* Open `src/components/WizardFour/WizardFour.js`.
* Import `connect` from `react-redux`.
* Import `updateFound` from `src/ducks/reducer.js`.
* Modify the `export default` statement to use connect.
  * `mapStateToProps` should only return one property from state.
  * `updateFound` should be passed in as a second parameter.
* Modify the `onClick` events to call `updateFound`.
  * Remember this action creator has one parameter.

<details>

<summary> Detailed Instructions </summary>

<br />

Let's begin by opening `src/ducks/reducer.js` and creating an `UPDATE_FOUND` action type. 

```js
const UPDATE_FOUND = 'UPDATE_FOUND';
```

Then we can create an `updateFound` action creator that uses `UPDATE_FOUND` as its `type`. This action creator should have a parameter called `found`. We will use the value of `found` for the payload property.

```js
export function updateFound( found ) {
  return {
    type: UPDATE_FOUND,
    payload: found
  }
}
```

Now let's add an `UPDATE_FOUND` case to the reducer. In this case, the reducer should update the value of `found` on state using the value set on the action's payload. Remember that we need to keep state immutable, so we'll make use of `Object.assign`.

```js
case UPDATE_FOUND:
  return Object.assign( {}, state, { found: action.payload } );
```

Our store now has everything it needs to update the `state`'s `found` property. Let's now implement this into `src/components/WizardFour/WizardFour.js`. Open this file and import `connect` from `react-redux` and import `updateFound` from `src/ducks/reducer.js`.

```js
import { connect } from 'react-redux';
import { updateFound } from '../../ducks/reducer.js';
``` 

Before we modify our component to `connect` to the store, let's create a `mapStateToProps` function. Since the fourth screen of the wizard process only asks the user if they have found their property, we only need `found` from the `store`'s state.

```js
function mapStateToProps( state ) {
  const { found } = state;

  return {
    found
  };
}

export default WizardFour;
```

Now that we have a `mapStateToProps` function, let's modify the `export default` statement to use `connect`. Remember that we should also include `updateFound` as a second parameter. This will allow us to call `updateFound` off of props without having to worry about `dispatch`.

```js
export default connect( mapStateToProps, { updateFound } )( WizardFour );
```

Now our component is connected to the `redux store`, let's access the function we need to change state on the Link element.
  * Set up the first Link element's `onClick` function equal to `{(e)=>this.props.updateFound("True")}`.
  * Set up the second Link element's `onClick` function equal to `{(e)=>this.props.updateFound("False")}`.
  * Because we've connected to `redux`, the updateFound function is now on props for this component.

```js
<Link to="/wFive"><button onClick={ (e)=>this.props.updateFound("True") }>Yes</button></Link>
<Link to="/wFive"><button onClick={ (e)=>this.props.updateFound("False") }>No </button></Link> 
```


</details>

### Solution

<details>

<summary> <code> src/ducks/reducer.js </code> </summary>

```js
const initialState = {
   loanType: 'Home Purchase',
   propertyType: 'Single Family Home',
   city: '',
   propToBeUsedOn: '',
   found: false,
   realEstateAgent: "false",
   cost: 0,
   downPayment: 0,
   credit: '',
   history: '',
   addressOne: '',
   addressTwo: '',
   addressThree: '',
   firstName: 'aa',
   lastName: '',
   email: ''
}

const UPDATE_LOAN_TYPE = "UPDATE_LOAN_TYPE";
const UPDATE_PROPERTY_TYPE = 'UPDATE_PROPERTY_TYPE';
const UPDATE_CITY = "UPDATE_CITY";
const UPDATE_PROP = "UPDATE_PROP";
const UPDATE_FOUND = "UPDATE_FOUND";

function reducer( state = initialState, action ) { 
    console.log('REDUCER HIT: Action ->', action );
    
    switch( action.type ){
      case UPDATE_LOAN_TYPE:
        return Object.assign( {}, state, { loanType: action.payload } );

      case UPDATE_PROPERTY_TYPE:
        return Object.assign( {}, state, { propertyType: action.payload } );

      case UPDATE_CITY:
        return Object.assign( {}, state, { city: action.payload } );

      case UPDATE_PROP:
        return Object.assign( {}, state, { propToBeUsedOn: action.payload } );

      case UPDATE_FOUND:
        return Object.assign( {}, state, { found: action.payload } );

      default: return state;
    }
} 

export function updateLoanType( loanType ){
  return {
    type: UPDATE_LOAN_TYPE,
    payload: loanType
  };
}

export function updatePropertyType( property ) {
  return {
    type: UPDATE_PROPERTY_TYPE,
    payload: property
  };
}

export function updateCity( city ) {
  return {
    type: UPDATE_CITY,
    payload: city
  };
}

export function updateProp( prop ) {
  return {
    type: UPDATE_PROP,
    payload: prop
  };
}

export function updateFound( found ) {
  return {
    type: UPDATE_FOUND,
    payload: found
  };
}

export default reducer; 
```

</details>

<details>

<summary> <code> src/components/WizardFour/WizardFour.js </code> </summary>

```js
import React,  { Component } from 'react';
import { Link } from 'react-router-dom';

import { connect } from 'react-redux';
import { updateFound } from '../../ducks/reducer';

class WizardFour extends Component {
  render() {
    const { updateFound } = this.props;

    return (
      <div className="parent-div">
        <div className="vert-align">
          <p>Have you already found your new home?</p><br />
          
          <div className="row">
            <Link to="/wFive">
              <button onClick={ ( e ) => updateFound( true ) }>Yes</button>
            </Link>

            <Link to="/wFive">
              <button onClick={ ( e ) => updateFound( false ) }>No</button>
            </Link>
          </div>
        </div>
      </div>
    )
  }
}

function mapStateToProps( state ) {
  const { found } = state;

  return {
    found
  };
}

export default connect( mapStateToProps, { updateFound } )( WizardFour );
```

</details>

<br />

<img src="https://github.com/DevMountain/home-loan-wizard/blob/solution/readme-assets/4g.gif" />

## Step 11 - Challenge

### Summary

In this step, we will complete the rest of the reducer for updating the remaining properties on state. We want this step to be a challenge for you, meaning there will not be any guided instructions. Try to complete this step without looking at any previous steps. If you get stuck, try looking back at the previous three steps.

### Instructions 

* Open `src/ducks/reducer.js`.
* Create an action type for updating the following state properties:
  * `realEstateAgent`
  * `cost`
  * `downPayment`
  * `credit`
  * `history`
  * `addressOne`
  * `addressTwo`
  * `addressThree`
  * `firstName`
  * `lastName`
  * `email`
* Create an action creator for each property listed above.
* Update the reducer to have a case for each new action type.
  * The case should update state with the value on the payload.
  * Remember to keep state immutable.

### Solution

<details>

<summary> <code> src/ducks/reducer.js </code> </summary>

```js
const initialState = {
   loanType: 'Home Purchase',
   propertyType: 'Single Family Home',
   city: '',
   propToBeUsedOn: '',
   found: false,
   realEstateAgent: "false",
   cost: 0,
   downPayment: 0,
   credit: '',
   history: '',
   addressOne: '',
   addressTwo: '',
   addressThree: '',
   firstName: 'aa',
   lastName: '',
   email: ''
}

const UPDATE_LOAN_TYPE = "UPDATE_LOAN_TYPE";
const UPDATE_PROPERTY_TYPE = 'UPDATE_PROPERTY_TYPE';
const UPDATE_CITY = "UPDATE_CITY";
const UPDATE_PROP = "UPDATE_PROP";
const UPDATE_FOUND = "UPDATE_FOUND";
const UPDATE_AGENT = "UPDATE_AGENT";
const UPDATE_COST = "UPDATE_COST";
const UPDATE_DOWN_PAYMENT = "UPDATE_DOWN_PAYMENT";
const UPDATE_CREDIT = "UPDATE_CREDIT";
const UPDATE_HISTORY = "UPDATE_HISTORY";
const UPDATE_ADDRESS_1 = "UPDATE_ADDRESS_1";
const UPDATE_ADDRESS_2 = "UPDATE_ADDRESS_2";
const UPDATE_ADDRESS_3 = "UPDATE_ADDRESS_3";
const UPDATE_FIRST = "UPDATE_FIRST";
const UPDATE_LAST = "UPDATE_LAST";
const UPDATE_EMAIL = "UPDATE_EMAIL";

function reducer( state = initialState, action ) { 
    console.log('REDUCER HIT: Action ->', action );
    
    switch( action.type ){
      case UPDATE_LOAN_TYPE:
        return Object.assign( {}, state, { loanType: action.payload } );

      case UPDATE_PROPERTY_TYPE:
        return Object.assign( {}, state, { propertyType: action.payload } );

      case UPDATE_CITY:
        return Object.assign( {}, state, { city: action.payload } );

      case UPDATE_PROP:
        return Object.assign( {}, state, { propToBeUsedOn: action.payload } );

      case UPDATE_FOUND:
        return Object.assign( {}, state, { found: action.payload } );

      case UPDATE_AGENT:
        return Object.assign( {}, state, { realEstateAgent: action.payload } );

      case UPDATE_COST:
        return Object.assign( {}, state, { cost: action.payload } );

      case UPDATE_DOWN_PAYMENT:
        return Object.assign( {}, state, { downPayment: action.payload } );

      case UPDATE_CREDIT:
        return Object.assign( {}, state, { credit: action.payload } );

      case UPDATE_HISTORY:
        return Object.assign( {}, state, { history: action.payload } );

      case UPDATE_ADDRESS_1:
        return Object.assign( {}, state, { addressOne: action.payload } );

      case UPDATE_ADDRESS_2:
        return Object.assign( {}, state, { addressTwo: action.payload } );

      case UPDATE_ADDRESS_3:
        return Object.assign( {}, state, { addressThree: action.payload } );

      case UPDATE_FIRST:
        return Object.assign( {}, state, { firstName: action.payload } );

      case UPDATE_LAST:
        return Object.assign( {}, state, { lastName: action.payload } );

      case UPDATE_EMAIL:
        return Object.assign( {}, state, { email: action.payload } );

      default: return state;
    }
} 

export function updateLoanType( loanType ){
  return {
    type: UPDATE_LOAN_TYPE,
    payload: loanType
  };
}

export function updatePropertyType( property ) {
  return {
    type: UPDATE_PROPERTY_TYPE,
    payload: property
  };
}

export function updateCity( city ) {
  return {
    type: UPDATE_CITY,
    payload: city
  };
}

export function updateProp( prop ) {
  return {
    type: UPDATE_PROP,
    payload: prop
  };
}

export function updateFound( found ) {
  return {
    type: UPDATE_FOUND,
    payload: found
  };
}

export function updateAgent( agent ) {
  return {
    type: UPDATE_AGENT,
    payload: agent
  };
}

export function updateCost( cost ) {
  return {
    type: UPDATE_COST,
    payload: cost
  };
}

export function updateDownPayment( payment ) {
  return {
    type: UPDATE_DOWN_PAYMENT,
    payload: payment
  };
}

export function updateCredit( credit ) {
  return {
    type: UPDATE_CREDIT,
    payload: credit
  };
}

export function updateHistory( history ) {
  return {
    type: UPDATE_HISTORY,
    payload: history
  };
}

export function updateAddress1( address ) {
  return {
    type: UPDATE_ADDRESS_1,
    payload: address
  };
}

export function updateAddress2( address ) {
  return {
    type: UPDATE_ADDRESS_2,
    payload: address
  };
}

export function updateAddress3( address ) {
  return {
    type: UPDATE_ADDRESS_3,
    payload: address
  };
}

export function updateFirst( first ) {
  return {
    type: UPDATE_FIRST,
    payload: first
  };
}

export function updateLast( last ) {
  return {
    type: UPDATE_LAST,
    payload: last
  };
}

export function updateEmail( email ) {
  return {
    type: UPDATE_EMAIL,
    payload: email
  };
}

export default reducer; 
```

</details>

## Step 12 - Challenge

### Summary

In this step, we will hook up the rest of the views to the store and modify the events to call our action creators. We want this step to be a challenge for you, meaning there will not be any guided instructions. Try to complete this step without looking at any previous steps. If you get stuck, try looking back steps eight through ten.

### Instructions 

Open the remaining `wizard` components ( Wizard 5-10 ) and update them to connect to the store. Remember to use `mapStateToProps` to grab only the property(s) that component is modifying. Also remember to pull in the action creator(s) from the reducer. Then modify the events in the component ( `onChange` || `onClick` ) to call the action creator(s). 

### Solution

<details>

<summary> <code> src/components/WizardFive/WizardFive.js </code> </summary>

```js
import React,  { Component } from 'react';
import { Link } from 'react-router-dom';

import { connect } from 'react-redux';
import { updateAgent } from '../../ducks/reducer';

class WizardFive extends Component {
  render() {
    const { updateAgent } = this.props;

    return (
      <div className="parent-div">
        <div className="vert-align">
          <p>Are you currently working with a real estate agent?</p> <br />
          <div className="row">
            <Link to="/wSix">
              <button onClick={ () => updateAgent( true ) }>Yes</button>
            </Link>

            <Link to="/wSix">
              <button onClick={ () => updateAgent( false ) }>No</button>
            </Link>
          </div>
        </div>
      </div>
    )
  }
}

function mapStateToProps( state ) {
  const { realEstateAgent } = state;

  return {
    realEstateAgent
  };
}

export default connect( mapStateToProps, { updateAgent } )( WizardFive );
```

</details>

<details>

<summary> <code> src/components/WizardSix/WizardSix.js </code> </summary>

```js
import React,  { Component } from 'react';
import { Link } from 'react-router-dom';

import { connect } from 'react-redux';
import { updateCost, updateDownPayment } from '../../ducks/reducer';

class WizardSix extends Component {
  render() {
    const { updateCost, updateDownPayment } = this.props;

    return (
      <div className="parent-div">
        <div className="vert-align">
          <p>What is the estimated purchase price?</p> <br />
          <input type="text" placeholder="amount" onChange={ ( e ) => updateCost( e.target.value ) } /> <br />

          <p>How much are you putting down as a down payment?</p> <br />
          <input type="text" placeholder="amount" onChange={ ( e ) => updateDownPayment( e.target.value ) } />  

          <Link to="/wSeven">
            <button className="margin-btn"> Next </button>
          </Link>
        </div>
      </div>
    )
  }
}

function mapStateToProps( state ) {
  const { cost, downPayment } = state;

  return {
    cost,
    downPayment
  };
}

export default connect( mapStateToProps, { updateCost, updateDownPayment } )( WizardSix );
```

</details>

<details>

<summary> <code> src/components/WizardSeven/WizardSeven.js </code> </summary>

```js
import React,  { Component } from 'react';
import { Link } from 'react-router-dom';

import { connect } from 'react-redux';
import { updateCredit } from '../../ducks/reducer';

class WizardSeven extends Component {
  render() {
    const { updateCredit } = this.props;

    return (
      <div className="parent-div">
        <div className="vert-align">
          <p>Estimate your credit score</p> <br />
          
          <div className="row">
            <Link to="/wEight">
              <button onClick={ () => updateCredit('Excellent') }>Excellent</button>
            </Link>

            <Link to="/wEight">
              <button onClick={ () => updateCredit('Good') }>Good</button>
            </Link>

            <Link to="/wEight">
              <button onClick={ () => updateCredit('Fair') }>Fair</button>
            </Link>

            <Link to="/wEight">
              <button onClick={ () => updateCredit('Poor') }>Poor</button>
            </Link> 
          </div>
        </div>
      </div>
    )
  }
}

function mapStateToProps( state ) {
  const { credit } = state;

  return {
    credit
  };
}

export default connect( mapStateToProps, { updateCredit } )( WizardSeven );
```

</details>

<details>

<summary> <code> src/components/WizardEight/WizardEight.js </code> </summary>

```js
import React,  { Component } from 'react';
import { Link } from 'react-router-dom';

import { connect } from 'react-redux';
import { updateHistory } from '../../ducks/reducer';

class WizardEight extends Component {
  render() {
    const { updateHistory } = this.props;

    return (
      <div className="parent-div">
        <div className="vert-align">
          <p>Have you had a bankruptcy or foreclosure in the past seven years? </p><br />
          <div className="row">
              <Link to="/wNine">
                <button value="Has never been in bankruptcy" onClick={ ( e ) => updateHistory( e.target.value ) }>No</button>
              </Link>

              <Link to="/wNine">
                <button value="Has had bankruptcy before" onClick={ ( e ) => updateHistory( e.target.value ) }>Bankruptcy</button>
              </Link>

              <Link to="/wNine">
                <button value="Has had a foreclosure before" onClick={ ( e ) => updateHistory( e.target.value ) }>Foreclosure</button>
              </Link>

              <Link to="/wNine">
                <button value="Has had both a foreclosure and a bankruptcy" onClick={ ( e ) => updateHistory( e.target.value ) }>Both</button>
              </Link>
          </div>
        </div>
      </div>
    )
  }
}

function mapStateToProps( state ) {
  const { history } = state;

  return {
    history
  };
}

export default connect( mapStateToProps, { updateHistory } )( WizardEight );
```

</details>

<details>

<summary> <code> src/components/WizardNine/WizardNine.js </code> </summary>

```js
import React,  { Component } from 'react';
import { Link } from 'react-router-dom';

import { connect } from 'react-redux';
import { updateAddress1, updateAddress2, updateAddress3 } from '../../ducks/reducer';

class WizardNine extends Component {
  render() {
    const { updateAddress1, updateAddress2, updateAddress3 } = this.props;

    return (
      <div className="parent-div">
        <div className="vert-align">
            <p>What is your address?</p> <br />

            <input type="text" placeholder="Line One" onChange={ ( e ) => updateAddress1( e.target.value ) } />
            <input type="text" placeholder="Line Two" onChange={ ( e ) => updateAddress2( e.target.value ) } />
            <input type="text" placeholder="Line Three" onChange={ ( e ) => updateAddress3( e.target.value ) } />
        
            <Link to="/wTen">
              <button className="margin-btn"> Next </button>
            </Link>
        </div>
      </div>
    )
  }
}

function mapStateToProps( state ) {
  const { addressOne, addressTwo, addressThree } = state;

  return {
    addressOne,
    addressTwo,
    addressThree
  };
}

export default connect( mapStateToProps, { updateAddress1, updateAddress2, updateAddress3 } )( WizardNine );
```

</details>

<details>

<summary> <code> src/components/WizardTen/WizardTen.js </code> </summary>

```js
import React,  { Component } from 'react';
import { Link } from 'react-router-dom';

import { connect } from 'react-redux';
import { updateFirst, updateLast, updateEmail } from '../../ducks/reducer';

class WizardTen extends Component {
  render() {
    const { updateFirst, updateLast, updateEmail } = this.props;

    return (
      <div className="parent-div">
        <div className="vert-align">
            <p>What is your name?</p> <br />

            <input type="text" placeholder="First Name" onChange={ ( e ) => updateFirst( e.target.value ) } />
            <input type="text" placeholder="Last Name" onChange={ ( e ) => updateLast( e.target.value ) } />
            <input type="text" placeholder="email" onChange={ ( e ) => updateEmail( e.target.value ) } />
            
            <Link to="/wEleven">
              <button className="margin-btn"> Next </button>
            </Link>
        </div>
      </div>
    )
  }
}

function mapStateToProps( state ) {
  const { firstName, lastName, email } = state;

  return {
    firstName,
    lastName,
    email
  };
}


export default connect( mapStateToProps, { updateFirst, updateLast, updateEmail } )( WizardTen );
```

</details>

## Contributions

If you see a problem or a typo, please fork, make the necessary changes, and create a pull request so we can review your changes and merge them into the master repo and branch.

## Copyright

© DevMountain LLC, 2017. Unauthorized use and/or duplication of this material without express and written permission from DevMountain, LLC is strictly prohibited. Excerpts and links may be used, provided that full and clear credit is given to DevMountain with appropriate and specific direction to the original content.

<p align="center">
<img src="https://devmounta.in/img/logowhiteblue.png" width="250">
</p>
