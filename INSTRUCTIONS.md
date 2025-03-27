# Module 8 Assignment: MongoDB and the Mongoose ORM

(**NOTE:** View a rendered version of this file in VS Code with `ctrl-shift-v` or `cmd-shift-v`)

&nbsp;
## Introduction

For this assignment, you will be creating a blog website using MongoDB. The blog application allows readers to read and comment on posts, view posts by tag, and allows an admin user to login and edit/create posts as well as remove comments.

[You can see an example of the completed application here](https://mongodb-blog-example.herokuapp.com/).

[Click here to access the admin login page](https://mongodb-blog-example.herokuapp.com/admin/).

* Username: `albertgator`
* Password: `twofoursixbitsdollar`

&nbsp;
## Setup

Copy the starter files inside of `unsolved` into the root directory of your GitHub repository.

Ensure you include a `.gitignore` file in your repo that includes at minimum:

```
**/.DS_Store
**/node_modules/
.env
```

Run `npm i` in the root directory of your repository (your `package.json` should be in the root directory).

You'll see that there is a `.env.EXAMPLE` file included in the unsolved folder. You'll need to create a `.env` file with the same contents, but replace the fake session key with your own value. This can be any string of words or characters (no spaces).

&nbsp;
## Instructions

The first thing you'll need to do is code the Mongoose models in the `/models` folder. Follow the instructions in each file to add the correct properties to each model. You must complete the model files before the automated tests will run.

Next, navigate to `/controllers/post.js` and finish implementing the `get`, `create`, `update`, and `remove` methods.

Finally, deploy your application to [Heroku](https://www.heroku.com/) and use MongoDB for the production database. [Please see this guide for instructions on adding MongoDB to Heroku](./Adding_MongoDB_to_Heroku.md).

&nbsp;
## App Behavior

The completed application should behave in the same manner as [this example](https://mongodb-blog-example.herokuapp.com/).

To run the application locally, run:

```
npm run dev
```

You can then navigate to [http://localhost:3000](http://localhost:3000) to view the application.

&nbsp;
## Testing

Automated tests are included with this assignment. To receive full credit, all automated tests must pass.

To run the tests once, run:

```
npm test
```

To run the tests in watch mode, run:

```
npm run test:watch
```

&nbsp;
## Requirements for full credit

To receive full credit for this assignment, your program MUST:

  * Be implemented according to the above [instructions](#instructions).
  * Be deployed to Heroku with a MongoDB-powered database that is seeded.
  * Pass all automated tests.

&nbsp;
## Submission

When submitting this assignment, please include:

  * A link to the assignment's GitHub repository.
  * A link to the deployed application on Heroku.
  * A screenshot of the automated test results.