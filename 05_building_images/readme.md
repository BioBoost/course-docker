# Chapter 05 - Building Images

When building images to create containers from, one could start from scratch; compiling, building, configuring and installing all the dependencies by our self. This would be feasible but tedious task. A better idea is to start *from* an already existing image that provides the basis and build on top of that.

Let's say we wish to create a container that hosts a small web-application, build in NodeJS that uses the express framework.

## A NodeJS app

Start by creating a small hello world application on NodeJS. Do this by creating a project directory on your development host called `hello-docker-from-node`. Best to put this beauty in a git repo with a `README.md` file added to it.

Issue an `npm init` inside the project directory to setup the `package.json` file:

```json
{
  "name": "hello-docker-from-node",
  "version": "1.0.0",
  "description": "Hello World App in NodeJS to demonstrate docker",
  "main": "app.js",
  "scripts": {
    "start": "node app.js",
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [
    "hello",
    "world",
    "docker"
  ],
  "author": "Nico De Witte <nico.dewitte@vives.be>",
  "license": "ISC",
  "repository": {
    "type": "git",
    "url": "git+https://github.com/BioBoost/hello-docker-from-node.git"
  },
  "bugs": {
    "url": "https://github.com/BioBoost/hello-docker-from-node/issues"
  },
  "homepage": "https://github.com/BioBoost/hello-docker-from-node#readme",
  "dependencies": {
    "express": "^4.16.4"
  }
}

```

Next install the express framework by issueing `npm install express --save`.

Add a small hello world app to the application file:

```javascript
const express = require('express');
const app = express();
const port = 3000;

app.get('/', (req, res) => {
  res.send('Hello World!');
});

app.listen(port, () => console.log(`Hello World app listening on port ${port}!`));
```

Test it by running `npm start`. Also surf to `http://localhost:3000` to test it.