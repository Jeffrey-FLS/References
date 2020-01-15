# Define PropTypes and Set Default Prop Values

### Step 1 - Install propTypes and set as dev-dependency `npm i prop-types --save-dev`

### Step 2 - There are two methods to implement in class propTypes, the first is by static methods within the class and the second is declaring the method outside of the class. And one way to set up Function propType Components

```jsx
import React from "react";
import PropTypes from 'prop-types';

class BotCollection extends React.Component {

    static defaultProps = {
        bots: []
    };

	// Implementation
    static propTypes = {
        bots: PropTypes.array
    };

    render() {
        <div></div>
    }
};

export default BotCollection;

```

### Setting the value outside the class 

```jsx
import React from "react";
import PropTypes from 'prop-types';

class BotCollection extends React.Component {
    
    static defaultProps = {
        bots: []
    };

    render() {
        <div></div>
    }
};

// Implementation
BotCollection.propTypes = {
	bots: PropTypes.array
};

export default BotCollection;

```

### Setting the value within a function component

```jsx
import React from "react";
import PropTypes from 'prop-types';

const BotCollection = () => {
    return(
        <div></div>
        );
};

// Implementation
BotCollection.propTypes = {
	bots: PropTypes.array
};

export default BotCollection;
```

### Step 3 - Setting default props follows the same pattern for both in class and functional components. With the difference of calling defaultProps instead of propTypes, with its default value

```jsx

// In class Component
static defaultProps = {
    bots: []
};

// Outside Class and Functional Component
BotCollection.defaultProps = {
	bots: []
};
```



### References:

#### [React PropType](https://reactjs.org/docs/typechecking-with-proptypes.html)

#### [Validating React component props with prop-types](https://blog.logrocket.com/validating-react-component-props-with-prop-types-ef14b29963fc/)

