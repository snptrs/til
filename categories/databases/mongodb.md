# MongoDB

mongosh is an interactive MongoDB shell.

Install it with Homebrew: `brew install mongosh`

## Basic commands
- View databases: `show dbs`
- Switch databases: `use <db name>`
- View collections: `show collections`
- Delete a collection: `db.dropDatabase()`
- Clear screen: `cls`

## Inserting data
- `db.collectionName.insertOne({ name: "Sean" })`
- Not all documents in a collection need to share the same fields.
- `db.collectionName.insertMany([{ name: "Sean" }, { name: "Pete" }])`

## Retrieving data
- `db.collectionName.find()`
- Just get the first result: `db.collectionName.findOne()`
- `db.collectionName.find().limit(2)`
- `db.collectionName.find().sort({ name: 1, city: -1 }).limit(2)`
    - 1 sorts ascending, -1 sorts descending
- `db.collectionName.find().skip(1).limit(2)`
    - Skips the first n records
- Equivalent of a WHERE clause:
    - `db.collectionName.find({ name: "Sean" })`
    - `db.collectionName.find({ city: "Brighton", age: 30 })`
- Choose which fields to return:
    - `db.collectionName.find({ name: "Sean" }, { age: 1, city: 1 })`
        - 1 to return to field, 0 to not return it (e.g. you could do `_id: 0` to not automatically return the ID.
        - Or, just do 0 on certain fields to not return them but return everything else

### Retrieving data with complex queries
- `db.collectionName.find({ name: { $eq: "Sean" }})`
- Not equal to: `db.collectionName.find({ name: { $ne: "Sean" }})`
- Other complex query operators:
    - Greater than: `$gt`
    - Greater than or equal to: `$gte`
    - Less than: `$lt`
    - less than or equal to: `$lte`
- Value is in a list of values: `db.collectionName.find({ name: { $in: ["Sean", "Pete"] }})`
- Or, not in the list: `db.collectionName.find({ name: { $nin: ["Sean", "Pete"] }})`
- Return documents that have a particular field on them:  `db.collectionName.find({ name: { $exists: true }})`
- Multiple criteria are treated as AND by default: `db.collectionName.find({ distance: { $gte: 2, $lte: 20 }, city: "Brighton" })`
- To treat them as OR: `db.collectionName.find({ $or: [{ distance: { $lte: 20 }}, { city: "Brighton" }] })`
- Using $not to return results that don't match a query: `db.collectionName.find({ age: { $not: { $lte: 30 } }})`
- Comparing two values - this will return all documents where col1 value is greater than col2 value: `db.collectionName.find({$expr: { $gt: ["$col1", "$col2"] }})`
- Selecting based on a nested value: `db.collectionName.find({ "address.city": "Brighton" })`

## Updating data

### Updating single documents
- `db.collectionName.update({ name: "Sean" }, { $set: { city: "Brighton" } })`
- Increment an existing value: `db.collectionName.update({ name: "Sean" }, { $inc: { age: 1 } })`
- Rename a column: `db.collectionName.update({ name: "Sean" }, { $rename: { city: "town" } })`
- Remove a column from a document: `db.collectionName.update({ name: "Sean" }, { $unset: { city: "" } })`
- Push a value to an array: `db.collectionName.update({ name: "Sean" }, { $push: { skills: "Coding" } })`
- Remove a value from an array: `db.collectionName.update({ name: "Sean" }, { $pull: { skills: "Coding" } })`
- Replace an entire document with new values: `db.collectionName.replaceOne({city: "Brighton"}, { name: "Shannon" })`

### Updating multiple documents
- Remove the city field from all documents containing a city: `db.collectionName.updateMany({ city: { $exists: true }}, {$unset: { city: "" }})`

## Deleting data
- `db.collectionName.deleteOne({name: "Sean"})`
- Delete all records that don't have a city: `db.collectionName.deleteMany({ city: { $exists: false }})`

## References
- [MongoDB Crash Course](https://www.youtube.com/watch?v=ofme2o29ngU): Really good tutorial.
- [Getting Started — MongoDB Manual](https://www.mongodb.com/docs/manual/tutorial/getting-started/)
