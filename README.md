# Node.js, Express and MongoDB Project Structure

This is a basic project structure to help you to start building your own RESTful web APIs (for Android, IOS, or JavaScript frameworks) using Express framework and MongoDB with a good structure practices based on clean MVC Architecture.

## Features

- Fundamental of Express: routing, middleware, sending response and more
- Fundamental of Mongoose: Data models, data validation and middleware
- RESTful API including pagination and sorting
- CRUD operations with MongoDB
- Security: encyption, sanitization and more
- Authentication with JWT : login and signup
- Authorization (User roles and permissions)
- Error handling
- Environment Varaibles
- handling error outside Express
- Catching Uncaught Exception

## Project Structure

### Controllers

The controllers directory contains all the functions that will be executed when reaching a specifing route.

- baseController: contains all the functions that can be reusable by multiple models across the API (for example CRUD).
- authController: contains all the basic logic for user implementation, login, signup, JWT, routes protection + restriction function for a certain role.
- errorController: contains custom error message.
- userController: contains all the logic for user related functions. It also uses baseController to gain time.

### Models

The models directory contains the structure of your models for collections in MongoDB.

- You can execute hooks function like pre in this file, allowing you to do some checking before saving the received data in the database. For example in userModel, pre is used for for checking the password and hash it.
- You can use validator to check fields and return error message if the data is not accepted.

### Routes

The routes directory contains all the routes for the Front-End app to go get, post, put, patch the data.

- You just have to define if the type of route you want (post, get). The first argument is the path of your route, the second argument is the function that will be called.

~~~~javascript
// first argument is '/login'
// second argument is authController.login
router.post('/login', authController.login);
~~~~

- You can also define a route that can executes multiples functions depending on the type of request you are doing

~~~~javascript
// We are defining a route that take an ID (represented by the :id placeholder)
// Then we define what this route will be doing if it's a get, a path or a delete request
router
    .route('/:id')
    .get(userController.getUser)
    .patch(userController.updateUser)
    .delete(userController.deleteUser);
~~~~

### app.js

This file defines all the middleware that the API will use when launching, go see the file itself for more informations about the middlewares. In the Routes section of the file, you'll need to import all your routes files and follow this schema:

~~~~javascript
// First argument is the access route
// Second argument is your route file
app.use('/api/v1/users', userRoutes);
~~~~

### config.env

This file is for your environment variables, don't add it to git as it needs to be secret. For example, your secret for generating JSON Web Token will be there, as the url of your database. (pour l'exemple, il sera laissé dans le git).
  