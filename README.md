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
