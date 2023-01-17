---
title: The MERN Stack
date: '2023-01-17'
tags: ['multi-author', 'next-js', 'feature']
draft: false
summary: 'This tutorial covers the basics of the MERN stack and shows how to build a simple CRUD application from scratch using it.'
---

This tutorial will demonstrate the functionality of the MERN stack by configuring the server side with Node.js and Express.js connected to MongoDB. Then, you will create several APIs. Afterwards, you will be guided through the process of building the frontend using React for user interfaces. Once both the backend and frontend are completed, you will connect them together.

# Overview: An Examination of the Term MERN Stack

[MongoDB:](https://www.mongodb.com/docs/) a cross-platform document-oriented database program

[Express.js:](http://expressjs.com/en/starter/installing.html) a web application framework for Node.js

[React:](https://reactjs.org/docs/getting-started.html) a JavaScript library for creating user interfaces

[Node.js:](https://nodejs.org/en/docs/) An open source, cross-platform, JavaScript run-time environment that executes JavaScript code outside of a browser

All of these make up the MERN stack, a collection of technologies that simplify application development. The backend is built using MongoDB, Express.js, and Node.js, and the frontend is powered by React. According to the most recent Stack Overflow developer survey, Node.js and React are presently among the most utilized web frameworks and technologies, and MongoDB is also frequently used. MERN stack developers are in high demand, but getting there requires patience and a solid grounding in JavaScript.

## Setup the Server with Node and Express

The MERN configuration is intended to be highlighted by this brief demo. In order to utilize it as a boilerplate and raise your MERN stack projects to industry standards, the goal is to create a straightforward project with the best structure available.

Our MERN stack lesson begins with a brief demo on how to build up a server using Express.js and Node.js

### npm init

Enter the folder through the terminal, then type `$ npm init -y` to create the project folder. This will generate an empty npm project with the default settings.

You'll then get something that looks like this:

![npm-init](/static/images/posts/mern/npm-init.png)

If you want to modify the default settings, simply open the package.json file that was created.

### Install Dependencies

Dependencies are the essential functionalities, libraries or pieces of code that are essential for parts of our code to work.

With the help of `$ npm i express mongoose body-parser config`, we'll then install a few dependencies. Hit the Enter key after typing or copying the aforementioned command. What you'll see will resemble this:

![dependencies](/static/images/posts/mern/dependency.png)

This will install the following dependencies for our project:

[body-parser:](https://www.npmjs.com/package/body-parser) Allows us to get the data throughout the request

[express:](https://www.npmjs.com/package/express) our main framework

[mongoose:](https://www.npmjs.com/package/mongoose) used to connect and interact with MongoDB

[config:](https://www.npmjs.com/package/config) allows you to define default parameters for your application

The command `$ npm I -D nodemon` can be used to add nodemon as an optional development dependency. Update the scripts part of your package.json file to include `"app": "nodemon app.js"` in order to use nodemon. By doing this, it will be made sure that the server restarts itself everytime the source code is modified.

The application is launched from the app.js file. It's crucial to include a start script definition in the package. "start" in a json file should be "node app.js." This will include the command to launch the program.

After making these modifications, your package.json file ought to resemble the following illustration:

![example-json](/static/images/posts/mern/example-json.png)

### Setting the Entry Point

Create a file called `app.js` as our entry point right away. By using the `$ touch app.js` command from the project folder, you can create this file (on macOS and Linux).

paste the subsequent code:

```
// app.js

const express = require('express');

const app = express();

app.get('/', (req, res) => res.send('Hello world!'));

const port = process.env.PORT || 8082;

app.listen(port, () => console.log(`Server running on port ${port}`));
```

After completing the necessary setup, run the command `$ node app` to start the server. You will see the message `Server running on port 8082` in the console. To confirm that the server is running, you can open a browser and navigate to `http://localhost:8082`.

If you do not set up nodemon, you will need to manually restart the server every time you make changes to the code. However, if you have set up nodemon, it will automatically detect changes and restart the server for you, eliminating the need for manual restarts.

To set up nodemon, make the following changes to the scripts section in your package.json file:

```
// package.json

{
  "name": "mern-demo",
  "version": "1.0.0",
  "description": "",
  "main": "app.js",
  "scripts": {
    "start": "node app.js",
    "app": "nodemon app.js",
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "repository": {
    "type": "git",
    "url": "git+https://github.com/nurislam03/MERN_A_to_Z.git"
  },
  "author": "Nur Islam",
  "license": "MIT",
  "bugs": {
    "url": "https://github.com/nurislam03/MERN_A_to_Z/issues"
  },
  "homepage": "https://github.com/nurislam03/MERN_A_to_Z#readme",
  "dependencies": {
    "body-parser": "^1.19.0",
    "express": "^4.17.1",
    "mongoose": "^5.5.15",
    "validation": "0.0.1"
  },
  "devDependencies": {
    "nodemon": "^1.19.1"
  }
}
```

The command `$ npm run app` should now be entered to start your project. To debug and fix any issues that may have arisen up to this point, you can try executing the commands listed below:

```
$ npm install
$ npm run app
```

You should now see an output like this in your terminal:

![output-sample](/static/images/posts/mern/output-sample-terminal.png)

## Managing the Database with MongoDB

It's time to go to work setting up our MongoDB MERN database. We will make use of MongoDB Atlas for simplicity. Make an account here first. Following account creation, you will see something similar to this:

![mongo-db](/static/images/posts/mern/mongo-db.webp)

There is a button for creating a new project when you click the Project 0 area in the top left corner. Create a project, then choose it. Now, from the project you just established, click the Build a Cluster button. You will be shown all the data.

You can name the database by clicking the Cluster Name area at the bottom, then clicking the Create Cluster button. If everything goes according to plan, you should find something like this after two to three minutes:

![cluster-mongo-db](/static/images/posts/mern/cluster-mongo-db.webp)

After selecting CONNECT, enter your database's login and password on the following form:

![connection-mongo-db](/static/images/posts/mern/connetion-mongodb.webp)

Select the Create MongoDB User button at this point. Additionally, you have the option of selecting either your current IP address or a different IP address. Now, you can view various methods by clicking the CONNECT button or the Choose a connection method button. Choose appropriately:

![mern-stack-a-z](/static/images/posts/mern/mern-stack-a-z.webp)

Choose the Connect Your Application section in this instance. You will now receive the database URL that we will utilize in the following step:

![mern-stack-a-z-two](/static/images/posts/mern/mern-stack-a-z-two.webp)

### Integrate the Database into your Project

We need to incorporate our completed database into our project. Create the files default.json and db.js inside the project folder, as well as the config folder.

Add the next bit of code:

```
// default.json

{
  "mongoURI":
    "mongodb+srv://mern123:<password>@mernatoz-9kdpd.mongodb.net/test?retryWrites=true&w=majority"
}
 /* Replace <password> with your database password */
// db.js

const mongoose = require('mongoose');
const config = require('config');
const db = config.get('mongoURI');

const connectDB = async () => {
  try {
    mongoose.set('strictQuery', true);
    await mongoose.connect(db, {
      useNewUrlParser: true,
    });

    console.log('MongoDB is Connected...');
  } catch (err) {
    console.error(err.message);
    process.exit(1);
  }
};

module.exports = connectDB;
```

To connect to the database, we need to make a small change to our app.js file. This is an update for your app.js:

```
// app.js

const express = require('express');
const connectDB = require('./config/db');

const app = express();

// Connect Database
connectDB();

app.get('/', (req, res) => res.send('Hello world!'));

const port = process.env.PORT || 8082;

app.listen(port, () => console.log(`Server running on port ${port}`));
```

The project can now be launched by using the $ npm run app command. Watch out for a message to print out that says "MongoDB is Connected..."

Great! So far, everything is going well, and we have successfully connected to our database. It's time to finish setting up the routes before moving on to creating RESTful APIs.

### Build RESTful APIs with the MERN stack

Make a folder called `routes` to get things going. Create a folder inside it called api to house all of our APIs. Create a `book.js` file inside the `api` folder. To demonstrate how it functions, we will shortly provide some APIs here.

Paste the following code into `books.js`:

```
// routes/api/books.js

const express = require('express');
const router = express.Router();

// Load Book model
const Book = require('../../models/Book');

// @route GET api/books/test
// @description tests books route
// @access Public
router.get('/test', (req, res) => res.send('book route testing!'));

// @route GET api/books
// @description Get all books
// @access Public
router.get('/', (req, res) => {
  Book.find()
    .then(books => res.json(books))
    .catch(err => res.status(404).json({ nobooksfound: 'No Books found' }));
});

// @route GET api/books/:id
// @description Get single book by id
// @access Public
router.get('/:id', (req, res) => {
  Book.findById(req.params.id)
    .then(book => res.json(book))
    .catch(err => res.status(404).json({ nobookfound: 'No Book found' }));
});

// @route GET api/books
// @description add/save book
// @access Public
router.post('/', (req, res) => {
  Book.create(req.body)
    .then(book => res.json({ msg: 'Book added successfully' }))
    .catch(err => res.status(400).json({ error: 'Unable to add this book' }));
});

// @route GET api/books/:id
// @description Update book
// @access Public
router.put('/:id', (req, res) => {
  Book.findByIdAndUpdate(req.params.id, req.body)
    .then(book => res.json({ msg: 'Updated successfully' }))
    .catch(err =>
      res.status(400).json({ error: 'Unable to update the Database' })
    );
});

// @route GET api/books/:id
// @description Delete book by id
// @access Public
router.delete('/:id', (req, res) => {
  Book.findByIdAndRemove(req.params.id, req.body)
    .then(book => res.json({ mgs: 'Book entry deleted successfully' }))
    .catch(err => res.status(404).json({ error: 'No such a book' }));
});

module.exports = router;
```

### Database Model

We must develop a model for each of our resources before we can communicate with our database. Create a folder called models in the root and then change Book.js in that folder with the following code:

```
// models/Book.js

const mongoose = require('mongoose');

const BookSchema = new mongoose.Schema({
  title: {
    type: String,
    required: true
  },
  isbn: {
    type: String,
    required: true
  },
  author: {
    type: String,
    required: true
  },
  description: {
    type: String
  },
  published_date: {
    type: Date
  },
  publisher: {
    type: String
  },
  updated_date: {
    type: Date,
    default: Date.now
  }
});

module.exports = Book = mongoose.model('book', BookSchema);
```

Run the project after that to verify that everything is working as it should, and use Postman to test all the APIs. It's vital to remember that you must run the project first before testing APIs with Postman.

### Authenticate and Authorize Users

Web applications must provide authentication and permission. Authentication is the process of confirming a person's claims of identity. The process of determining the user's access level is called authorization.

The majority of the time, developers utilize JWT as an authentication technique when using a Node.js backend and a React frontend. JSON Web Tokens are known as JWTs. JWTs are encoded, URL-safe strings with limitless data storage capacity.

A React fronted often transmits a JWT to the backend. If the token is legitimate, the backend verifies it and executes the necessary activities.

## Build the Frontend

All is well thus far! It's time to move on to the frontend section of our MERN stack tutorial now that we have our backend setup. React will be used in this section to create the user interfaces. Our basic file setup will be generated using Create React App.

Additionally, to bundle our modules and create our JavaScript, we'll utilize Babel and webpack, accordingly. You don't need to install or configure technologies like webpack or Babel if you don't have much experience with them. To allow you to concentrate on the code, they are pre-configured and hidden.

You only need to create a project to get started. Additionally, you'll need to have Node.js 8.10 or later and npm 5.6 or later installed on your computer.

### Setup Create React App

Run `$ npx create-react-app my-app` to obtain the first setup file after setting any directory in a terminal as the location for all the project's files.

You can provide any other name for your project in place of `my-app`.

Note: The project name needs to be written in lowercase. If all goes according to plan, you should see something similar to the following image, which also includes some instructions ([update node](https://www.linode.com/docs/guides/how-to-update-nodejs/), if required):

In order to use the built-in commands for your project, you will first need to navigate to the project folder by running the command `$ cd [your_project_folder]`.

Once inside the project directory, you can use the available commands. If you are using Yarn, enter `$ yarn start`. If you are using npm, enter `$ npm start`.

Both of these commands will run the app in development mode. Now, open http://localhost:3000 to view it in the browser. This page will automatically reload if you make changes to the code:

![react-logo](/static/images/posts/mern/react-app-browser.webp)

The project directory structure looks like this:

![mern-stack-folder](/static/images/posts/mern/mern-stack-folder.webp)

### Add Bootstrap and Font Awesome to your React App

Bootstrap is a popular CSS framework that provides a variety of components and styles that can be used to create a responsive and attractive website. Font Awesome is a popular icon library that provides a variety of icons that can be used to create a website with a professional look and feel.

Open the index.html file located in the mern a to z client/public/index.html folder, and replace all of the code with the following:

```
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8" />
    <link rel="shortcut icon" href="%PUBLIC_URL%/favicon.ico" />
    <meta name="viewport" content="width=device-width, initial-scale=1" />
    <meta name="theme-color" content="#000000" />
    <!--
      manifest.json provides metadata used when your web app is installed on a
      user's mobile device or desktop. See https://developers.google.com/web/fundamentals/web-app-manifest/
    -->
    <link rel="manifest" href="%PUBLIC_URL%/manifest.json" />
    <!--
      Notice the use of %PUBLIC_URL% in the tags above.
      It will be replaced with the URL of the `public` folder during the build.
      Only files inside the `public` folder can be referenced from the HTML.

      Unlike "/favicon.ico" or "favicon.ico", "%PUBLIC_URL%/favicon.ico" will
      work correctly both with client-side routing and a non-root public URL.
      Learn how to configure a non-root public URL by running `npm run build`.
    -->

    <!-- bootstrap css cdn -->
    <link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/4.0.0/css/bootstrap.min.css" integrity="sha384-Gn5384xqQ1aoWXA+058RXPxPg6fy4IWvTNh0E263XmFcJlSAwiGgFAW/dAiS6JXm" crossorigin="anonymous">

    <!-- fontawesome cdn -->
    <link rel="stylesheet" href="https://use.fontawesome.com/releases/v5.2.0/css/all.css" integrity="sha384-hWVjflwFxL6sNzntih27bfxkr27PmbbK/iSvJ+a4+0owXq79v+lsFkW54bOGbiDQ" crossorigin="anonymous">

    <title>MERN A to Z</title>
  </head>
  <body>
    <noscript>You need to enable JavaScript to run this app.</noscript>
    <div id="root"></div>
    <!--
      This HTML file is a template.
      If you open it directly in the browser, you will see an empty page.

      You can add webfonts, meta tags, or analytics to this file.
      The build step will place the bundled scripts into the <body> tag.

      To begin the development, run `npm start` or `yarn start`.
      To create a production bundle, use `npm run build` or `yarn build`.
    -->

    <!-- bootstrap JS cdn -->
    <script src="https://code.jquery.com/jquery-3.2.1.slim.min.js" integrity="sha384-KJ3o2DKtIkvYIK3UENzmM7KCkRr/rE9/Qpg6aAZGJwFDMVNA/GpGFF93hXpG5KkN" crossorigin="anonymous"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/popper.js/1.12.9/umd/popper.min.js" integrity="sha384-ApNbgh9B+Y1QKtv3Rn7W3mgPxhU9K/ScQsAP7hUibX39j7fakFPskvXusvfa0b4Q" crossorigin="anonymous"></script>
    <script src="https://maxcdn.bootstrapcdn.com/bootstrap/4.0.0/js/bootstrap.min.js" integrity="sha384-JZR6Spejh4U02d8jOt6vLEHfe/JQGiRRSQQxSfFWpi1MquVdAyjUar5+76PVCmYl" crossorigin="anonymous"></script>

  </body>
</html>
```

The following functionalities will be present on our frontend:

Create, add, or store a new book

Display all of the books that we have in our database.

Display just one book

Revise a book

Delete a book

Use the subsequent command to add the required dependencies now:

`$ npm install --save react-router-dom`

`$ npm install --save axios`

## Axios

Similar to a Fetch API, Axios is a lightweight HTTP client for Node.js and the browser. Axios is an async/await library for legible asynchronous code that is promise-based. It is simple to use in any frontend framework and is simple to integrate with React. We'll use Axios to call our APIs.

Axios is frequently used for a variety of factors. The backward compatibility of Axios is one of its main advantages. Axios can even be used with older browsers like IE11 because it internally issues an XMLHttpRequest.

When sending a request, Axios also automatically stringsifies the payload. But it's crucial to transform the payload to JSON when utilizing the Fetch API.

### Package.json

At this point, the code in our package.json file ought to resemble (but not necessarily match) the following:

```
// MERN_A_to_Z_Client - package.json

{
  "name": "mern-demo",
  "version": "0.1.0",
  "private": true,
  "dependencies": {
    "@testing-library/jest-dom": "^5.16.5",
    "@testing-library/react": "^13.4.0",
    "@testing-library/user-event": "^13.5.0",
    "axios": "^1.2.1",
    "react": "^18.2.0",
    "react-dom": "^18.2.0",
    "react-router-dom": "^6.4.5",
    "react-scripts": "5.0.1",
    "web-vitals": "^2.1.4"
  },
  "scripts": {
    "start": "react-scripts start",
    "build": "react-scripts build",
    "test": "react-scripts test",
    "eject": "react-scripts eject"
  },
  "eslintConfig": {
    "extends": [
      "react-app",
      "react-app/jest"
    ]
  },
  "browserslist": {
    "production": [
      ">0.2%",
      "not dead",
      "not op_mini all"
    ],
    "development": [
      "last 1 chrome version",
      "last 1 firefox version",
      "last 1 safari version"
    ]
  }
}
```

### Create the Component Folder

Create a components folder inside the src folder (mern-demo/src/), and then place the following five files there:

CreateBook.js \sShowBookList.js \sBookCard.js \sShowBookDetails.js \sUpdateBookInfo.js
These five files will be used later on in our work.

## React Hooks and Functional Components

React functional components are one of the framework's more recent additions. We only have class-based components before. A JavaScript function that returns a React element or JSX is essentially what makes up a functional component in React. It is possible to write a functional component using the standard keyword or arrow function. The foundation of props is a function argument. A functional component can only be applied to other files after they have been exported:

```
function Hello(props) {
  return <h1>Hello, {props.name}</h1>;
}

export default Welcome;
```

A legitimate React functional component is the example function that was just provided. We shall use functional components in this course. You can read more about React functional components in this post to get a better grasp of them.

Developers could only control state and other React capabilities within class-based components prior to the release of React version 16.8. Developers may now control state and other features within functional components thanks to the addition of Hooks in React version 16.8.

## Setup Routes

We'll use React Router to set up our routes. React Router is a collection of navigational components that compose declaratively with your application. React Router keeps your UI in sync with the URL. It has a simple API with powerful features like lazy code loading, dynamic route matching, and location transition handling built in.

### App.js

Open the App.js file in the src folder (mern-demo/src/), and then replace the code with the following:

```
import { BrowserRouter as Router, Route, Routes } from 'react-router-dom';
import './App.css';

import CreateBook from './components/CreateBook';
import ShowBookList from './components/ShowBookList';
import ShowBookDetails from './components/ShowBookDetails';
import UpdateBookInfo from './components/UpdateBookInfo';

const App = () => {
  return (
    <Router>
      <div>
        <Routes>
          <Route exact path='/' element={<ShowBookList />} />
          <Route path='/create-book' element={<CreateBook />} />
          <Route path='/edit-book/:id' element={<UpdateBookInfo />} />
          <Route path='/show-book/:id' element={<ShowBookDetails />} />
        </Routes>
      </div>
    </Router>
  );
};

export default App;
```

Here, all of the routes are defined. The component that corresponds to a given path definition will be displayed. These files and components have not yet been developed; the path setting has only been finished.

## Update the CSS File

Open the App.css file in the src folder (mern-demo/src/), and then replace the code with the following:

```
.App {
  text-align: center;
}

.App-logo {
  animation: App-logo-spin infinite 20s linear;
  height: 40vmin;
  pointer-events: none;
}

.App-header {
  background-color: #282c34;
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  font-size: calc(10px + 2vmin);
  color: white;
}

.App-link {
  color: #61dafb;
}

@keyframes App-logo-spin {
  from {
    transform: rotate(0deg);
  }
  to {
    transform: rotate(360deg);
  }
}

.CreateBook {
  background-color: #2c3e50;
  min-height: 100vh;
  color: white;
}

.ShowBookDetails {
  background-color: #2c3e50;
  min-height: 100vh;
  color: white;
}

.UpdateBookInfo {
  background-color: #2c3e50;
  min-height: 100vh;
  color: white;
}

.ShowBookList {
  background-color: #2c3e50;
  height: 100%;
  width: 100%;
  min-height: 100vh;
  min-width: 100px;
  color: white;
}

/* BookList Styles */
.list {
  display: grid;
  margin: 20px 0 50px 0;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: 1fr;
  grid-gap: 2em;
}

.card-container {
  width: 250px;
  border: 1px solid rgba(0,0,.125);
  margin: 0 auto;
  border-radius: 5px;
  overflow: hidden;
}

.desc {
  height: 130px;
  padding: 10px;
}

.desc h2 {
  font-size: 1em;
  font-weight: 400;
}

.desc h3, p {
  font-weight: 300;
}

.desc h3 {
  color: #6c757d;
  font-size: 1em;
  padding: 10px 0 10px 0;
}
```

### Add Feature Components

Create the following five files in the src/components folder (mern-demo/src/components/):

CreateBook.js \sShowBookList.js \sBookCard.js \sShowBookDetails.js \sUpdateBookInfo.js
These five files will be used later on in our work.

```
// CreateBook.js
import React, { useState } from 'react';
import { Link } from 'react-router-dom';
import axios from 'axios';

import { useNavigate } from 'react-router-dom';

const CreateBook = (props) => {
  // Define the state with useState hook
  const navigate = useNavigate();
  const [book, setBook] = useState({
    title: '',
    isbn: '',
    author: '',
    description: '',
    published_date: '',
    publisher: '',
  });

  const onChange = (e) => {
    setBook({ ...book, [e.target.name]: e.target.value });
  };

  const onSubmit = (e) => {
    e.preventDefault();

    axios
      .post('http://localhost:8082/api/books', book)
      .then((res) => {
        setBook({
          title: '',
          isbn: '',
          author: '',
          description: '',
          published_date: '',
          publisher: '',
        });

        // Push to /
        navigate('/');
      })
      .catch((err) => {
        console.log('Error in CreateBook!');
      });
  };

  return (
    <div className='CreateBook'>
      <div className='container'>
        <div className='row'>
          <div className='col-md-8 m-auto'>
            <br />
            <Link to='/' className='btn btn-outline-warning float-left'>
              Show BooK List
            </Link>
          </div>
          <div className='col-md-8 m-auto'>
            <h1 className='display-4 text-center'>Add Book</h1>
            <p className='lead text-center'>Create new book</p>

            <form noValidate onSubmit={onSubmit}>
              <div className='form-group'>
                <input
                  type='text'
                  placeholder='Title of the Book'
                  name='title'
                  className='form-control'
                  value={book.title}
                  onChange={onChange}
                />
              </div>
              <br />

              <div className='form-group'>
                <input
                  type='text'
                  placeholder='ISBN'
                  name='isbn'
                  className='form-control'
                  value={book.isbn}
                  onChange={onChange}
                />
              </div>

              <div className='form-group'>
                <input
                  type='text'
                  placeholder='Author'
                  name='author'
                  className='form-control'
                  value={book.author}
                  onChange={onChange}
                />
              </div>

              <div className='form-group'>
                <input
                  type='text'
                  placeholder='Describe this book'
                  name='description'
                  className='form-control'
                  value={book.description}
                  onChange={onChange}
                />
              </div>

              <div className='form-group'>
                <input
                  type='date'
                  placeholder='published_date'
                  name='published_date'
                  className='form-control'
                  value={book.published_date}
                  onChange={onChange}
                />
              </div>
              <div className='form-group'>
                <input
                  type='text'
                  placeholder='Publisher of this Book'
                  name='publisher'
                  className='form-control'
                  value={book.publisher}
                  onChange={onChange}
                />
              </div>

              <input
                type='submit'
                className='btn btn-outline-warning btn-block mt-4'
              />
            </form>
          </div>
        </div>
      </div>
    </div>
  );
};

export default CreateBook;
```

The ShowBookList.js component will be responsible for showing all the books we already have stored in our database.

```
// ShowBookList.js
import React, { useState, useEffect } from 'react';
import '../App.css';
import axios from 'axios';
import { Link } from 'react-router-dom';
import BookCard from './BookCard';

function ShowBookList() {
  const [books, setBooks] = useState([]);

  useEffect(() => {
    axios
      .get('http://localhost:8082/api/books')
      .then((res) => {
        setBooks(res.data);
      })
      .catch((err) => {
        console.log('Error from ShowBookList');
      });
  }, []);

  const bookList =
    books.length === 0
      ? 'there is no book record!'
      : books.map((book, k) => <BookCard book={book} key={k} />);

  return (
    <div className='ShowBookList'>
      <div className='container'>
        <div className='row'>
          <div className='col-md-12'>
            <br />
            <h2 className='display-4 text-center'>Books List</h2>
          </div>

          <div className='col-md-11'>
            <Link
              to='/create-book'
              className='btn btn-outline-warning float-right'
            >
              + Add New Book
            </Link>
            <br />
            <br />
            <hr />
          </div>
        </div>

        <div className='list'>{bookList}</div>
      </div>
    </div>
  );
}

export default ShowBookList;
```

BookCard.js will take a book’s info from ShowBookList.js and makes a card for each book.

```
// BookCard.js
import React from 'react';
import { Link } from 'react-router-dom';
import '../App.css';

const BookCard = (props) => {
  const book = props.book;

  return (
    <div className='card-container'>
      <img
        src='https://images.unsplash.com/photo-1495446815901-a7297e633e8d'
        alt='Books'
        height={200}
      />
      <div className='desc'>
        <h2>
          <Link to={`/show-book/${book._id}`}>{book.title}</Link>
        </h2>
        <h3>{book.author}</h3>
        <p>{book.description}</p>
      </div>
    </div>
  );
};

export default BookCard;
```

ShowBookDetails.js will show the details of a book.

```
// ShowBookDetails.js
import React, { useState, useEffect } from 'react';
import { Link, useParams, useNavigate } from 'react-router-dom';
import '../App.css';
import axios from 'axios';

function ShowBookDetails(props) {
  const [book, setBook] = useState({});

  const { id } = useParams();
  const navigate = useNavigate();

  useEffect(() => {
    axios
      .get(`http://localhost:8082/api/books/${id}`)
      .then((res) => {
        setBook(res.data);
      })
      .catch((err) => {
        console.log('Error from ShowBookDetails');
      });
  }, [id]);

  const onDeleteClick = (id) => {
    axios
      .delete(`http://localhost:8082/api/books/${id}`)
      .then((res) => {
        navigate('/');
      })
      .catch((err) => {
        console.log('Error form ShowBookDetails_deleteClick');
      });
  };

  const BookItem = (
    <div>
      <table className='table table-hover table-dark'>
        <tbody>
          <tr>
            <th scope='row'>1</th>
            <td>Title</td>
            <td>{book.title}</td>
          </tr>
          <tr>
            <th scope='row'>2</th>
            <td>Author</td>
            <td>{book.author}</td>
          </tr>
          <tr>
            <th scope='row'>3</th>
            <td>ISBN</td>
            <td>{book.isbn}</td>
          </tr>
          <tr>
            <th scope='row'>4</th>
            <td>Publisher</td>
            <td>{book.publisher}</td>
          </tr>
          <tr>
            <th scope='row'>5</th>
            <td>Published Date</td>
            <td>{book.published_date}</td>
          </tr>
          <tr>
            <th scope='row'>6</th>
            <td>Description</td>
            <td>{book.description}</td>
          </tr>
        </tbody>
      </table>
    </div>
  );

  return (
    <div className='ShowBookDetails'>
      <div className='container'>
        <div className='row'>
          <div className='col-md-10 m-auto'>
            <br /> <br />
            <Link to='/' className='btn btn-outline-warning float-left'>
              Show Book List
            </Link>
          </div>
          <br />
          <div className='col-md-8 m-auto'>
            <h1 className='display-4 text-center'>Book's Record</h1>
            <p className='lead text-center'>View Book's Info</p>
            <hr /> <br />
          </div>
          <div className='col-md-10 m-auto'>{BookItem}</div>
          <div className='col-md-6 m-auto'>
            <button
              type='button'
              className='btn btn-outline-danger btn-lg btn-block'
              onClick={() => {
                onDeleteClick(book._id);
              }}
            >
              Delete Book
            </button>
          </div>
          <div className='col-md-6 m-auto'>
            <Link
              to={`/edit-book/${book._id}`}
              className='btn btn-outline-info btn-lg btn-block'
            >
              Edit Book
            </Link>
          </div>
        </div>
      </div>
    </div>
  );
}

export default ShowBookDetails;
```

UpdateBookInfo.js will update the info of a book.

```
// UpdateBookInfo.js
import React, { useState, useEffect } from 'react';
import { Link, useParams, useNavigate } from 'react-router-dom';
import axios from 'axios';
import '../App.css';

function UpdateBookInfo(props) {
  const [book, setBook] = useState({
    title: '',
    isbn: '',
    author: '',
    description: '',
    published_date: '',
    publisher: '',
  });

  const { id } = useParams();
  const navigate = useNavigate();

  useEffect(() => {
    axios
      .get(`http://localhost:8082/api/books/${id}`)
      .then((res) => {
        setBook({
          title: res.data.title,
          isbn: res.data.isbn,
          author: res.data.author,
          description: res.data.description,
          published_date: res.data.published_date,
          publisher: res.data.publisher,
        });
      })
      .catch((err) => {
        console.log('Error from UpdateBookInfo');
      });
  }, [id]);

  const onChange = (e) => {
    setBook({ ...book, [e.target.name]: e.target.value });
  };

  const onSubmit = (e) => {
    e.preventDefault();

    const data = {
      title: book.title,
      isbn: book.isbn,
      author: book.author,
      description: book.description,
      published_date: book.published_date,
      publisher: book.publisher,
    };

    axios
      .put(`http://localhost:8082/api/books/${id}`, data)
      .then((res) => {
        navigate(`/show-book/${id}`);
      })
      .catch((err) => {
        console.log('Error in UpdateBookInfo!');
      });
  };

  return (
    <div className='UpdateBookInfo'>
      <div className='container'>
        <div className='row'>
          <div className='col-md-8 m-auto'>
            <br />
            <Link to='/' className='btn btn-outline-warning float-left'>
              Show BooK List
            </Link>
          </div>
          <div className='col-md-8 m-auto'>
            <h1 className='display-4 text-center'>Edit Book</h1>
            <p className='lead text-center'>Update Book's Info</p>
          </div>
        </div>

        <div className='col-md-8 m-auto'>
          <form noValidate onSubmit={onSubmit}>
            <div className='form-group'>
              <label htmlFor='title'>Title</label>
              <input
                type='text'
                placeholder='Title of the Book'
                name='title'
                className='form-control'
                value={book.title}
                onChange={onChange}
              />
            </div>
            <br />

            <div className='form-group'>
              <label htmlFor='isbn'>ISBN</label>
              <input
                type='text'
                placeholder='ISBN'
                name='isbn'
                className='form-control'
                value={book.isbn}
                onChange={onChange}
              />
            </div>
            <br />

            <div className='form-group'>
              <label htmlFor='author'>Author</label>
              <input
                type='text'
                placeholder='Author'
                name='author'
                className='form-control'
                value={book.author}
                onChange={onChange}
              />
            </div>
            <br />

            <div className='form-group'>
              <label htmlFor='description'>Description</label>
              <textarea
                type='text'
                placeholder='Description of the Book'
                name='description'
                className='form-control'
                value={book.description}
                onChange={onChange}
              />
            </div>
            <br />

            <div className='form-group'>
              <label htmlFor='published_date'>Published Date</label>
              <input
                type='text'
                placeholder='Published Date'
                name='published_date'
                className='form-control'
                value={book.published_date}
                onChange={onChange}
              />
            </div>
            <br />

            <div className='form-group'>
              <label htmlFor='publisher'>Publisher</label>
              <input
                type='text'
                placeholder='Publisher of the Book'
                name='publisher'
                className='form-control'
                value={book.publisher}
                onChange={onChange}
              />
            </div>
            <br />

            <button
              type='submit'
              className='btn btn-outline-info btn-lg btn-block'
            >
              Update Book
            </button>
          </form>
        </div>
      </div>
    </div>
  );
}

export default UpdateBookInfo;
```

## Connect and run the frontend to the backend

We just finished putting all of our parts together! We now need to make a small adjustment to our server-side backend project.

A failure occurs if the frontend part attempts to reach our backend API:

```"Access to XMLHttpRequest at 'http://localhost:8082/api/books' from origin 'http://localhost:3000' has been blocked by CORS policy: Response to preflight request doesn't pass access control check: No 'Access-Control-Allow-Origin' header is present on the requested resource."

```

We must install cors on our backend server side app to resolve issue. Run $ npm install cors from the project folder.

Add the following code to app.js, the backend's entry point:

```
// app.js

const express = require('express');
const connectDB = require('./config/db');
const cors = require('cors');

// routes
const books = require('./routes/api/books');

const app = express();

// Connect Database
connectDB();

// cors
app.use(cors({ origin: true, credentials: true }));

// Init Middleware
app.use(express.json({ extended: false }));

app.get('/', (req, res) => res.send('Hello world!'));

// use Routes
app.use('/api/books', books);

const port = process.env.PORT || 8082;

app.listen(port, () => console.log(`Server running on port ${port}`));
```

It's crucial that you include the following line: `app.use(express.json(extended: false));` Express is able to read data supplied via a POST or PUT request thanks to the express.json method. It is employed to identify incoming items as JSON objects.

## Run the app (frontend and backend)

Now that we've finished our backend and frontend projects, we can run them both at the same time. Open two terminals and run the following commands:

```
$ cd backend
$ npm run app
```

```
$ cd frontend
$ npm start
```

## Test your MERN stack app in the browser

Let's do a quick check in the browser. Open your browser to http://localhost:3000. Now, you have the ability to add, remove, display, and edit books. The following routes need to function appropriately:

Add a fresh volume:

http://localhost:3000/create-book

![mern-stack-add-book](/static/images/posts/mern/mern-stack-add-book.webp)

Show the list of books:

http://localhost:3000/

![mern-stack-show-book-list](/static/images/posts/mern/mern-stack-book-list.webp)

Show any book’s info:

http://localhost:3000/show-book/:id

![mern-stack-show-book-info](/static/images/posts/mern/mern-stack-book-info.webp)

Update a book’s info:

http://localhost:3000/edit-book/:id

![mern-stack-update-book-info](/static/images/posts/mern/mern-stack-book-edit.webp)

## Conclusion

Congratulations! You've successfully built a MERN stack app. You've learned how to create a full-stack application using MongoDB, Express, React, and Node.js. You've also learned how to use the MERN stack to build a CRUD application.
