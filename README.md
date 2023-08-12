# Individual Assignment Docker And Node.js <img src="https://img.shields.io/badge/-Node.js-05122A?style=flat&logo=node.js" width="90" alt="node.js logo"> <img src="https://img.shields.io/badge/-Docker-05122A?style=flat&logo=docker" width="90" alt="docker logo">


<p align="center">
  <img src="https://i.morioh.com/2020/01/30/682d7390521c.jpg" width="60%" alt="logo">
</p>

## Getting started

These instructions will get you through simply simulation to create the application backend system
with Node.js and docker simulation container.

### Prerequisites

- Make sure that you have Docker to installed in your device
  - Windows or macOS:
    [Install Docker Desktop](https://www.docker.com/get-started)
  - Linux: [Install Docker](https://www.docker.com/get-started)
- Download or copy this [data](https://gist.github.com/berdoezt/e51718982926f0caa3fcd8ed45111430) and add all with name app.js in your folder.
  
### Running a sample

After you install docker, run the file that you installed until the file that is installed is complete and check with:

console
```
docker --version
```

so you can see this if your installed is complete 

![checkversi.jpg](https://i.postimg.cc/XN5Ln4Wf/checkversi.jpg)

First, create a new directory where all the files would live. In this directory create a package.json file that describes your app and its dependencies:

package.json 
```
{
  "name": "week-6-haikalshahab93",
  "version": "1.0.0",
  "description": "<p align=\"center\">\r   <img src=\"https://i.morioh.com/2020/01/30/682d7390521c.jpg\" width=\"60%\" alt=\"logo\">\r </p>",
  "main": "app.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "start": "node app.js"
  },
  "author": "",
  "license": "ISC"
}


```

After this lets go to your folder application and create the dockerfile 
so after this your application is have like this

Then, create a app.js file that defines a web app for server:

app.js 
```
const http = require('http');

const hostname = '0.0.0.0';
const port = 3001;

const server = http.createServer((req, res) => {
  res.statusCode = 200;
  res.setHeader('Content-Type', 'text/plain');
  res.end('Hello World');
});

server.listen(port, hostname, () => {
  console.log(`Server running at http://${hostname}:${port}/`);
});
```
In the next steps, we'll look at how you can run this app inside a Docker container using the official Docker image. First, you'll need to build a Docker image of your app.

## Create file Dockerfile
    
    1. Create an empty file called Dockerfile

The first thing we need to do is define from what image we want to build from. Here we will use the latest version node:alpine  available from the Docker Hub:

     FROM node:alpine

Next we create a directory to hold the application code inside the image, this will be the working directory for your application:

     # Create app directory
        WORKDIR app

This image comes with Node.js and NPM already installed so the next thing we need to do is to install your app dependencies using the npm binary. Please note that if you are using npm version 4 or earlier a package-lock.json file will not be generated.

    # Install app dependencies
    # A wildcard is used to ensure both package.json AND package-lock.json are copied
    # where available (npm@5+)
    
    COPY package*.json ./

    RUN npm install
    
    # If you are building your code for production
    # RUN npm ci --omit=dev

To bundle your app's source code inside the Docker image, use the COPY instruction:

    # Bundle app source
    COPY . .

Your app binds to port 3001 so you'll use the EXPOSE instruction to have it mapped by the docker daemon:   

    EXPOSE 3001

define the command to run your app using CMD which defines your runtime. Here we will use node app.js to start your server:

    CMD [|"node","app.js"]


Your Dockerfile should now look like this:

    FROM node:alpine

    # Create app directory
    WORKDIR /app

    # Install app dependencies
    # A wildcard is used to ensure both package.json AND package-lock.json are copied
    # where available (npm@5+)

    COPY package*.json ./

    RUN npm install

    # If you are building your code for production
    # RUN npm ci --omit=dev

    # Bundle app source
    COPY . .

    EXPOSE 3001

    CMD [|"node","app.js"]

 After this include to container docker images with comment :

    docker build . -t yourfilename

So If your action is success you can see this for your your terminal

<p>
<img src="assets/createcontainer.png" alt="image-container" width="50%">
</p>

Then after this you can check your build with:
    
    docker images

If you build is successfully so you can see your build like this

![image](assets/dockerimagehascreated.png)

After this lets run your docker image with
    
    docker run -p yourlocalserver:dockerserver nameyourrepositorydocker

    # for example:

    docker run -p 3000:3001 dockertest2

So after this you can see this image like this:

![Server-run](./assets/serverrun.png)

So if you run the localserver so you can see what you write
like this:

![localhost-run-image](./assets/localhostrun.png)

So if you want to stop the server so you can run this:

    docker stop CONTAINER_ID

    # for example

    docker stop 81bfafbbbd2e

So if want know your docker server image is run or stop,you can
use this comment

    docker ps 

### So if you want know all of the process or you have the problem you can comming this:

[https://docs.docker.com/get-started/overview/](https://docs.docker.com/get-started/overview/)


### The technology use to create the application

<a href="https://nodejs.org/it/docs">
<img src="https://img.shields.io/badge/-Node.js-05122A?style=flat&logo=node.js" width="90" alt="node.js logo">
</a>
<a href="https://docs.docker.com/">
 <img src="https://img.shields.io/badge/-Docker-05122A?style=flat&logo=docker" width="90" alt="docker logo">
</a>









    



