# Thoughts

## Background

### UseEffect && Dependencies

```js
useEffect(() => {
  window.localStorage.setItem("itm", itm);
}, [itm]);
```

- **The Array dependency list** describes 'when' the side-effect will run: when the value of itm changes, here

### A Dependency Problem

```js
//via prop
function somePropPassedFunction(i) {
  window.localStorage.setItem("itm", i);
}

useEffect(() => {
  somePropPassedFunction(itm);
}, []); //call some fn passed as a prop
```

... what should go in the dependency list?

- somePropPassedFunction()
- itm

Here, though, when the function 'changes' due to component re-rendering, the effect will run again... NOT the goal

### A Solution, useCallback

```js
const updateLS = useCallback(() => window.localStorage.setItem("itm", itm), [
  itm,
]);
useEffect(() => {
  updateLS();
}, [updateLS]);
```

- on re-renders the fn doesn't re-build
