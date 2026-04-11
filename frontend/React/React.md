# React

#### What is React?

- A JavaScript library for building UI
- Component-based, declarative
- Uses Virtual DOM for efficient updates

#### Component

- A JavaScript function that you can sprinkle with markup.
- Class component
- Function components

#### State

- React components use props to communicate with each other. Parent component can pass some information to its child components by give them props.
- State is component's menory

---

## Hooks

#### useState

`useState` is a React Hook that lets you add a **State** variable to your component.

```typescript
const [state, setState] = useState(initialState);
```

#### useId

`useId` is a React Hook for generating unique IDs that can be passed to accessibility attributes.

```typescript
const id = useId()

// example
import { useId } from 'react';

function PasswordField() {
  const passwordHintId = useId();
```

### useEffect

`useEffect` is a React Hook that lets you synchronize a component with an external system.

> ```typescript
> useEffect(setup, dependencies?)
> // setup: function that runs your side effect
> // dependencies: array of values React watches
> ```

```typescript
import { useState, useEffect } from "react";
import { createConnection } from "./chat.js";
function ChatRoom({ roomId }) {
  const [serverUrl, setServerUrl] = useState("https://localhost:1234");

  useEffect(() => {
    const connection = createConnection(serverUrl, roomId);
    connection.connect();
    return () => {
      connection.disconnect();
    };
  }, [serverUrl, roomId]);
  // ...
}
```

### useEffectEvent

`useEffectEvent` is a React hook that lets you define **event handlers that read the latest props/state without stale closures**, _without needing to recreate the handler on every render_, and _without re-wiring effects/listeners_ repeatedly.

```typescript
const onEvent = useEffectEvent(callback)
//callback: A function containing the logic for your Effect Event. The function can accept any number of arguments and return any value. When you call the returned Effect Event function, the callback always accesses the latest committed values from render at the time of the call.


// example
function App() {
  const [count, setCount] = useState(0);

  const handleClick = useEffectEvent(() => {
    console.log("Latest count:", count);
  });

  return <button onClick={handleClick}>Click</button>;
}
```

### useRef

`useRef` is a React Hook that lets you reference a value that’s not needed for rendering.

```typescript
const ref = useRef(initialValue);

ref = { current: initialValue };
```

> It’s commonly used for two main purposes:
>
> 1. Accessing DOM elements
>
> ```typescript
> function InputFocus() {
>  const inputRef = useRef(null)
>
>  function handleFocus() {
>    inputRef.current.focus()
>  }
>
>  return (
>   <>
>     <input ref={inputRef} />
>    <button onClick={handleFocus}>Focus</button>
>  </>
>  )
> }
>
> // inputRef.current is the real DOM <input> element.
> ```
>
> 2. Persisting mutable state without triggering re-renders
>
> ```typescript
> function Timer() {
>   const countRef = useRef(0)
>
>   useEffect(() => {
>     const id = setInterval(() => {
>       countRef.current++
>       console.log(countRef.current)
>     }, 1000)
>
>     return () => clearInterval(id)
>   }, [])
>
>   return <div>Look at the console</div>
> }
>
> // countRef.current updates, but React never rerenders the component.
>
> // This avoids unnecessary UI updates.
> ```

### useMemo

`useMemo` is a React Hook that lets you cache the result of a calculation between re-renders.

```typescript
const cachedValue = useMemo(calculateValue, dependencies);

// example
const sortedList = useMemo(() => sort(items), [items]);
// If items doesn’t change, React returns the previous sorted result.
```

> **When useMemo Works**
>
> - You have an expensive computation (sorting, heavy math, data transforms,
>   language processing)
> - That computation runs on every render
> - But the inputs don’t change often
>
> **When useMemo Doesn’t Help**
>
> - Very cheap computations
> - Recalculating on every render doesn’t hurt performance
> - Dependencies change every render anyway

### useCallback

`useCallback` is a React Hook that lets you cache a function definition between re-renders.

```typescript
const cachedFn = useCallback(fn, dependencies);

// useCallback(fn, deps) ≈ useMemo(() => fn, deps)
```

### useContext

`useContext` is a React Hook that lets you read and subscribe to context from your component.

```typescript
const value = useContext(SomeContext)

// example
const ThemeContext = React.createContext("light");

function App() {
  return (
    <ThemeContext.Provider value="dark">
      <Toolbar />
    </ThemeContext.Provider>
  );
}

function Toolbar() {
  const theme = useContext(ThemeContext);
  return <div className={theme}>Toolbar theme is {theme}</div>;
}
```

> **Core Concept**
>
> 1. A **Provider** — where data lives
> 2. A **Consumer** — where data is read
> 3. The actual **value** being shared

### useReducer

`useReducer` is a React Hook that lets you add a reducer to your component.

> **what it does**
>
> - Keeps and manages state
> - Centralizes state update logic in one place
> - Uses a reducer function to decide how to update state based on actions
> - Returns a state value and a dispatch function to trigger updates

```typescript
const [state, dispatch] = useReducer(reducer, initialState);

// example
// reducer function
function reducer(state, action) {
  switch (action.type) {
    case "increment":
      return { count: state.count + 1 };
    case "decrement":
      return { count: state.count - 1 };
    default:
      return state;
  }
}

// in component
const [state, dispatch] = useReducer(reducer, { count: 0 });

// update state
dispatch({ type: "increment" });
```

### useActionState

`useActionState` is a **built-in React Hook** that lets you **manage component state that’s tied to the result of an Actions**, most commonly a **form action**. Instead of using separate state hooks (`useState`) and managing loading/pending state manually, this hook bundles:

- a current state value
- an action dispatcher you use to submit
- a `isPending` flag while the action is running

```typescript
const [state, formAction, isPending] = useActionState(fn, initialState, permalink?)

// fn — an action function that will be executed when the form is submitted or the dispatcher is called
// initialState — the starting state before any action runs
// permalink? (optional) — a URL used for progressive enhancement when JavaScript isn’t yet running (e.g., SSR hydration scenarios)

//example (Form Submission)

import { useActionState } from "react";

async function increment(prevCount, formData) {
  return prevCount + 1;
}

function Counter() {
  const [count, formAction, isPending] = useActionState(increment, 0);

  return (
    <form action={formAction}>
      <p>Count: {count}</p>
      <button disabled={isPending}>Increment</button>
      {isPending && "Updating..."}
    </form>
  );
}
```

### useTransition

`useTransition` is a React hook for **marking some state updates as “transitions” (urgent vs non-urgent)** so React can keep the UI responsive during slow or expensive updates.

```typescript
const [isPending, startTransition] = useTransition();

// isPending: a boolean that tells you “a low-priority update is ongoing”
// startTransition: a function you wrap around state updates you consider non-urgent

// example
const [isPending, startTransition] = useTransition();

function handleSearch(e) {
  setText(e.target.value); //urgent

  startTransition(() => {
    setList(bigArray.filter((item) => item.includes(e.target.value)));
  });
}
```

> **🧠 What startTransition Does**
>
> React will treat updates inside `startTransition` as **low-priority work**:
>
> - It may delay rendering them until after urgent updates finish
> - It keeps your app responsive during heavy rendering
> - It lets React interrupt the update if something more urgent happens

### useOptimistic

`useOptimistic` is a React Hook that lets you optimistically update the UI.

> `setOptimistic(...)` **must be called inside an Actions**

```typescript
const [optimisticState, setOptimistic] = useOptimistic(value, reducer?);

// parameters
// value: The value returned when there are no pending Actions.
// optional reducer(currentState, action): The reducer function that specifies how the optimistic state gets updated. It must be pure, should take the current state and reducer action arguments, and should return the next optimistic state.

// returns
// optimisticState: The current optimistic state. It is equal to value unless an Action is pending, in which case it is equal to the state returned by reducer (or the value passed to the set function if no reducer was provided).
// The set function that lets you update the optimistic state to a different value inside an Action.

// example
import { useOptimistic, startTransition, useState } from "react";

function LikeButton({ initialLiked }) {
  const [liked, setLiked] = useState(initialLiked);
  const [optimisticLiked, setOptimisticLiked] = useOptimistic(liked);

  async function onLike() {
    startTransition(async () => {
      setOptimisticLiked(true);          // instant UI
      const saved = await saveLike();    // your async call
      setLiked(saved);                   // real state converges
    });
  }

  return <button onClick={onLike}>{optimisticLiked ? "Liked" : "Like"}</button>;
}
```

---

## APIs

### Cache

`cache` is only use with React **Server Components**

```typescript
import { cache } from "react";
import calculateUserMetrics from "lib/user";

const getUserMetrics = cache(calculateUserMetrics);

function Profile({ user }) {
  const metrics = getUserMetrics(user);
  // ...
}

function TeamReport({ users }) {
  for (let user in users) {
    const metrics = getUserMetrics(user);
    // ...
  }
  // ...
}
```

### lazy

lazy is a built-in React function that lets you **defer loading a component’s code until it’s actually needed** (i.e., when it’s rendered for the first time). This is part of **code-splitting**, which improves performance by reducing the size of your initial JavaScript bundle.

```typescript
// Call lazy outside your components to declare a lazy-loaded React component:
import { lazy } from 'react';

const MarkdownPreview \= lazy(() \=\> import('./MarkdownPreview.js'));
```

> **When to use lazy()**
>
> - Large and not critical for initial view
> - Used only on certain routes or interactions
> - Beneficial to split into a separate chunk

### Memo

memo is a **higher-order component (HOC)** that wraps a component to make React skip re-rendering it when its props haven’t changed. It’s a **performance optimization** tool — not a change in behavior.

```typescript
import { memo } from 'react';

function UserCard({ user }) {
  return <div>{user.name}</div>;
}

const MemoUserCard = memo(UserCard);
```

### use

`use` is a React API that lets you read the value of a resource like a `Promise` or `context`.

> - Must Be Inside a Component/Hook

> - When fetching data in a **Server Component**, the docs recommend using `async/await` rather than `use()` — because `await` integrates more naturally with the rendering pipeline on the server. But `use()` remains useful in **Client Components** (e.g., resolving a server-provided Promise).

```typescript
const value = use(resource);

// example
import { use } from "react";

function MyComponent({ messagePromise }) {
  const message = use(messagePromise);
  const theme = use(ThemeContext);
}
// messagePromise could be a Promise for async data.
// ThemeContext is a React Context object.
// use() returns the resolved value of the resource.
```
