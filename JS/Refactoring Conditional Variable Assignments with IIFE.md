When determining the value of a variable based on certain conditions, it's common to initialize the variable with a mutable `let` binding and then assign it a value within an `if-else` structure. However, an alternative and often cleaner approach is to use an immediately invoked function expression (IIFE) to encapsulate the logic and directly assign the result to an immutable `const` variable.

Consider the traditional approach:

```javascript
const onClick = () => {
  let updatedArray;
  if (condition) {
    updatedFilters = valueA;
  } else {
    updatedFilters = valueB;
  }
  // Use updatedFilters
};
```

This can be simplified and made more declarative by using an IIFE:

```javascript
const onClick = () => {
  const updatedArray = (() => {
    if (condition) {
      return valueA;
    }
    return valueB;
  })();
  // Use updatedFilters
};
```

The second approach has several benefits over the first. Firstly, it promotes the use of immutable variables, which can help prevent bugs related to unintended reassignments. Secondly, it encapsulates the logic for determining the value of `updatedFilters` within a single, concise expression, making the code more readable and maintainable. Lastly, this pattern makes it clearer that `updatedFilters` is meant to be a constant value determined by a specific piece of logic, emphasizing the declarative nature of the code.