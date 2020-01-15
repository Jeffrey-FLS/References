# Setting up Redux in React

### Step 1 - Install Redux and React Redux with 

```bash
npm install redux --save
npm install react-redux --save
```



### Step 2 - Run the script template below in the root directory in order to create the required directories to start Redux

```bash
mkdir -p src/redux/{actions,constants,reducers,services} &
touch src/redux/actions/index.js &
touch src/redux/constants/index.js &
touch src/redux/reducers/index.js &
touch src/redux/services/index.js &
touch src/redux/store.js 
```



### Step 3 - Create a constants file within the constants directory in order to start laying out the actions needed to mutate (change) state within the app. Constants is like a mapping template for the actions (functions) that will be used within every component and desired change in state, laying out the architecture of what will be used (build) in redux. Besides setting layouts, constants help by keeping the same action name within the actions and reducers file; and will be able to speed up the development process with the help of IntelliSense by auto completing the constants actions whenever you start typing a constant, therefore avoiding any errors.  

### In this example I'm going to create a like / dislike button with the a default amount of likes for redux testing. Therefore, I'm going to create a `test.constants.js` file 

```js
// src/redux/constants/test.constants.js

export const testConstants = {
    LIKE: 'LIKE',
    DISLIKE: 'DISLIKE',
};
```

### Now withing the constants directory there is an `index.js` file to export all constant files that live within that directory, and assign this export

```js
// src/redux/constants/index.js
export * from './test.costants';
```



### Step 4 - Lets create the actions file in order to set the logic function behind every action constants listed

```js
// src/redux/actions/test.actions.js
import { testConstants } from "../constants";

export function addLike(){
    return {type: testConstants.LIKE}
}
export function removeLike(){
    return {type: testConstants.DISLIKE}
}
```

### The actions file is used as function guides in react components and then compute the directed values to then be sent to the reducers (which will be in the next step)  to process the final value for the state change 

### Now just like constant directory have an `index.js` file for concatinating all file within that directory, so does the actions folder. Which will then serve as a point in location for when called inside the components

```js
// src/redux/actions/index.js
export * from './test.actions';
```



### Step 5  -  Now lets the create the final step process of changing the state using reducers. First import the constants needed to set the actions. After define the default values of state, whether that'd be in an initialState value file or within the reducer file

```js
// src/redux/reducers/test.reducer.js
import { testConstants } from "../constants";

const defaultState = {
    likes: 2000,
    text: ""
};

function reducer(prevState = defaultState, action){
    switch(action.type){
        case testConstants.LIKE:
            return {...prevState, likes: prevState.likes + 1};
        case testConstants.DISLIKE:
            return {...prevState, likes: prevState.likes - 1};
        case testConstants.CHANGE_TEXT:
            return {...prevState, [action.payload.name]: action.payload.newText};
        default:
            return prevState
    }
}

export default reducer;
```

### The reducer file will be waiting for the action calls in the components, to then receive the values from the components (if any) in order to make the assigned changes as a new state value

### To finish up in reducers, lets export the reducers directory in `index.js`, with the difference of combining all of the present reducers into one reducer, using the  combineReducers component from redux. Whenerver the application grows with more reducers, import the reducer and assign it within the combineReducers function

```js
// src/redux/reducers/index.js
import { combineReducers } from 'redux';
import { testReducer } from './test.reducer'

const rootReducer = combineReducers({
    testReducer
});

export default rootReducer;
```



### Step 6 - Now that we have the actions and reducers set, lets create a store file which will have the state values and functions (like dispatch) to utilize the action calls and render its functions returns inside the reducers

```js
// src/redux/store.js

import { createStore } from 'redux';
import rootReducer from "../redux/reducers";

const store = createStore(rootReducer);

export default store;
```

### Inside the `src/index.js` file, import Provider and wrap it around App component or Router Component if present. Afterwards import the store and create the prop values in Provider with the name of store assigned to the imported store value in order to obtain its states and reducers in all components within the app

```jsx
// src/index.js

// React Components
import React from 'react';
import ReactDOM from 'react-dom';
import * as serviceWorker from './serviceWorker';
import {BrowserRouter as Router, Route} from 'react-router-dom';
import store from './redux/store';
import {Provider} from 'react-redux';

// Assets
import './styles/index.scss';

// Components
import App from './app/App';

ReactDOM.render(
    <Provider store={store}>
        <Router>
            <Route path="/" component={App}/>
        </Router>
    </Provider>,
    document.getElementById('root')
);

// If you want your app to work offline and load faster, you can change
// unregister() to register() below. Note this comes with some pitfalls.
// Learn more about service workers: https://bit.ly/CRA-PWA
serviceWorker.unregister();

```



### Step 7 - Now that we have all of the redux done, lets incorporate it inside the components

```js
// src/app/components/HomePage.component.js

// React Components
import React, {Component} from 'react';
import { connect } from 'react-redux';

// Assets
import './LoginPage.component.scss';
import {FaUserAlt} from 'react-icons/fa';
import {FaLock} from 'react-icons/fa';
import {FaFacebookF} from 'react-icons/fa';
import {FaGoogle} from 'react-icons/fa';

// Redux Actions
import { addLike, removeLike, changeText } from "../../../redux/actions";

class HomePage extends Component {

    fetchUser = (username, password) => {
        // fetch('http://localhost:3000/api/v1/users')
    };

    render() {
        return (
            <div className="loginPage">
                <header className="login_-_header_--_loginPage"><h1>Quizzzity</h1></header>

                <div className="container">
                    <div className="row">

                    <div className="login col-12 col-sm-8 col-md-6 col-lg-5">
                    <div className="login_-_body">
                        <div className="login_-_title">
                            <h1>Login</h1>
                        </div>

                        <form action="" className="login_-_form">
                            <label htmlFor="username"><FaUserAlt/></label>
                            <input type="text" id="username"
                                   placeholder="Username"/>

                            <label htmlFor="password"><FaLock/></label>
                            <input type="password" id="password"
                                   placeholder="Password"/>

                            <div className="login_-_form_--_remember-forgot">
                            <label className="checkbox-container" htmlFor="remember">Remember
                                <input type="checkbox" name="remember"/>
                                <span className="checkmark"/>
                            </label>

                                <a href="#">Forgot Password?</a>
                            </div>

                            <br/>

                            <div className="login_-_form_--_buttons">
                                <input type="submit" value="Sign-In"/>

                                <div className="login_-_form_--_buttons--social-links">
                                    <button onClick={this.props.addLike}><FaFacebookF/></button>
                                    <h1>{this.props.likes}</h1>
                                    <button onClick={this.props.removeLike}><FaGoogle/></button>
                                </div>
                            </div>
                        </form>
                    </div>
                    </div>
                </div>

                <div className="login_-_breakline">
                    <h3>OR</h3>
                </div>

                <div className="login_-_create-new">
                    <button>Create New Account</button>
                </div>

                    <input name="text" value={this.props.text} onChange={this.props.changeText}/>
                    <h1>{this.props.text}</h1>

                </div>
            </div>
        )
    }
}


function msp(state){
    return {
        likes: state.testReducer.likes,
        text: state.testReducer.text
    }
}

const mdp = {
    addLike,
    removeLike,
    changeText
};


export default connect(msp, mdp)(LoginPage);

```





### References :

#### [React Redux Site](https://redux.js.org/introduction/installation/)