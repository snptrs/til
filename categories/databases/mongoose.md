# Mongoose

- [Mongoose](https://mongoosejs.com/) is a wrapper around [MongoDB](./mongodb.md).
- Add Mongoose to a project with `npm install mongoose`.

## Basics

### Require Mongoose and connect to a DB

```javascript
const mongoose = require("mongoose");

mongoose.connect("mongodb://localhost/dbName", () => {
  // Can pass two optional arguments
  // The first function you pass to Mongoose will run every time it connects to the DB
  console.log("Connected!");
  // The second is an error handler
}, e => console.error(e));
```

Mongoose will queue queries and execute them once it connects to the DB, so you don't have to wait for the connection.

### Creat a model

