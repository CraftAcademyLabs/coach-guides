Start by creating a new React app and clean it up as usual.
```
yarn create react-app hello_world_redux_demo
```

Now we first want to make the simplest hello world possible. 
```
// src/App.jsx

import React from 'react';
const App = () => { {
  return (
    <>
      <h1>
        Hello World
      </h1>
    </>
  );
}
export default App;
```

From there, we will instead display Hello World from the value of a variable. 

```
const App = () => { {
  const message = 'Hello World from a variable'
  return (
    <>
      <h1>
        {message}
      </h1>
    </>
  );
}

```
Okey, that's peanuts. So let's achieve the same functionality from a React hook. 

```
const App = () => { {
  // const message = 'Hello World from a variable'
  const [message, setMessage] = useState('Hello world from hooked state')
  return (
    <>
      <h1>
        {message}
      </h1>
    </>
  );
}

```
Show also how we can put the string in our `message state` into a object where the value is stored in `greeting`. That will just lead us to say `{message.greeting}` in the return statement.
Just a way of displaying that we can pass in objects where we want to store a value and that only leads to the value being nested one level further down. But it doesn't increase the complexity of the code in anyway. 

OKey, but let's get our hands dirty with redux. 

```
yarn add redux react-redux
```

Now, we need to set up the stage by adding a few new folders and files. 
Make sure your folder structure looks like this: 

```
src/
├── App.jsx
├── index.js
├── serviceWorker.js
└── state
    ├── reducers
    │   └── rootReducer.js
    └── store
        ├── configureStore.js
        └── initialState.js
```

We will start with the `initialState.js`. 

```
// src/state/store/initialState.js

const initialState = {
  greeting: 'Hello World from application state'
}

export default initialState
```

lets stay in the `store` folder and continue with configuring our `configureStore.js`
```
// src/state/store/configureStore.js
import { createStore } from 'redux';
import rootReducer from '../reducers/rootReducer'

const configureStore = () => {
  return createStore(rootReducer);
}

export default configureStore
```

Now we can see that here we are importing and making use of a `rootReducer` that has now yet been created. Let's do that. 

```
// src/state/reducers/rootReducer.js
import initialState from '../store/initialState'

const rootReducer = (state = initialState) => {
  return state
}

export default rootReducer
```

We are still not yet there with the setup, we need to also connect to Redux. Let´s go to our `index.js`

```
// scr/index.js
import React from 'react';
import ReactDOM from 'react-dom';
import { Provider } from 'react-redux'
import configureStore from './state/store/configureStore';
import App from './App.jsx';
import reportWebVitals from "./reportWebVitals";

const store = configureStore();

window.store = store

ReactDOM.render(
  <Provider store={store}>
      <App />
  </Provider>,
  document.getElementById('root')
);

reportWebVitals();

```

Now, this won't change much for us if we spin up the application. But if we open up our developer tools and go to the console we can see some pretty amazing things already. 
In your console write `window.store.getState()`
Then you will see the object that is our `initialState` and the `greeting` with the value that we set earlier. 

So, we are connected, in theory. Let's put that into action in our `App` component to display the greeting from our application state. 

import React from 'react'
import { useSelector } from 'react-redux'

```
import React from 'react'
import { useSelector } from 'react-redux'

const App = () => {
  // const message = "Hello World from variable"
  // const [message, setMessage] = useState('Hello world from hooked state')
  const message = useSelector(state => state.greeting)
  return (
    <>
      <h1>{message}</h1>
    </>
  )
}
export default App
```

Et voila! We are now subscribing to the redux state through the `useSelector` hook and we are displaying the string that we have stored in there! 

Now we can play around with this to demonstrate that the initialState is an object like the object they are used to in a class component. If we add keys that contains an other object, then we can still access the value by the keys in that nested object. 