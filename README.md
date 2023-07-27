## DAY013: USER AUTH SYSTEM WITH JWT & MONGODB

### Step 1: Project Setup

1. Create a new directory for your project and navigate into it.

2. Initialize a new Node.js project by running the following command:

```bash
npm init
```

3. Install required dependencies: Express, Mongoose, Cors, bcryptjs, and jsonwebtoken.

```bash
npm install express mongoose cors bcryptjs jsonwebtoken
```

### Step 2: Create MongoDB Database and Collection

Using the MongoDB shell, create a collection called "foods".

```javascript
// Using the MongoDB shell, create a collection called "foods"
db.createCollection('foods');

// Insert sample food items into the "foods" collection
db.foods.insertMany([
  { 'food': 'Chicken Biriyani', 'price': 200 },
  { 'food': 'Mutton Biriyani', 'price': 350 },
  { 'food': 'Egg Roll', 'price': 80 }
]);
```

### Step 3: Create User Model - `user.model.js`

Create a file named `user.model.js` inside the `models` directory.

```javascript
// Import the 'mongoose' library, which is a popular Node.js library used to interact with MongoDB, a NoSQL database.
const mongoose = require('mongoose');

// Define a 'userSchema' object using the 'mongoose.Schema' constructor to create a new Mongoose schema.
const userSchema = mongoose.Schema({
    // Define the 'name' field in the schema. It is of type 'String' and is required, meaning it must be provided when creating a new user document.
    'name': { type: String, require: true },

    // Define the 'email' field in the schema. It is of type 'String', required, and has the 'unique' constraint, meaning each email must be unique in the 'users' collection.
    'email': { type: String, require: true, unique: true },

    // Define the 'pass1' field in the schema. It is of type 'String' and required, meaning it must be provided when creating a new user document.
    'pass1': { type: String, require: true }
}, { versionKey: false }); // The second argument is an optional configuration object. Setting 'versionKey' to false means Mongoose won't create a '__v' field to track document versions.

// Export the Mongoose model created with the given schema.
// The model is named 'usermodel', and it will be used to interact with the 'users' collection in MongoDB.
module.exports = mongoose.model('usermodel', userSchema, 'users');

// A log message to indicate that the 'usermodel' is ready for use.
console.log('user model is ready for use');
```

### Step 4: Create User Routes - `user.routes.js`

Create a file named `user.routes.js` inside the `routes` directory.

```javascript
// Importing the Express library and creating a new router instance
const express = require('express');
const userRouter = express.Router();

// consuming the user model
// Importing the user model from the user.model.js file
const userModel = require('../model/user.model');

// Importing the bcryptjs and jsonwebtoken libraries
const bcrypt = require("bcryptjs");
const jwt = require("jsonwebtoken");

// Defining a POST route for user signup
userRouter.post('/signup', (req, res) => {
    // Hashing the user's password using bcrypt
    var salt = bcrypt.genSaltSync(10);
    var hash = bcrypt.hashSync(req.body.pass1, salt);

    // Creating a new user instance with the hashed password
    let newUser = new userModel({
        'name': req.body.name,
        'email': req.body.email,
        'pass1': hash
    });

    // Saving the new user to the database
    newUser.save()
        .then((userInfo) => {
            // Responding with success or error messages based on the result of the save operation
            if (!userInfo)
                res.status(200).json({ 'message': 'error while signup' })
            else
                res.status(200).json({ 'message': 'signup successfully completed' })
        })
        .catch((error) => {
            // res.status(200).json({'message': error});
            // Handling errors, including checking for duplicate email entries
            if (error.keyPattern.email)
                res.status(200).json({ 'message': 'email already registered with us !!' });
            else
                res.status(200).json({ 'message': error });
        });
});

// Defining a POST route for user signin
userRouter.post('/signin', (req, res) => {
    // Finding the user with the provided email in the database
    userModel.findOne({ 'email': req.body.email })
        .exec()
        .then((userInfo) => {
            // Handling cases where the user does not exist in the database
            if (!userInfo)
                res.status(200).json({ 'message': 'user does not exist !' });
            else {
                //res.status(200).json(userInfo);
                // Checking if the provided password matches the hashed password in the database
                let db_hash_pass = userInfo.pass1;
                let isValid = bcrypt.compareSync(req.body.pass1, db_hash_pass);
                if (isValid) {
                    // Creating a JSON Web Token (JWT) if the password is valid
                    let token = jwt.sign({ 'userActive': userInfo.name }, 'myPrivateKey', { expiresIn: '1h' });

                    //we will fetch some userinformation 
                    // Sending success response with user information and the JWT token
                    res.status(200).json({
                        'message': 'success',
                        'userActive': userInfo.name,
                        'token': token
                    });
                }
                // res.status(200).json({'message':'success'});
                else {
                    // Responding with an error message for invalid credentials
                    res.status(200).json({ 'message': 'Wrong Credentials !' });
                }
            }
        })
        .catch((error) => {
            // Handling errors
            res.status(200).json({ 'message': error });
        });
});

// Exporting the userRouter for use in other parts of the application
module.exports = userRouter;

// A log message indicating that the user router is ready to use
console.log('user router is ready to use');
```

### Step 5: Update the Main Server File - `main.js`

In your `main.js` file, update the server setup to include the user routes and the JWT authentication middleware.

```javascript
// Importing the Express library and assigning it to the variable 'express'.
const express = require('express');

// Importing the 'cors' middleware for enabling Cross-Origin Resource Sharing (CORS).
const cors = require('cors');

// Setting the port number to 3000.
const port = 3000;

// Importing the 'mongoose' library for MongoDB interaction.
const mongoose = require('mongoose');
// Importing the 'foodRouter' from the './routes/food.routes' file.
const foodRouter = require('./routes/food.routes')

// + Importing the 'userRoute' from the './routes/user.route' file.
const userRoute = require('./routes/user.route');

// Setting the MongoDB connection string.
const db = 'mongodb://127.0.0.1:27017/foodDB';
// Connecting to MongoDB using Mongoose.
mongoose.connect(db)
    .then(() => {
        console.log('connencted to mongodb');
    })
    .catch((error) => {
        console.log('error connecting ' + error);
    })
    .finally(() => {
        console.log('node with mongo');
    });

// Creating an instance of Express.
const app = express();
// Enabling Cross-Origin Resource Sharing (CORS) for all routes.
app.use(cors());

// Parsing incoming request bodies in JSON format.
app.use(express.urlencoded({ extended: true }));
app.use(express.json());

// Attaching the 'foodRouter' to the '/api' route.
app.use('/api', foodRouter);

// + Attaching the 'userRoute' to the '/users' route.
app.use('/users', userRoute);

// Handling a GET request on the root path '/'.
app.get('/', (req, res) => {
    res.send("<h1>Welcome to Food Order</h1>")
});

// Starting the server and listening on the specified port.
app.listen(port, () => {
    console.log('Server started at ' + port);
});
```

### Step 6: Implement JWT Authentication Middleware - `auth.js`

Create a file named `auth.js` inside the `middleware` directory.

```javascript
// Importing the 'jsonwebtoken' library for JWT operations
const jwt = require('jsonwebtoken');

// Middleware function for checking authentication
function checkAuth(req, res, next) {
    try {
        // Verifying the authenticity of the JSON Web Token (JWT)
        // Extracting the token from the 'token' header of the 'req' object
        // Verifying the token using the 'jsonwebtoken' library and the secret key 'myPrivateKey'
        jwt.verify(req.headers.token, 'myPrivateKey');
        
        // If the token is valid, call the 'next' function to pass control to the next middleware or route
        next();//--> food api
    }
    catch (error) {
        // If an error occurs during token verification (e.g., token is invalid or expired), execute the following block

        // Send a JSON response back to the client with status code 200 (OK)
        // The response contains a message indicating that the token is not valid or has expired
        return res.status(200).json({ 'message': 'Token is not valid or expired' })
    }
}

// Exporting the 'checkAuth' middleware function to be used in other parts of the application
module.exports = checkAuth;

// Logging a message to the console to indicate that the middleware is working
console.log('checkauth middleware is working');
```

### Step 7: Protect Food API with `checkAuth` Middleware

In this step, we will protect the food-related routes in `food.router.js` using the `checkAuth` middleware. By adding `checkAuth` as a second argument to the route handlers, these routes will require authentication through JWT before they can be accessed.

1. Open the `food.router.js` file inside the `routes` directory.

2. Import the `checkAuth` middleware at the beginning of the file:

```javascript
// consuming the checkAuth middleware
const checkAuth = require('../middleware/auth');
```

3. Apply the `checkAuth` middleware to the food-related routes:

```javascript
// Route to fetch all foods info from MongoDB
foodRouter.get('/foods', checkAuth, (req, res) => {
    // ... (code to fetch all food items from MongoDB)
});

// Route to fetch a specific food item by its ID from MongoDB
foodRouter.get('/food/:id', checkAuth, (req, res) => {
    // ... (code to fetch a specific food item by ID from MongoDB)
});

// Route to fetch food items within a given price range from MongoDB
foodRouter.get('/food/:lim1/:lim2', checkAuth, (req, res) => {
    // ... (code to fetch food items within a given price range from MongoDB)
});

// Route to adding a new food information into the database.
foodRouter.post('/food', checkAuth, (req, res) => {
    // ... (code to add a new food item to the database)
});

// Route to delete a specific food item by its ID from MongoDB
foodRouter.delete('/food/:id', checkAuth, (req, res) => {
    // ... (code to delete a specific food item by ID from MongoDB)
});

// Route to update a specific food item by its ID in MongoDB using PUT or PATCH
foodRouter.all('/food/:id', checkAuth, (req, res) => {
    // ... (code to update a specific food item by ID in MongoDB)
});
```

Now, the `checkAuth` middleware is used in the `foodRouter` to protect the food-related routes. By adding `checkAuth` as a second argument to the route handlers, those routes will require authentication through JWT before they can be accessed.

### Step 8: Test the API

1. Start the server by running the following command in the terminal:

```bash
node main.js
```

2. Use tools like Postman or any REST client to test the API endpoints:

   - User Signup: POST http://localhost:3000/users/signup
   - User Signin: POST http://localhost:3000/users/signin
   - Protected Food API: GET http://localhost:3000/api/foods (requires valid JWT token in the 'token' header)

3. Observe the responses and verify that the user authentication and food API protection are working as expected.

That's it! It is successfully implemented user authentication using JWT in the Food Order API. We can further enhance the API by adding more features, error handling, and validation as per our requirements. Happy coding!
