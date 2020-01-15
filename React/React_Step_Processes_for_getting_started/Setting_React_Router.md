# Setting React Router

### Step 1 - To install the react router module, run `npm install react-router-dom`

### Step 2 - Set React Router at the root file in index.js by importing react router and wrapping App Component with Router

```jsx
// React Components
import React from 'react';
import ReactDOM from 'react-dom';
import * as serviceWorker from './serviceWorker';
import { BrowserRouter as Router, Route } from 'react-router-dom';

// Assets
import './styles/index.scss';

// App Components
import App from './app/App';

ReactDOM.render(
    <Router>
        <Route path="/" component={App} />
    </Router>,
    document.getElementById('root')
);

// If you want your app to work offline and load faster, you can change
// unregister() to register() below. Note this comes with some pitfalls.
// Learn more about service workers: https://bit.ly/CRA-PWA
serviceWorker.unregister();
```



### Step 3 - Import Route and Switch from react-router-dom, and wrap the destined Routes with Switch

```jsx
// React Components
import React, { Component } from 'react';
import { Switch, Route, withRouter } from "react-router-dom";

// Assets
import './App.scss';

// App Components
import UserMenuPage from "./pages/userMenu/UserMenuPage.component";

class App extends Component {

    state = {
        loginPage: true,
        quizzes: []
    };

    componentDidMount() {
        fetch('http://localhost:3000/api/v1/quizzes')
            .then(response => response.json())
            .then(data => {
                // debugger
                this.setState({
                    quizzes: data
                });
            }).catch(console.error);
    }


    render() {
        return (
        <div className="App">
          <Switch>
            <Route path="/userMain" render={(routerProps) => <UserMenuPage quizzes={this.state.quizzes} {...routerProps}/>}/>
            <Route path="/" component={LoginPage}/>
          </Switch>
        </div>
    );
  }
}

export default App;

```



### Step 4 - Using Links



### References : 

#### [React Router Website](https://reacttraining.com/react-router/web/guides/quick-start) 