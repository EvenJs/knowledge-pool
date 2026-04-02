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
