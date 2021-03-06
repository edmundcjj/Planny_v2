# planny-v2

This is a self project of my own to practice creating a full stack web application using the various tech stacks. A personal itinerary planner where one can plan an itinerary for a holiday trip so that one does not get so lost not knowing what to do during the trip.

You can view the complete app here - https://itinerary-planner.herokuapp.com/


## Getting Started

The instructions below will get you a copy of the project up and running on your local machine for development and testing purposes. See deployment section for notes on how to deploy the project on a live system.


### Prerequisites

Make sure to download and install the following items
* Text Editor - Up to your own preference, I personally prefer atom (https://atom.io/)
* Node.js - https://nodejs.org/en/
* PostgreSQL - https://www.postgresql.org/download/
* Heroku CLI - https://devcenter.heroku.com/articles/heroku-cli
* Git - https://git-scm.com/

Do remember to check that the environment variables are updated with the above items
![alt text](https://i.imgur.com/AmKg1k8.png)


### Installation

Once you are done with the prerequisites, let's move on to the installation. Note that the next few steps are meant for localhost development only.

**Step 1** => Fork the project to your own github account

**Step 2** => Git clone the project to your local computer directory using a terminal
![alt text](https://i.imgur.com/7nUYl4T.png)

**Step 3** => In the terminal, dive down to the cloned project folder and type the command "npm install"
![alt text](https://i.imgur.com/unCQuUu.png)
This command will install all the packages required for this particular project

**Step 4** => Get a google developers api key and update it in the code wherever needed. Visit https://developers.google.com/places/web-service/get-api-key to see how to get a api key.

**Final step** => In the terminal, type the command "nodemon index.js", launch the browser and type in the address as shown in the picture, you will see the default page.
![alt text](https://i.imgur.com/2gVDwtT.png)


## Deployment

The following steps below will show you how to deploy your local project to Heroku so that it is publicly accessible.

**Step 1** => Create an account with heroku.

**Step 2** => Make sure the code shown below exists in the package.json file
![alt text](https://i.imgur.com/GluENIY.png)
Do remember to edit the version of node with the version you have installed in your local system!

**Step 3** => Open git cmd, type the command "heroku login" and enter your credentials
![alt text](https://i.imgur.com/5RjmuJ7.png)

**Step 4** => Open another git cmd, dive down to the project folder and type the command
```
heroku create sitename
```
where sitename is the name of your app. This will create a url like: http://sitename.herokuapp.com"

**Step 5** => In the same git cmd in step 4, enter the following command to push your project to heroku
```
git push heroku master
```

**Step 6** => Similarly to step 5, enter the following command
```
heroku ps:scale web=1
```
This will ensure you have at least one dyno(process) running.

**Step 7** => Click the link below to add the heroku postgres addon to your heroku project
```
https://elements.heroku.com/addons/heroku-postgresql
```

**Step 8** => Ensure that the following piece of code exists in the db.js file
```
// inside of db.js

//require the url library
//this comes with node, so no need to yarn add
const url = require('url');

//check to see if we have this heroku environment variable
if( process.env.DATABASE_URL ){

  //we need to take apart the url so we can set the appropriate configs

  const params = url.parse(process.env.DATABASE_URL);
  const auth = params.auth.split(':');

  //make the configs object
  var configs = {
    user: auth[0],
    password: auth[1],
    host: params.hostname,
    port: params.port,
    database: params.pathname.split('/')[1],
    ssl: true
  };

}else{

  //otherwise we are on the local network
  var configs = {
      user: 'akira',
      host: '127.0.0.1',
      database: 'pokemons',
      port: 5432
  };
}

//this is the same
const pool = new pg.Pool(configs);
```

**Step 9** => Create database tables on the heroku db in the same git cmd in step 6
```
heroku pg:psql < tables.sql
```

**You are now ready to launch the app deployed to heroku. You can launch the app in your heroku dashboard**


## Wireframes

The following below shows the wireframes I came up with during the planning process.
![alt text](https://i.imgur.com/pBR5YOP.png)


## ERD Diagrams

The following shows the relationships between the various database tables for this project.
![alt text](https://i.imgur.com/AB7fxI5.png)

## User Stories
Click this link to view the user stories for this project - https://trello.com/b/KRfeVL3E


## Built With
**Frameworks**
* [Node](https://expressjs.com/en/4x/api.html) - Open-source, cross-platform JavaScript run-time environment that executes JavaScript code server-side.
* [Express](https://expressjs.com/en/4x/api.html) - The back-end web framework used for node.js
* [MDBootstrap](https://mdbootstrap.com/) - The front-end framework used that aligns with Google Material Design

**NPM Packages**
* [NPM request](https://www.npmjs.com/package/request) - To handle api calls to external APIs
* [NPM express](https://www.npmjs.com/package/express) - Fast, unopinionated, minimalist web framework for node.
* [NPM express-handlebars](https://www.npmjs.com/package/express-handlebars) - Handlebars view engine for Express web framework
* [NPM bcrypt](https://www.npmjs.com/package/bcrypt) - Library to help with hashing passwords
* [NPM body-parser](https://www.npmjs.com/package/body-parser) - Parse incoming request bodies in a middleware before your handlers, available under the req.body property.
* [NPM cookie-parser](https://www.npmjs.com/package/cookie-parser) - Parse Cookie header and populate req.cookies with an object keyed by the cookie names. Optionally you may enable signed cookie support by passing a secret string, which assigns req.secret so it may be used by other middleware.
* [NPM method-override](https://www.npmjs.com/package/method-override) - Lets you use HTTP verbs such as PUT or DELETE in places where the client doesn't support it.
* [NPM nodemon](https://www.npmjs.com/package/nodemon) - nodemon will watch the files in the directory in which nodemon was started, and if any files change, nodemon will automatically restart your node application.
* [NPM pg](https://www.npmjs.com/package/pg) - Non-blocking PostgreSQL client for node.js. Pure JavaScript and optional native libpq bindings.

**Database**
* [PostgreSQL](https://www.postgresql.org/) - Open Source Database

**APIs**
* [Google Place Details](https://developers.google.com/places/web-service/details) - Google Place Details API
* [Google Place Autocomplete](https://developers.google.com/places/web-service/autocomplete) - Google Place Autocomplete API
