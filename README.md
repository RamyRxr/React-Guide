# React Complete Developer Handbook

## Table of Contents
1. Introduction to React
2. JSX and Virtual DOM
3. Components
4. Props and State
5. Rendering and Lifecycle
6. Hooks in Depth
7. Context API
8. State Management with Redux
9. Axios - HTTP Client
10. React Router
11. Advanced Topics and Best Practices
12. Visual Diagrams and Flowcharts

---

## 1. Introduction to React

React is a **JavaScript library** for building user interfaces. It allows you to create **reusable components** and efficiently update the UI when data changes.

### Core Concepts:
- **Declarative:** Describe what the UI should look like.
- **Component-Based:** Build encapsulated pieces of UI.
- **Virtual DOM:** Efficiently updates only what changes.

**Example:**
```jsx
function Welcome() {
  return <h1>Hello, World!</h1>;
}
export default Welcome;
```

---

## 2. JSX and Virtual DOM

JSX stands for **JavaScript XML**. It lets you write HTML in React.

**Example:**
```jsx
const element = <h1>Hello, {user.name}</h1>;
```

### Virtual DOM Diagram:
```
[Component Tree] → [Virtual DOM Diffing] → [Real DOM Updates]
```

---

## 3. Components

React components can be **Functional** or **Class-Based**.

### Functional Component:
```jsx
function Button({ label }) {
  return <button>{label}</button>;
}
```

### Class Component:
```jsx
class Button extends React.Component {
  render() {
    return <button>{this.props.label}</button>;
  }
}
```

---

## 4. Props and State

### Props
- Passed from parent to child.
- Read-only.

**Example:**
```jsx
function Welcome({ name }) {
  return <h1>Hello, {name}</h1>;
}
```

### State
- Managed inside a component.
- Mutable via `useState`.

**Example:**
```jsx
function Counter() {
  const [count, setCount] = useState(0);
  return (
    <div>
      <p>{count}</p>
      <button onClick={() => setCount(count + 1)}>+</button>
    </div>
  );
}
```

---

## 5. Rendering and Lifecycle

React updates the UI whenever state or props change.

### Lifecycle Diagram:
```
Mount → Update → Unmount
```

### Lifecycle Methods (Class Components)
- `componentDidMount()`
- `componentDidUpdate()`
- `componentWillUnmount()`

---

## 6. Hooks in Depth

Hooks let you use state and lifecycle in functional components.

### Common Hooks

#### `useState`
Manages local state.
```jsx
const [value, setValue] = useState('Hello');
```

#### `useEffect`
Performs side effects (API calls, timers).
```jsx
useEffect(() => {
  console.log("Mounted");
  return () => console.log("Unmounted");
}, []);
```

#### `useContext`
Access global context.
```jsx
const value = useContext(MyContext);
```

#### `useRef`
Access DOM elements or store mutable values.
```jsx
const inputRef = useRef(null);
<input ref={inputRef} />;
```

#### `useMemo` and `useCallback`
Optimize performance by memoizing values or functions.

#### `useReducer`
Alternative to useState for complex logic.
```jsx
function reducer(state, action) {
  switch (action.type) {
    case 'increment':
      return { count: state.count + 1 };
  }
}
const [state, dispatch] = useReducer(reducer, { count: 0 });
```

#### `useLayoutEffect`
Runs synchronously after all DOM mutations.

#### `useImperativeHandle`
Customizes the instance value exposed by `ref`.

#### `useId`
Generate unique IDs for accessibility or keys.

#### `useTransition` and `useDeferredValue`
Handle concurrent rendering and slow updates smoothly.

---

## 7. Context API

Used for global state sharing.

**Example:**
```jsx
const ThemeContext = createContext();

function App() {
  return (
    <ThemeContext.Provider value="dark">
      <Toolbar />
    </ThemeContext.Provider>
  );
}
function Toolbar() {
  const theme = useContext(ThemeContext);
  return <div>Theme: {theme}</div>;
}
```

**Diagram:**
```
[Provider] → [Context] → [Consumers]
```

---

## 8. State Management with Redux

Redux provides a **centralized store** for your app state.

### Core Principles
1. Single source of truth.
2. State is read-only.
3. Changes via pure functions (reducers).

**Example (Redux Toolkit):**
```js
import { configureStore, createSlice } from '@reduxjs/toolkit';

const counterSlice = createSlice({
  name: 'counter',
  initialState: { value: 0 },
  reducers: {
    increment: (state) => { state.value += 1; }
  }
});

export const { increment } = counterSlice.actions;
export const store = configureStore({ reducer: { counter: counterSlice.reducer } });
```

**Flow Diagram:**
```
UI → Dispatch(Action) → Reducer → Store → UI Update
```

---

## 9. Axios - Promise-Based HTTP Client

Axios is used to perform HTTP requests.

### Installation
```bash
npm install axios
```

### Basic Usage
```js
axios.get('/api/users').then(res => console.log(res.data));
```

### POST Request
```js
axios.post('/api/add', { name: 'Ramy' });
```

### Async/Await
```js
const fetchData = async () => {
  try {
    const res = await axios.get('/api/data');
    console.log(res.data);
  } catch (err) {
    console.error(err);
  }
};
```

### Interceptors
```js
axios.interceptors.request.use(config => {
  config.headers.Authorization = 'Bearer TOKEN';
  return config;
});
```

### Cancel Tokens
```js
const source = axios.CancelToken.source();
axios.get('/api/data', { cancelToken: source.token });
source.cancel('Request canceled');
```

### Multiple Requests
```js
axios.all([axios.get('/users'), axios.get('/posts')])
  .then(axios.spread((users, posts) => {
    console.log(users.data, posts.data);
  }));
```

---

## 10. React Router

Used for **client-side navigation**.

**Installation:**
```bash
npm install react-router-dom
```

**Example:**
```jsx
import { BrowserRouter, Routes, Route, Link } from 'react-router-dom';

function App() {
  return (
    <BrowserRouter>
      <Link to="/about">About</Link>
      <Routes>
        <Route path="/" element={<Home />} />
        <Route path="/about" element={<About />} />
      </Routes>
    </BrowserRouter>
  );
}
```

---

## 11. Advanced Topics and Best Practices

- **Memoization:** Use `React.memo`, `useMemo`, `useCallback`
- **Error Boundaries**
- **Code Splitting** with `React.lazy` and `Suspense`
- **Portal Rendering**
- **Performance Optimization**
- **Folder Structure:**
```
src/
 ├── components/
 ├── hooks/
 ├── context/
 ├── redux/
 └── utils/
```

---

## 12. Visual Diagrams (Text-based)

### React Data Flow
```
Parent → Props → Child
Child → Event → Parent (State Update)
```

### Redux Data Flow
```
Component → Dispatch(Action) → Reducer → Store → Rerender
```

---

# Summary

This guide covers:
- React core concepts and lifecycle
- Every hook and their use
- State management with Context and Redux
- HTTP calls with Axios
- Routing with React Router
- Optimization and best practices

Now you can use this as your all-in-one **React reference handbook**.
