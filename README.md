# Mongo1.0

Topics:

- Databases
- MongoDB
- `mongod` and `mongosh`
- [SQL vs NoSQL Databases](https://www.geeksforgeeks.org/difference-between-sql-and-nosql/)
- [Mongoose](https://mongoosejs.com/docs/)
- Creating documents.
- Performing basic queries in [Mongo Shell](https://www.mongodb.com/docs/mongodb-shell/run-commands/)
- Understanding [module exports](https://www.freecodecamp.org/news/module-expoarts-how-to-export-in-node-js-and-javascript/)
- Controller, Models, Routes Structure

## Description

Use Node.js and Express to write an API that can create and read Bears stored in a MongoDB Database.

## Instructions

### Start MongoDB

For this project you need to have _MongoDB Community Edition_ installed and running locally or an account with a _Database As A Service_ provider like [Mongo Atlas](https://www.mongodb.com/cloud/atlas). This DBAAS providers offer a free tier with 500MB size limit that can be used for development and testing.

#### Using a Local Mongo Server

If you don't have MongoDB installed, please click on [this link](https://docs.mongodb.com/manual/administration/install-community/) for instructions on how to **install** and **run** the server and the _mongo shell_. Follow the instructions for your _Operating System_.

After MongoDB is installed, follow the instructions on the documentation to start the server. Then run the _mongo shell_ from a separate terminal and execute the `show dbs` command. If all goes well you should see a list of available databases, similar to the sample below.

```
 > show dbs
 admin  0.000GB
 local  0.000GB
```

### Create API Server

Create an _Express_ application and add a route for `/` that returns HTTP status code `200` and the following JSON object:

```json
{
  "message": "API running"
}
```

**Use _Postman_ to test your API.**

### Connect API Server to MongoDB

Add _mongoose_ to the project and use it to connect your API to the `bears` database in MongoDB. The `bears` database will be created automatically by MongoDB if it doesn't exist. If there is an error connecting to the database, do **NOT** start the API and display the following message to the console: _"Database connection failed"_.

If the connection to MongoDB succeeds, start the API and show the following message to the console: _"All your databases are belong to us!"_.

### Create Bear Schema and Model

Create a _Schema_ and a _Model_ for the _Bears_ collection. Each _Bear_ Model should conform to the following schema:

```js
{
  species: "Indian Black Bear", // required string
  latinName: "Ursus Indiano", // required string
  createdOn: Mon Aug 14 2017 12:50:16 GMT-0700 (PDT) // required Date, should default to current date and time
}
```

### Create API Endpoints

Configure the API to respond to the following routes:

| Method | Endpoint      | Description                                                          |
| ------ | ------------- | -------------------------------------------------------------------- |
| POST   | /api/bear     | Creates a bear using the information sent inside the `request body`. |
| GET    | /api/bear     | Returns an array of all the bear objects contained in the database.  |
| GET    | /api/bear/:id | Returns the bear object with the specified id.                       |
| PUT    | /api/bear/:id | Updates a given id bear. Returns Updated Bear                        |
| Delete | /api/bear/:id | Deletes a given id bear. Returns {success: true}                     |

#### Endpoint Specifications

When the client makes a `POST` request to `/api/bear`:

- If the request body is missing the `species` or `latinName` property, cancel the request, respond with HTTP status code `400`, and return the following JSON response: `{ errorMessage: "Please provide both species and latinName for the Bear." }`.

- If the information about the _Bear_ is valid, save the new _Bear_ the the database, return HTTP status code `201` and return the newly created _Bear Document_. Check the added bear in mongo shell.

- If there's an error while saving the _Bear_, cancel the request, respond with HTTP status code `500` and return the following JSON object: `{ error: "There was an error while saving the Bear to the Database" }`.

When the client makes a `GET` request to `/api/bear`:

- If there's an error in retrieving the _Bears_ from the database, cancel the request, respond with HTTP status code `500` and return the following JSON object: `{ error: "The information could not be retrieved." }`.

When the client makes a `GET` request to `/api/bear/:id` (remember, `:id` is a
parameter embedded in the URL, not in the query-string):

- If the _Bear_ with the specified `id` is not found, return HTTP status code `404` and the following JSON object: { message: "The Bear with the specified ID does not exist." }.

- If there's an error in retrieving the _Bear_ from the database, cancel the request, respond with HTTP status code `500` and return the following JSON object: `{ error: "The information could not be retrieved." }`.

When the client makes a `PUT` request to `/api/bear/:id`:

- If the _Bear_ with the specified `id` is not found, return HTTP status code `404` and the following JSON object: { message: "The Bear with the specified ID does not exist." }.

- If the information about the _Bear_ is valid, save the updated _Bear_ the the database, return HTTP status code `204` and return the updated _Bear Document_. Check the updated bear in mongo shell.

- Update a _Bear_ using mongo shell

When the client makes a `DELETE` request to `/api/bear/:id`:

- If the _Bear_ with the specified `id` is not found, return HTTP status code `404` and the following JSON object: { message: "The Bear with the specified ID does not exist." }.

- If the information about the _Bear_ is valid, delete the _Bear_

- Delete a _Bear_ using mongo shell

### Additional Notes

Remember to use `body-parser` to read information from the request body.

Delete the database after the project is complete

```
> use bears;
> db.dropDatabase();

```

**Stop the MongoDB database server when not in use to save computer resources**.
