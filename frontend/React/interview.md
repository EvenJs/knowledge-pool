## Redux

### Q: What is Redux and why is it used in React applications?

> Redux is a predictable state management library used to manage the global state of a React application.  
> It provides a single source of truth (store), ensuring that all components share consistent data and making state changes traceable and easier to debug.

```javascript
// store.js
import { createStore } from "redux";

const initialState = { count: 0 };

function counterReducer(state = initialState, action) {
  switch (action.type) {
    case "INCREMENT":
      return { count: state.count + 1 };
    default:
      return state;
  }
}

const store = createStore(counterReducer);
export default store;
```

> React components can then connect to this store to read or modify the state.  
> **Why use it:** Centralized state management.  
> Predictable state updates via pure functions.  
> Time-travel debugging and middleware support (like redux-thunk for async).

### Q: Explain the three core principles of Redux.

> Single source of truth – The state of your app is stored in one object tree within a single store.  
> State is read-only – The only way to change the state is to dispatch an action, which describes what happened.  
> Changes are made with pure functions – Reducers are pure functions that take the previous state and an action, then return a new state.

### Q: What are actions and reducers in Redux?

> Actions are plain JavaScript objects that describe what happened.

```javascript
const addTodo = (text) => ({
  type: "ADD_TODO",
  payload: text,
});
```

> Reducers specify how the app’s state changes in response to actions.

```javascript
function todoReducer(state = [], action) {
  switch (action.type) {
    case "ADD_TODO":
      return [...state, action.payload];
    default:
      return state;
  }
}
```

> Reducers must be pure — they should not mutate state or perform side effects.

### Q: How do you handle asynchronous logic in Redux?

> Redux by itself only supports synchronous updates. For asynchronous operations (like API calls), we use middleware, such as redux-thunk or redux-saga.

```javascript
// Example (using redux-thunk):
// action
export const fetchUsers = () => async (dispatch) => {
  dispatch({ type: "FETCH_USERS_REQUEST" });
  const res = await fetch("/api/users");
  const data = await res.json();
  dispatch({ type: "FETCH_USERS_SUCCESS", payload: data });
};
```

> redux-thunk allows you to return a function from an action creator instead of an object, so you can handle side effects like async calls before dispatching the final action.

### Q: What are the advantages of using Redux Toolkit?

> Redux Toolkit (RTK) simplifies Redux development by reducing boilerplate and providing built-in best practices.  
> **Key features:**
>
> - configureStore() – automatically sets up Redux DevTools and thunk middleware
> - createSlice() – combines action creators and reducers in one
> - createAsyncThunk() – handles async requests easily

```javascript
import {
  createSlice,
  createAsyncThunk,
  configureStore,
} from "@reduxjs/toolkit";

export const fetchTodos = createAsyncThunk("todos/fetch", async () => {
  const res = await fetch("/api/todos");
  return res.json();
});

const todoSlice = createSlice({
  name: "todos",
  initialState: [],
  reducers: {},
  extraReducers: (builder) => {
    builder.addCase(fetchTodos.fulfilled, (state, action) => action.payload);
  },
});

const store = configureStore({ reducer: { todos: todoSlice.reducer } });
```

> Benefits: less boilerplate, integrated immutability, and improved developer experience

---

## Testing

### Q: How to test async code in React?

> Use await findBy... or waitFor.

```javascript
await waitFor(() => expect(screen.getByText("Loaded")).toBeInTheDocument());
```

### Q: What is snapshot testing?

> It ensures the UI doesn’t change unexpectedly by comparing rendered output with a stored snapshot.

```javascript
expect(container).toMatchSnapshot();
```

### Q: How do you mock API calls in tests?

> Use jest.mock() or mock service worker (MSW).

```javascript
jest.mock("./api", () => ({ getUsers: jest.fn() }));
```

### Q: How do you test custom hooks?

> Use renderHook from @testing-library/react.

```javascript
const { result } = renderHook(() => useCounter());
expect(result.current.count).toBe(0);
```
