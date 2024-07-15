# Selector specificity

For every CSS rule, the user agent evaluates the specificity to determine which declarations should apply to an element.

Specificity is expressed in three parts:

- An ID selector adds 1,0,0
- A class selector adds 0,1,0
- A type selector adds 0,0,1

| ID  | Class | Type |
| --- | ----- | ---- |
| 1   | 0     | 0    |
| 0   | 1     | 0    |
| 0   | 0     | 1    |

Order of priority goes left to right, so one ID selector has a higher specificity than 10 class selectors.

Where there are multiple selectors with an equal specificity, the cascade order means that the final selector to be evaluated will win.

## Examples

These examples are from _CSS: The Definitive Guide, Fifth edition_.

```css
h1 {
  color: red;
} /* 0,0,1 */

body h1 {
  color: green;
} /* 0,0,2 (winner)*/
```

```css
h2.grape {
  color: purple;
} /* 0,1,1 (winner) */

h2 {
  color: silver;
} /* 0,0,1 */
```

```css
html > body table tr[id="totals"] td ul > li {
  color: maroon;
} /* 0,1,7 */

li#answer {
  color: navy;
} /* 1,0,1 (winner) */
```

## Calculating specificity

This [specificty calculator](https://specificity.keegan.st) lets you enter multiple selectors and then sort by specificity.

## References

- [Specificity - CSS: Cascading Style Sheets | MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/Specificity)
