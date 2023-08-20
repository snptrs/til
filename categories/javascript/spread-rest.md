# Spread and rest

## Spread
When `...` is used on the RHS of an assignment, it's called the spread operator. Use it to expand an iterable (e.g. an array, string or object) into a list of elements.

```javascript
const first = ["heads", "shoulders"];
const second = ["knees", "and"];
const complete = [...first, ...second, "toes"];
complete; // => ["heads", "shoulders", "knees", "and", "toes"]

let person = {
  firstName: "Bart",
  lastName: "Simpson"
};
person = {...person, city: "Springfield"};
// => { firstName: 'Bart', lastName: 'Simpson', city: 'Springfield' }
```

## Rest
When `...` is used on the LHS of an assignment, it's called the rest operator. Coupled with a variable name, it's known as a rest element.  It takes zero or more elements and stores them in an array.

```javascript
const [first, second, ...others] = ["tea", "coffee", "hot chocolate", "beer"];
others; // => ["hot chocolate", "beer"]
```

We can also use it in function definitions to allow an unkown number of arguments to be passed in as an array.

```javascript
const phrase = (...words) => {
  return words.join(', ');
};

phrase("rock", "paper", "scissors");
// => 'rock, paper, scissors'
```

## References
- [Rest parameters - JavaScript | MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/rest_parameters)
- [Spread syntax (...) - JavaScript | MDN](https://developer.mozilla.org/en-US-/docs/Web/JavaScript/Reference/Operators/Spread_syntax)