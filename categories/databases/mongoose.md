# Mongoose

- [Mongoose](https://mongoosejs.com/) is a wrapper around [MongoDB](./mongodb.md).
- Add Mongoose to a project with `npm install mongoose`.

## Basics

### Require Mongoose and connect to a DB

```javascript
// script.js
const mongoose = require("mongoose");

mongoose.connect("mongodb://localhost/dbName", () => {
  // Can pass two optional arguments
  // The first function you pass to Mongoose will run every time it connects to the DB
  console.log("Connected!");
  // The second is an error handler
}, e => console.error(e));
```

Mongoose will queue queries and execute them once it connects to the DB, so you don't have to wait for the connection.

### Create a model

```javascript
// User.js
const mongoose = require("mongoose");

const userSchema = new mongoose.Schema({
  name: String,
  city: String
});

module.exports = mongoose.model("User", userSchema);
```

### Using the model

```javascript
// script.js
const mongoose = require("mongoose");
const User = require("./User");

mongoose.connect("mongodb://localhost/userDB");

async function doStuff() {
  // This will create a new User and add it to the DB
  const user = await User.create({ name: "Sean", city: "Brighton" });
  
  // To update fields after creation, update the object's properties,
  // then save it to the DB again
  user.city = "Paris";
  await user.save();
  
  // An alternative to .create is using new User(), then saving manually to the DB:
  // const user = new User({ name: "Sean", city: "Brighton" });
  // user.save();
}
```

## Schema data types
- Basic types
  - `String`
  - `Number`
  - `Date`

- Document IDs
  - To reference the ObjectID of another document: `mongoose.SchemaTypes.ObjectID`

- Arrays
  - We can either just declare a blank array: `ingredients: []`
  - or specify the type of data within the array: `ingredients: [String]`
  
- Nesting values
  - This is similar to creating a JS object:
  ```javascript
  address: {
    street: String,
    city: String
  }
  ```
  
