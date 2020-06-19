# Files 
___
## Config
___
### -isAuthenticated.js
    This folder contains a function that checks if there is a current authenticated user and if it does then it lets the browser continue on. If not it redirects the user to the signin page.

### -passport.js
    reuires both the passport node package as well as assigning the passport local stratagy to a constructor function for localstrategy

    local stratagey has a function that searches the database for a user matching the email provided. it then checks both the email and if the password provided matches the selected password. if either fail it sends and error back but if both pass it then lets returns the user in the done function. 

### -config.json
    This file contains databse connection information.

## models
___
### index.js
    this file passes back all models used by squilize to create and interact with tables for the db

### user.js
    This is a model file that creates a model for the user table as well as adding a prototype method for comparing and validating encypted passwords.
        -note bcryptjs is required in the file to work with encypted information
## Public
___
*I am combining the js and html files that have the same name for the sake of brevidy.*
### login js/html
    login page has a form that allows for the submitting of a user email and password. as well as a link to the signup page

    login.js has a link to the login button that takes the form data then sends a post request to the api/login route (email/password) then attempts to load the /members page.

### members js/html
    members page has has a welcom page with the users name and a logout button that sends a get request to /logout.

    members.js simply sents a get request to api/user_data and writes a name to the member name class area (is email)

### signup js/html
    Signup page is very similar to login in form but instead of sending data to be checked and loged in it insead sends information to be submitted into the database and then redirects to /members like login.
## Routes
___
### api.routes.js
    these are the API routes for accessing and using data tools created in the config/models folders.

    - (post) /api/login - sends a post requestand attempts to use passport.authenticate to validate login. if pass it returns user info if not it returns errors discribed above

    - (post) /api/signup - sends a post request with a user.create call to send form data to database and create a new entry.

    - (get) /logout - runs the logout method to clear the active user and then redirects to ("/") which is the signup page.

    - (get) /api/user_data -  if there is no user it returns a empty object if there is user data it returns an object with email and id.

### html-routes.js
    three simple get calls to send the html files to be rendered for members/loging/signup. also retuires the isAuthenticated file to a function that is used in the /members route to verify if the login attempt is matches data in the database.

## server.js
___
    - Requires express and passport
    - has app.use lines to allow for sending files and sets the public folder as the static files used in the exress server file rendering.
    - Requires routes for express server
    -launches server on specified port (has both a local port and enviromental port for deployment online)

# dependancies
 
## PassportJS - local statagy
    a node package (local stratagy specified) that allows for local user authentication via information submitted to a database. Local statagy provides the constructor function used when creating and checking user cerdentials

## mysql/squilize
    used to create and interact with a database. Squilize allows for models to be used to create and interact with tables.

## bcryptjs
    used to hash passwords for security when checking for a valid password and storing it

## express server
    used to create a listending server that can make the needed get and post calls for the application
