UseMemo and UseCallback are those Hhooks which are used for optimization purpose
useMemo: Invokes the provided function & caches the result
useMemo():takes 1st parameter function whose return value  needs to be cached and takes 2nd parameter as dependency.
useCallback Hook returns a memoized callback function.
 useMemo Hook returns a memoized value.


import React, { useState, useCallback } from 'react';
// A simple child component
const Child = React.memo(({ onClick }) => {
  console.log('Child rendered');
  return <button onClick={onClick}>Click Me</button>;
});
function Parent() {
  const [count, setCount] = useState(0);
  // Memoizing the increment function
  const increment = useCallback(() => {
    setCount(count + 1);
  }, [count]); // This function will only change when `count` changes
  return (
    <div>
      <h1>Count: {count}</h1>
      <Child onClick={increment} />
    </div>
  );
}
export default Parent;












useCallback and useMemo are two React hooks that help optimize performance by memoizing values or functions.

1. useCallback:

Memoizes a function to prevent it from being recreated on every render unless its dependencies change.

This is useful when passing callbacks to child components that depend on specific props or state values.


Example:

import React, { useState, useCallback } from 'react';

const Button = React.memo(({ handleClick }) => {
  console.log('Button rendered');
  return <button onClick={handleClick}>Click me</button>;
});

function App() {
  const [count, setCount] = useState(0);

  const increment = useCallback(() => {
    setCount((prevCount) => prevCount + 1);
  }, []); // The function will only be recreated if its dependencies change (none here)

  return (
    <div>
      <h1>Count: {count}</h1>
      <Button handleClick={increment} />
    </div>
  );
}

export default App;

Without useCallback: The increment function would be recreated every time the App component re-renders, causing the Button component to also re-render unnecessarily.

With useCallback: The increment function is only recreated if its dependencies change, preventing the Button from re-rendering unless necessary.



2. useMemo:

Memoizes the result of a computation to avoid re-calculating it on every render unless its dependencies change.

Use this when an expensive calculation depends on some props or state values.


Example:

import React, { useState, useMemo } from 'react';

function App() {
  const [count, setCount] = useState(0);
  const [items, setItems] = useState([1, 2, 3, 4]);

  // Use useMemo to only recalculate the sum when `items` changes
  const total = useMemo(() => {
    console.log('Calculating total');
    return items.reduce((a, b) => a + b, 0);
  }, [items]); // Recalculate only when `items` changes

  return (
    <div>
      <h1>Count: {count}</h1>
      <h2>Total: {total}</h2>
      <button onClick={() => setCount(count + 1)}>Increment Count</button>
      <button onClick={() => setItems([...items, items.length + 1])}>Add Item</button>
    </div>
  );
}

export default App;

Without useMemo: The total would be recalculated on every render, even if items haven’t changed.

With useMemo: The total is only recalculated when the items array changes.




In summary:

useCallback: Memoizes a function.

useMemo: Memoizes a value (result of a function).


