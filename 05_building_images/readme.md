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

## Finding a Base Image

Before starting with building containers, we first need to decide from which image to start from. The closer it matches our dependencies, the less work we'll have.

Many image are available that provide support for Node inside Docker. Many of them could be used. To make it easier to determine an active and supported image, Docker Hub will provide some extra information such as 'stars' and 'pulls'. People can 'star' images that they like. This will give an indication of the popularity. 'pulls' shows the amount of times that the images has been pulled, either to create an new image, or to deploy a container that is based on that image.

Another parameter that could help deciding what image to use is the developer. The developer is the first part before the `/` in the full container name. For example `nodered/node-red-docker` means that the image with name `node-red-docker` is made by the `nodered` developer or team.

Some images don't have a developer name and `/` sign. These images are 'official' images. They are created and maintained by the people of docker. They provide many of the popular solutions. Many times depending on one of these images is preferable.

The best choice in our case would be the official `Node` image. Luckily node is so popular, that it also supported for both `arm32v7` and `arm64v8`. If that was not the case we had to start from an image such as alpine or raspbian and install the dependencies ourselves, or use an unofficial image.

The node image can be found at [https://hub.docker.com/_/node](https://hub.docker.com/_/node). Different versions are available but since we are running this on a Raspberry Pi, its best to go lightweight and pick the alpine based image. A good version (tag) would be `11.11.0-alpine`.

> **INFO** - **TestDrive the Base Image**
>
> You can always test-drive the base image by issueing the command `docker run -it --rm node:11.11.0-alpine sh`, which would spawn a shell. You can check the node version using `node --version` or you can test a simple script. Starting a container with the command `docker run -it --rm node:11.11.0-alpine` would allow you to just enter javascript code.