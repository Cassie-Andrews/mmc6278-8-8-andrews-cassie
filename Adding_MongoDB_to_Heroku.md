# Adding MongoDB to a Heroku Application

(**NOTE:** View a rendered version of this file in VS Code with `ctrl-shift-v` or `cmd-shift-v`)

&nbsp;
## Introduction to MongoDB Atlas 🍃

Much like JawsDB for MySQL, [MongoDB Atlas](https://www.mongodb.com/atlas) is a database as a service (DAAS) for MongoDB. MongoDB also offers a generous free tier for projects that will suit our purposes. Unfortunately, there is no Heroku integration for MongoDB, so you'll need to set things up through the MongoDB Atlas site and manually connect through Heroku.

&nbsp;
## Instructions

To connect MongoDB Atlas to a Heroku app:

1. Create a Heroku app like you normally would through the Heroku dashboard (or the CLI if you're so inclined).
1. [Sign up for a MongoDB Atlas Account](https://www.mongodb.com/cloud/atlas/register). Just put "None" for company.
1. Verify your email and then answer the questions about why you're using MongoDB. I selected "learn MongoDB" for purpose and that I was building a blog for the application being built question.
1. On the "Deploy a cloud database" page, select the "Free Shared" tier and click "create".
1. Leave the default settings as-is (AWS US East Virginia region, etc.) and click "Create Cluster".
1. This should launch you into "Security Quickstart". Create a database user by entering a username and password (I recommend generating the password). Be sure to save this password and the username that you create.
1. Under "Where would you like to connect from?", you should see an option to add IP addresses to a the access list. This is a whitelist of allowed IP addresses that can connect to your MongoDB database. Enter 0.0.0.0 and add the description "internet" and click "Add entry".
    * **NOTE:** 0.0.0.0/0 as a value essentially means that any address on the internet can connect to your application. For our purposes, we'll be connecting from our personal computer as well as letting our application on Heroku connect to this database. We're still protected through our username and password, but we could make this more secure by only allowing certain addresses to connect.
1. Click finish to close the security quickstart and click "Database" in the menu on the left under "Deployment".
1. Next to Cluster0, click "Connect" and "Connect your application".
1. You should now see a URI that looks like: `mongodb+srv://<username>:<password>@<cluster_number>.<letters>.mongodb.net/<database_name>?retryWrites=true&w=majority`
1. Copy this URL, but replace the username and password with your database username/password from the previous steps. In the spot between `mongodb.net/` and the `?`, add the database name. For the mongo blog assignment, use  `mongo_blog`. Ex: `mongodb+srv://myuser:mypass@cluster0.abcdefg.mongodb.net/mongo_blog?retryWrites=true&w=majority`
    * **NOTE:** If you don't add the database name to the URI, your application will save everything under the "test" database.
1. Go back to Heroku and open the dashboard for your application that you'ld like to connect to MongoDB.
1. Click the settings tab and "reveal config vars".
1. Add a variable for MONGODB_URI and set the value to the URI from the previous steps.

When you deploy your application to Heroku, it should connect to the production MongoDB instance as long as your connection is configured correctly to use the `process.env.MONGODB_URI` variable if available (See `config/connection.js` of the Mongo blog assignment for an example).

&nbsp;
## Schema and Seeding MongoDB 🌱

MongoDB is unlike MySQL in that NoSQL databases do not require schema to be set before using them. However you will still need to seed your Mongo database (including for the Mongo Blog assignment).

In order to connect to your production MongoDB database, use the same MongoDB URI to connect like you did in the steps above when connecting to Heroku. You can either use a tool like [Studio 3t](https://robomongo.org/) or an extension like [MongoDB for VS Code](https://marketplace.visualstudio.com/items?itemName=mongodb.mongodb-vscode) to connect to your production database to review or modify data.

You could also seed your database with these tools if you wished, but I prefer using JavaScript and Mongoose to seed MongoDB since we've usually already set up all the steps to connect to MongoDB in our project. If we do things this way, we'll protect ourselves from entering incorrect data because we'll be using the same rules we use for our application with Mongoose to insert data. In the mongo blog assignment, you'll see an example of this under `seed/seed.js`.

This file pulls in the `config/connection.js` file using `require` which causes the file to run and connect to MongoDB inside of Mongoose. It then imports the model files from `/models` and uses the `create` method to create multiple entries in the various collections all using JavaScript.

Because `config/connection.js` defaults to using the `MONGODB_URI` string if it exists, this file can also be used to seed the production database.

In the terminal, run `export MONGODB_URI="your_connection_string"` then `node seed/seed.js` and the script will connect to the production database and insert documents there instead of locally.

**NOTE:** Don't forget to either close your terminal or run `export MONGODB_URI=` to clear the URI from your environment, otherwise you may continue to connect to production when running the application locally.