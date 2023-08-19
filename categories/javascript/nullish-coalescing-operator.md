# Nullish coalescing operator (??)

Returns the right-hand value when the left-hand value is `null` or `undefined`. Otherwise, returns the left-hand value.

```javascript
const hey = null;
console.log(hey ?? "Hello!");
// Outputs "Hello!"
```

## Logical OR `||` operator

The nullish coalescing operator is subtly different from the `||` operator. `||` will return the right-hand value if the left-hand one is falsy, not just if it's `null` or `undefined`.

```javascript
const hey = "";
console.log(hey ?? "Hello!");
// Outputs "" because an empty string is not null or undefined

const hey = "";
console.log(hey || "Hello!");
// Outputs "Hello!" because an empty string is falsy
```

## References
- [Nullish coalescing operator (??) - JavaScript | MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Nullish_coalescing)