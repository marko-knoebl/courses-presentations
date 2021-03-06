# The effect hook and outdated state

## The effect hook and outdated state

As we've seen before, asynchronous functions may reference outdated state / data

## The effect hook and outdated state

example: buggy code that will keep referencing obsolete state in a closure

```js
function CounterWithLogging() {
  const [count, setCount] = useState(0);

  useEffect(() => {
    setInterval(() => {
      // the variable "count" will always refer to the
      // value from the initial rendering (0)
      console.log(count);
    }, 1000);
  }, []);

  return (
    <button onClick={() => setCount(count + 1)}>
      {count}
    </button>
  );
}
```

## Identifying potentially obsolete data in an effect hook

Linter rule that can help identifying obsolete data:

_react-hooks/exhaustive-deps_

## Fixing the problem of obsolete data

varying solutions depending on the scenario:

- move code inside the definition of an effect
- re-run an effect when any dependency changes (see hints in linter rules)
  - list additional dependencies
  - `useCallback`
- pass a "transformer" function to a state setter (which can always access the most recent state)
- store the most recent version of a state entry in a ref as well (this will also be available in older closures)

## Fixing the problem of obsolete data

example solution to the closure problem with _setInterval_: use the _ref_ hook and potentially a custom hook

see:

- [Dan Abramov: Making setInterval Declarative with React Hooks](https://overreacted.io/making-setinterval-declarative-with-react-hooks/)
- [use-interval on GitHub](https://github.com/donavon/use-interval)

## The effect hook and obsolete data

explanation: difference between state / props in function components and class components:

when props / state change:

- in class components, `this.props` and `this.state` will be replaced with new objects
- in function components, the component function is called again, and a new _closure_ is created that contains the new props / state values

note: in function components, old / obsolete data may still live on inside older closures
