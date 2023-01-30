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

| React Redux | Redux  |
| ------------ | ------------ |
| Better code organization with separate UI logic and State Management Logic  | UI logic and State Management Logic are in the same component  |
| Debugging can be hard in highly nested React Component Structure even with Dev Tool	  | Incredibly powerful Redux Dev Tools to ease debugging  |
| Built-in tool with React | Additional installation Required  |
| It re-renders all components whenever there is any update in the provider’s value prop.  | It only re-render the updated components.|

 ## 7) What is Babel in ReactJS?

 - Babel is transpiler that basically allows us convert the latest version of JavaScript code into the one that the browser understands.
 - It compile JSX into vanilla JavaScript

## 8) What are pure components in React?


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
