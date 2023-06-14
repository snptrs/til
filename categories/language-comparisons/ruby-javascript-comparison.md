# Ruby and JavaScript comparison

This is a comparison of various common methods and bits of syntax in Ruby and JavaScript to remind me how to do things in both languages.

## Basics

### Comments

| Ruby                                                          | JavaScript                                                 |
| ------------------------------------------------------------- | ---------------------------------------------------------- |
| # Use line comments for<br /># single and multi-line comments | // Line comments<br /><br />/* Multi-line<br />comments */ |

### Variables

| Ruby                  | JavaScript                                                                                                                            |
| --------------------- | ------------------------------------------------------------------------------------------------------------------------------------- |
| `first_name = 'Sean'` | `let firstName;` // Can declare without initialising<br />`let firstName = "Sean";`<br /><br />- Variables can only be declared once. |

- Reserved keywords can't be used as variable names: [JavaScript](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Lexical_grammar#reserved_words), [Ruby](https://ruby-doc.org/3.2.2/keywords_rdoc.html).

### Constants

| Ruby                  | JavaScript                                                    |
| --------------------- | ------------------------------------------------------------- |
| `FIRST_NAME = "Sean"` | `const firstName = "Sean";` // Must initialise when declaring |

- This is a helpful line from the JS docs about when to use `let` or `const`: ‘Use `const` when you can, and use `let` when you have to.’

### Data types and coercion

Ruby and JS are both [weakly typed](https://en.wikipedia.org/wiki/Strong_and_weak_typing). They'll try to convert values to the right type when used.

- [JavaScript data types and data structures](http://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures)

<!-- # TODO -->

## Strings

### Concatenating strings

| Ruby                                              | JavaScript                                                         |
| ------------------------------------------------- | ------------------------------------------------------------------ |
| `city = "London"`<br />`puts "I live in #{city}"` | `let city = "London";`<br />`` `I live in ${city}` // Backticks `` |

- Referred to as 'template literals' in JS and 'string interpolation' in Ruby.

Can also concatenate using `+`:

| Ruby                   | JavaScript                      |
| ---------------------- | ------------------------------- |
| `puts "Hello " + name` | `console.log("Hello " + name);` |


