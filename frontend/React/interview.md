## Hooks

### Q: What are React Hooks? List some commonly used Hooks

> Hooks are a feature introduced in React 16.8 that allow you to use state and other React features in functional components.  
> **Rules of hooks:**
>
> - Only call Hooks in functional components or custom Hooks
> - Only call Hooks at the top level, not inside loops, conditions, or nested functions

### Q: How does useState work in React?

> **How it works**
>
> - React stores state between re-renders
> - When setState is called, component re-renders
> - React preserves state value across renders
> - Each render gets its own state snapshot

> **Important notes**
>
> - State updates are asynchronous
> - State updates trigger re-renders
> - Cannot call useState conditionally
> - State is isolated to each component instance

### Q: What is useEffect and its purpose?

> useEffect handles side effects in functional components (data fetching, subscriptions, DOM manipulation).

> **Purpose**
>
> - Replace lifecycle methods (componentDidMount, componentDidUpdate, componentWillUnmount)
> - Handle side effects outside of render
> - Keep side effects synchronized with component state

### Q: What is a Custom Hook?

> A custom hook is a reusable JavaScript function that uses React hooks and follows the naming convention "use" prefix.

> **Purpose**
>
> - Extract and reuse component logic
> - Share stateful logic between components
> - Keep components clean and focused
> - Avoid code duplication

> **Benefits**
>
> - Code reusability across components
> - Separation of concerns
> - Easier testing
> - Cleaner component code
> - Share logic without HOCs or render props
> - Composable (hooks can use other hooks)

> **When to Create Custom Hooks:**
>
> - Logic is used in multiple components
> - Complex stateful logic needs extraction
> - Combining multiple hooks for specific functionality
> - Abstracting side effects

> **Best Practices:**
>
> - Always start name with "use"
> - Keep hooks focused and single-purpose
> - Document parameters and return values
> - Return objects for multiple values (easier to extend)
> - Handle cleanup in useEffect
> - Make hooks testable

## Q: What rules do you have to follow when using hooks?

React hooks have specific rules that must be followed to ensure they work correctly. These rules are enforced by the eslint-plugin-react-hooks linter plugin. Keep hooks at the top of your component

> **Rule 1: Only Call Hooks at the Top Level**  
> Never call hooks inside loops, conditions, or nested functions. Hooks must be called in the same order on every render to maintain their internal state correctly.
>
> **Rule 2: Only Call Hooks from React Functions**  
> Hooks can only be called from:
>
> > React function components  
> > Custom hooks (functions starting with "use")
>
> Never call hooks from:
>
> > Regular JavaScript functions  
> > Class components  
> > Event handlers (unless inside a function component)
>
> **Rule 3: Custom Hooks Must Start with "use"**  
> This naming convention allows React and linters to identify hooks and enforce the rules of hooks.  
> **Rule 4: Complete Dependency Arrays**  
> Always include all values from the component scope that change over time and are used by the effect in the dependency array.  
> **Rule 5: Don't Call Hooks Conditionally**  
> Hooks should always be called, even if their behavior is conditional

### Q: How do Hooks work in React?

> React maintains a list of hooks for each component using a linked list:  
> Component renders → React tracks hooks in order → Stores values in memory

```javascript
const Component = () => {
  const [count, setCount] = useState(0);
  const [name, setName] = useState("");

  useEffect(() => {}, [count]);
};
```

> React tracks: [useState(0), useState(""), useEffect(...)]

> **Benefits of Hooks:**
>
> - Reuse stateful logic without changing component hierarchy
> - Split complex components into smaller functions
> - Use state without classes
> - Easier to understand than lifecycle methods
> - Better code organization
> - Improved code reusability

> **Hook Flow:**
>
> 1. Component function runs
> 2. Hooks execute in order
> 3. React stores hook values
> 4. Component returns JSX
> 5. On re-render, React retrieves stored hook values
> 6. Hooks execute again in same order  
>    Key: Hooks must be called in the same order on every render!

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
