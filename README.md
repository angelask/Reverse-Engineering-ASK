# Reverse-Engineering-ASK
Unit 14 Sequlize Homework Reverse Engineering Code

For any of the code to work npm install is used to install myspl2 and sequelize packages on a local level and globally install sequelize-chi npm package. 

To set up Sequelize Project. Go to the root of the project directory and run “sequelize init:config & sequelize init:models in the bash terminal. This will create a few modules folders and files.

•	Config/config.json
•	Models/index.js

Middlewear will restrict the user from a route if not logged in, they will be redirected to login page. This code is boilerplate and will not change.

Next the database is connected

Config.json stores JSON with details about the environment. Open the file and complete the development section with mysql username “root” mysql password, database name, host number and dialect. Most of the information will be listed, verify for accuracy.  This will connect the database.  Passport.js will enable the programmer to login with local strategy username/email and password. To keep authentication state across HTTP request this file will also serialize and deserialize the user, it is boilerplate and will not change
Models folder contains two files

Index.js defines all the sequelize models for our database. This file will figure out which database to deploy depending on if the programmer will use Heroku (production) or run locally (development). Config.json will determine the correct configuration that is required. This file can also specify a database to be used for testing if the programmer requires it.  The Index file will then run through all the other javascript files inside the models folder and runs them through Sequelize using helper methods making sure all the associations between models are properly set up. It then exports an opject that will be used to interface with Sequelize in the other files.

User.js brings in bcryptjs a javascript program used to protect against rainbow table attacks which functions over time. It is also used to create a Sequelize model to export a function that takes two variables `sequelize and DataTypes`.  Sequelize is our connection to the database. DataTypes will be used to define what type of data each property on our model should be. A user variable is defined to run the function sequelize.define method it will pass two arguments, the name of our model as a string, and an object describing our model’s schema. Each property will represent a column in the database. sequelize.define returns an object, which we store inside the variable “User”. We return this variable at the end of the function.

Public folders are front end user interface files. These files include HTML, javascript and css for styling.

There are 3 javascript files/ 3 html files and one stylesheet.

•	Login.js/login.html used to validate user email address and password, if successful the code will redirect user to members page and clear form.  If user name and password cannot be verified, the code will redirect user to signup page.  If there is an error the error will be logged.

•	Member.js/member.html this file does a get request to determine which user is currently logged in.

•	Signup.js/signup.html To signup user will use the form to create username and password. Once the signup button is submitted form is not blank. If successful, the code will redirect user to members page. Error handling function is used to catch errors.

•	Style.css is used to set margins on the signup and login form.

Routes
Routes are ways that we can handle user navigation to various URLs throughout our application.

Routes included the following files api-routes.js and html-routes.js 
api-routes.js requires the models and passport packages. A function is created for user authentication called passport.authenticate. If a user has valid credentials they may proceed to members page, otherwise they receive an error.  This route allows the user to sign up with password which is automatically hashed and securely stored. If user is not successful they receive an error 401. Lastly there is a logout function 
html-routes.js requires path to be able to use a relative route to our html file. Authenticated is also required to verify user is accurately logged in. It will then send them to the members page. Code is written so that iif a member is not properly logged in, they cannot proceed to the member page but will instead be redirected to the signup page.

Server.js
The server.js file is used to create tables from our models, we need to sync them with our database. To do this, we’ll utilize the sequelize.sync() method.  The beginning of the code is used to require all packages, models, express, express-sessions, passport. We also require the routes html and api. The port is defined as 8080. Then we sync our database. The sequelize property on the db object is actually our connection to our database. ‘sync’ is a built in sequelize method that creates tables using the models we describe. After our database is sync’ed (this may take a certain amount of time) we start our express server. Using this method, we guarantee that our server won’t start before our database is ready. We also guarantee that our server won’t start 6 if there’s an error connecting to our database.

https://drive.google.com/file/d/1grxBGUcdieSOy-_sYK4nk0-7MK7nDjHa/view?usp=sharing
