## Context API Example

## Introduction

Context API is used to pass global variables anywhere in the code. It helps when there is a need for sharing state between a lot of nested components. It prevents prop drilling and the need to use Redux.

There is no need to install any third party libraries as it comes with React 16+ and it is very light weight and simple to use.

# Usage

First import react, createContext, useState

```javascript
import React, { createContext, useState } from "react";
```

Create the context normally in Context.js module along with provider and consumer

```javascript
const UserContext =React.createContext(); 
export const Provider = UserContext.Provider;
export const Consumer = UserContext.Consumer;

```

In your component consume the context, for example, this is a component called WelcomePage which consumes the value object:

```javascript
import React from "react";
import { Consumer } from "./Context";
  
const WelcomePage = () => {
    return (
        <div>
            <h1>Welcome User :</h1>
            <Consumer>
                {(value) => (
                    <h2>
                        Name: {value.name} id :{value.id}{" "}
                    </h2>
                )}
                //this function takes the value as prop
            </Consumer>
        </div>
    );
};
  
export default WelcomePage;
```

In your index.js where your root component is rendered, create the component and pass value object across to it:

```javascript
import {Provider} from './Context'
  
ReactDOM.render(
  <Provider value={{name:"Geeksforgeeks", id:195}}>
    <App />
  </Provider>,
  document.getElementById('root')
);
```

and in App.js:

```javascript
import WelcomePage from "./WelcomePage";
  
function App() {
  return (
    <div className="App">
       <WelcomePage/>      // will have access to the value object
    </div>
  );
} 
export default App;
```

From this, we can conclude that he value object is now 'global' and can be used in the App components render - thus in the App component any component has access to the value object, in this example, that is the WelcomePage component.

The example source in this project does something similar, it passes from an input box the value entered to a NotesContext component which then renders this in a list item in the App component.




