# React Evaluation 3

## 1) What is Redux?

- Redux is an open-source JavaScript library for managing and updating application state.
-  A single centralized store for state that needs to be used across your entire application.

**Example**
App.js
```javascript
import React from 'react';
import Login from './component/Login';
import Profile from './component/Profile';

function App() {
  return (
    <div className="App">
      <Profile />
      <Login />
    </div>
  );
}

export default App;

```

user.js
```javascript
import { createSlice } from '@reduxjs/toolkit'
export const userSlice = createSlice({
        name:"user",
        initialState: {value:{username:"",password:""}},
        reducers:{
            login(state,action){
                state.value = action.payload
            },
            logout(state){
                state.value = {username:"",password:""}
            }
        }
    })

export default userSlice.reducer
export const {login,logout} = userSlice.actions
```

Login.js

```javascript
import React, { useState } from 'react'
import { useDispatch } from 'react-redux'
import user, { login,logout } from '../features/user'
function Login() {
    const [userName,setUserName] = useState("")
    const [password,setPassword] = useState("")
    const dispatch = useDispatch()
  return (
    <div>
        <input type="text" id="username" value={userName} onChange={(e) => setUserName(e.target.value)} />
        <input type="password" id="password" value={password} onChange={(e) => setPassword(e.target.value)} />
        <button onClick={() => dispatch(login({username:userName,password:password}))}>Login</button>
        {
            user.username &&         <button onClick={() => dispatch(logout())}>Logout</button>
        }

    </div>
  )
}

export default Login
```

Profile.js

```javascript
import React from 'react'
import { useSelector } from 'react-redux'

function Profile() {
    const user = useSelector(state => state.user.value)
    if(!user.username){
        return
    }
  return (
    <div>
        <div>
            <p>Username: {user.username}</p>
            <p>Password: {user.password}</p>
        </div>
    </div>

  )
}

export default Profile
```

## 2) What is Redux in React js?

- React Redux is the official React UI bindings layer for Redux. It allows React components  to read data from a Redux store, and dispatch Actions to the Store to update state.

- It subscribes to the Redux store, checks to see if the data which your component wants have changed, and re-renders your component.

- The components of Redux architecture
	- **Store**
		A store is a place where the entire state of your application lists.
		
	- **Action**
	The actions that occur in the app based on user input, and trigger updates in the state
	
	- **Reducer**
	Reducer read the payloads from the actions and then updates the store via the state accordingly. It is a pure function to return a new state from the initial state.
	
## 3) What are the advantages of using Redux?

**Advantages**

1. **Centralized state management system:**
	Redux state is stored globally in the store. All the components of the entire application can easily access the data directly.
2.  **Performance Optimizations:**
	Redux store helps in improving the performance by skipping such unnecessary re-renders and ensuring that a given component re-renders only when its data has actually changed.
3. **Persist Data Long**
	Data stored in redux persists until page refresh, it is widely used to store long-term data that is required while the user navigates the application.
4. **Community Support**
	Redux has a large community of users. This makes it easier to ask for help.
5. **Time-Travel Debugging**
Redux logs all actions and states over time, It is simple to trace any bugs that emerge. You can also use Redux DevTools, Whic allows you to skip backwards and forwards in time to inspect the state of the application at any point. DevTools include a number of other powerful features that can maximize the usefulness of Redux.

## 4) Is it true that Redux can only be used with React?

No, You can use Redux with differenet frameworks and libraries such as Angular, React or Vue etc.

## 5) What do you understand about Redux Toolkit?

Redux Toolkit is a set of tools that helps simplify Redux development. It includes utilities for creating and managing Redux stores, as well as for writing Redux actions and reducers. The Redux team recommends using Redux Toolkit anytime you need to use Redux.

## 6) Differentiate between React Redux and React's Context API.

| React Context API | React Redux  |
| ------------ | ------------ |
| Better code organization with separate UI logic and State Management Logic  | UI logic and State Management Logic are in the same component  |
| Debugging can be hard in highly nested React Component Structure even with Dev Tool	  | Incredibly powerful Redux Dev Tools to ease debugging  |
| Built-in tool with React | Additional installation Required  |
| It re-renders all components whenever there is any update in the provider’s value prop.  | It only re-render the updated components.|

 ## 7) What is Babel in ReactJS?

 - Babel is transpiler that basically allows us convert the latest version of JavaScript code into the one that the browser understands.
 - It compile JSX into vanilla JavaScript

## 8) What are pure components in React?

- ReactJS Pure Component Class compares current state and props with new props and states to decide whether the React component should re-render itself or Not.
- Pure components have some performance improvements and render optimizations since React implements the shouldComponentUpdate() method for them with a shallow comparison for props and state.

```javascript
import React, { PureComponent } from "react";

class PureClassComponent extends PureComponent {
  constructor() {
    super();
    this.state = {
      courseName: "React JS"
    };
  }

  changeCourseName = () => {
    this.setState({ courseName: "React JS" });
  };

  render() {
    console.log("PureComponent -- Render method called");
    return (
      <div>
        <p> Course Name is : {this.state.name} </p>
        <button onClick={this.changeName}>Change CourseName</button>
      </div>
    );
  }
}
export default PureClassComponent;
```
## 9) What is children prop?

The children prop is used to pass the data from the parent component to the children component but this data must be enclosed within the parent's opening and closing tag.

**Example**
App.js
```javascript
import  Button from "./Button"
import Card from "./Card"

function App() {
	return (
	<div>
		<Button>Click</Button>
	</div>
	)
}

export default App;
```

Button.js
```javascript
function Button(props) {
	return (
	<div>
		<button>{props.children}</button>
	</div>
	)
}

export default Button;
```

## 10) Why you can't update props in React?

The props should be immutable and top-down. This means that a parent can send whatever prop values it likes to a child, but the child cannot modify its own props.

## 11) Redux toolkit

###  What is redux Provider?

The Provider component makes the Redux store available to any nested components that need to access the Redux store.

**Example**

```javascript
import React from "react";
import { createRoot } from "react-dom/client";
import { Provider } from "react-redux";
import { persistor, store } from "./app/store";
import { PersistGate } from "redux-persist/integration/react";

import App from "./App";
import "./index.css";
import "bootstrap/dist/css/bootstrap.min.css";
import "bootstrap/dist/js/bootstrap.bundle.min";

const container = document.getElementById("root");
const root = createRoot(container);

root.render(
  <React.StrictMode>
    <Provider store={store}>
      <PersistGate loading={null} persistor={persistor}>
        <App />
      </PersistGate>
    </Provider>
  </React.StrictMode>
);

```

### What is createSlice?

A function that accepts an initial state, an object of reducer functions, and a "slice name", and automatically generates action creators and action types that correspond to the reducers and state.

Internally, it uses createAction and createReducer.

#### Parameters
createSlice accepts a single configuration object parameter, with the following options:

**name**
A string name for this slice of state.

**initialState**
The initial values for reducers.

**reducers**
It's an object where the keys will become action type strings, and the functions are reducers that will be run when that action type is dispatched.

**Example**

```javascript
import { createSlice } from '@reduxjs/toolkit'

const initialState = { value: 0 }

const counterSlice = createSlice({
  name: 'counter',
  initialState,
  reducers: {
    increment(state) {
      state.value++
    },
    decrement(state) {
      state.value--
    },
  },
})

export const { increment, decrement } = counterSlice.actions
export default counterSlice.reducer
```

### What is extraReducers?

The extraReducers allows you to respond to an action in your slice reducer but does not create an action creator function.

The most common examples are responding to a createAsyncThunk action and responding to an action from another slice.

The extraReducers property in createSlice can be used as a function or as an object.

#### Parameters

**builder**
The builder have a case function.
	builder.addCase
	builder.addDefaultCase

If you create an action using createAsyncThunk function. You can handle loading, success & failure states.

**Example**

```javascript
const fetchUserById = createAsyncThunk(
  'users/fetchByIdStatus',
  async (userId, thunkAPI) => {
    const response = await userAPI.fetchById(userId)
    return response.data
  }
)

const {actions,reducer} = createSlice({
  name:'users',
  reducers:{
  },
  initialState:,
  extraReducers: (builder) => { builder.addCase(fetchUserById.pending, (state, action) => {
      state.loading=true;
      state.whoseDataIsLoading = action.payload;
    })
  }
});
```

1. fetchUserById.pending (handles loading state of the asyncThunk).
2. fetchUserById.rejected (handles failed state).
3. fetchUserById.fulfilled (handle success state).


### What is useSelector?

Allows you to extract data from the Redux store state.

#### Parameters

**selector**
It is a function argument that returns the part of the state you want.
**equalityFn**
It is a function used for custom equality.

**Example**

```javascript
import React from 'react'
import { useSelector } from 'react-redux'

export const CounterComponent = () => {
  const counter = useSelector((state) => state.counter)
  return <div>{counter}</div>
}

```

### What is useDispatch?

The useDispatch hook gives us access to our store's dispatch method. Dispatch is used to send actions into our redux store and is the only way we can affect the store from within a component.

**Example**

```javascript
import React from 'react'
import { useDispatch } from 'react-redux'

export const CounterComponent = ({ value }) => {
  const dispatch = useDispatch()

  return (
    <div>
      <span>{value}</span>
      <button onClick={() => dispatch({ type: 'increment-counter' })}>
        Increment counter
      </button>
    </div>
  )
}

```

### What is configureStore?

configureStore() wraps around the Redux library’s createStore() method and the combineReducers() method, and handles most of the store setup for us automatically.

#### Parameters

configureStore accepts a single configuration object parameter.

**reducer**

A single reducer function that will be used as the root reducer, or an object of slice reducers that will be passed to combineReducers()

**middleware**

An array of Redux middleware to install. If not supplied, defaults to
 the set of middleware returned by getDefaultMiddleware().

 **devTools**

 Whether to enable Redux DevTools integration. Defaults to true.
Additional configuration can be done by passing Redux DevTools options.

**preloadedState**

The initial state, same as Redux createStore.

**enhancers**

An enhancer is a function that allows you to add functionality to Redux that it doesn't come with out of the box.

An enhancer is a function that gets a copy of createStore and then a copy of all of the arguments passed to createStore before actually passing them to createStore. This allows you to create libraries and plugins that will augment how the store works.

**Example**

```javascript
import { configureStore } from '@reduxjs/toolkit'

import rootReducer from './reducers'

const store = configureStore({ reducer: rootReducer })
```

### What is thunk?

The word "thunk" is a programming term that means "a piece of code that does some delayed work". Rather than execute some logic now, we can write a function body or code that can be used to perform the work later.

Redux Thunk is a middleware that allows you to call the action creators that return a function(thunk) which takes the store’s dispatch method as the argument and which is afterwards used to dispatch the synchronous action after the API or side effects has been finished.

**Example**

```javascript
function getCartItems() {
	return async function (dispatch) => {
	const cartItems =  await fetch("API");
	if(cartItems) 
		dispatch({
			type: CART_ITEMS,
			payload: cartItems.json()
		})
}
}
```

## 12) redux-persist

### What is PersistGate?

PersistGate delays the rendering of your app's UI until your persisted state has been retrieved and saved to redux.
The loading prop can be null or any react instance to show during loading (e.g. a splash screen), for example loading={<Loading />}.

**Example**

```javascript
import React from "react";
import { createRoot } from "react-dom/client";
import { Provider } from "react-redux";
import { persistor, store } from "./app/store";
import { PersistGate } from "redux-persist/integration/react";

import App from "./App";
import "./index.css";
import "bootstrap/dist/css/bootstrap.min.css";
import "bootstrap/dist/js/bootstrap.bundle.min";

const container = document.getElementById("root");
const root = createRoot(container);

root.render(
  <React.StrictMode>
    <Provider store={store}>
      <PersistGate loading={null} persistor={persistor}>
        <App />
      </PersistGate>
    </Provider>
  </React.StrictMode>
);

```

### What is persistStore?

persistStore is the function that persists and rehydrates the state. With this function, our store will be saved to the local storage, and even after a browser refresh, our data will still remain.

#### Parameters

**store**
store redux store The store to be persisted.

**Example**

```javascript
import { persistStore } from 'redux-persist';
import { PersistGate } from 'redux-persist/integration/react';
import store from "../store".
let persistor = persistStore(store);

ReactDOM.render(
    <React.StrictMode>
        <Provider store={store}>
            <PersistGate persistor={persistor}>
                <App />
            </PersistGate>
        </Provider>
    </React.StrictMode>,
    document.getElementById('root')
);

```

### What is persistReducer?

persistReducer returns an enhanced reducer that wraps the rootReducer you pass in and will persist that reducer's state according to the config you pass in.

#### Parameters

**config**
It is a configuration object as its first parameter. You must specify the key and storage properties.

**reducer**
It accept a reducer.

**Example**

```javascript
import { configureStore } from "@reduxjs/toolkit";
import userReducer from "./slices/userSlice";
import storage from 'redux-persist/lib/storage';
import { persistReducer, persistStore } from 'redux-persist';
import thunk from 'redux-thunk';

const persistConfig = {
  key: 'root',
  storage,
}

const persistedReducer = persistReducer(persistConfig, userReducer)
```


## 13) redux-storage

### What is storage?

storage defines the storage engine to use. Redux Persist supports multiple different storage backends depending on the environment. For web use, the localStorage and sessionStorage APIs are both supported as well as basic cookies. Options are also available for React Native, Node.js, Electron and several other platforms.

**Example**
localStorage
```javascript
// src/redux/store.js
import { configureStore } from "@reduxjs/toolkit";
import storage from 'redux-persist/lib/storage';
import { persistReducer, persistStore } from 'redux-persist';
const persistConfig = {
  key: 'root',
  storage,
}
```

Session
```javascript
// src/redux/store.js
import { configureStore } from "@reduxjs/toolkit";
import storageSession from 'reduxjs-toolkit-persist/lib/storage/session'
import { persistReducer, persistStore } from 'redux-persist';
const persistConfig = {
  key: 'root',
  storageSession,
}
```


