# Redux
[Quick start](https://redux-toolkit.js.org/tutorials/quick-start)

# install in repo
```
yarn add @reduxjs/toolkit react-redux
```

# Create Store
```ts
import { configureStore } from '@reduxjs/toolkit'

export const store = configureStore({
  reducer: {},
})

// Infer the `RootState` and `AppDispatch` types from the store itself
export type RootState = ReturnType<typeof store.getState>
// Inferred type: {posts: PostsState, comments: CommentsState, users: UsersState}
export type AppDispatch = typeof store.dispatch
```

# Provide Store to React App

index.tsx
```TS
import React from 'react';
import ReactDOM from 'react-dom';
import './index.css';
import App from './App';

import { store } from './todo-redux/todo.store';
import { Provider } from 'react-redux';

ReactDOM.render(
  <React.StrictMode>
    <Provider store={store}>
      <App />
    </Provider>    
  </React.StrictMode>,
  document.getElementById('root')
);
```

# Create main Functionality page

1. create state
2. create initialStata
3. create slice (reducer parent?)

```TS
import { createSlice, PayloadAction } from '@reduxjs/toolkit'
import { ToDo } from '../models/todo.model'

export interface ToDoState {
  todos: ToDo[];
}

const initialState: ToDoState = {
    todos: [
        {
          descrition: 'do the chores',
          done: false
        },
        {
          descrition: 'make bed',
          done: false
        },
        {
          descrition: 'feed cat',
          done: true
        }
    ]
}

export const todoSlice = createSlice({
  name: 'todo',
  initialState,
  reducers: {
    toggleToDo: (state, action: PayloadAction<ToDo>) => {
        state.todos.filter(todo => {
            return todo.id === action.payload.id;
        })[0].done = !action.payload.done;
    },
    addNewToDo: (state, action: PayloadAction<ToDo>) => {
        state.todos = [...state.todos, action.payload];
    }
  },
})

// Action creators are generated for each case reducer function
export const { addNewToDo, toggleToDo } = todoSlice.actions

export default todoSlice.reducer
```

# Add reducer to store
```TS
import { configureStore } from '@reduxjs/toolkit'
import todoReducer from './toto.slice' <--

export const store = configureStore({
    reducer: {
        todo: todoReducer <--
    },
})

// Infer the `RootState` and `AppDispatch` types from the store itself
export type RootState = ReturnType<typeof store.getState>
// Inferred type: {posts: PostsState, comments: CommentsState, users: UsersState}
export type AppDispatch = typeof store.dispatch
```

# Us in App

```TS
import { addNewToDo, toggleToDo as toggleToDoAction } from './todo-redux/toto.slice';

function App() {
  const todos = useSelector((state: RootState) => state.todo.todos);
  const dispatch = useDispatch();

  const onAddNewTodo = (todo: ToDo): void => {
    dispatch(addNewToDo(todo));
  }

  const toggleToDo = (todo: ToDo): void => {
    dispatch(toggleToDoAction(todo)); 
  }

  [...]
```