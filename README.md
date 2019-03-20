
# Docker

## Why is it getting so popular ?

### Good background in the presentations below

[Introduction to Docker](https://www.slideshare.net/Docker/introduction-to-docker-2017)

[Microsoft - Introduction to Containers and Docker](https://docs.microsoft.com/en-us/dotnet/standard/microservices-architecture/container-docker-introduction/)

### Some important takeway from these presentations :

Lean and thin in comparision to Virtuals Machines

![Containers vs VMs](https://drive.google.com/uc?id=1pBJ0L11_hTcn3De4RScfG8rlnj4r2r0H)

Streamlines development across different OS and tech stack

![Development lifecycle](https://drive.google.com/uc?id=1Hw3hLhDHqkvYVn4FdSnG9aOzieKlFgK9)

Supports full Continuous Integration /Continuous Deployment lifecycle

![Testing and deployment lifecycle](https://drive.google.com/uc?id=1qcucrz-V8Z5kcmHbeUCb1PYhC1lsQojy)

## Installation

### For window: Docker Desktop for Windows
[Windows install](https://hub.docker.com/editions/community/docker-ce-desktop-windows)

***Requires Microsoft Windows 10 Professional or Enterprise 64-bit***

[Other windows versions](https://docs.docker.com/toolbox/overview/)

### For Mac: Docker Desktop for Mac
[Mac Install](https://hub.docker.com/editions/community/docker-ce-desktop-mac)

## Obligatory hello world !!
  Lets run a docker hello world to make sure docker is installed properly on your machine.

##### Check if docker is installed properly
In command prompt type ```c:> docker images```

If everything is good then you should see something like this.

![docker images](https://drive.google.com/uc?id=1WFNoi7Owk_mLpS5fhmd4rFUN0SZfEc7v)

Now lets run a docker container that just prints hello world.

```c:>docker run hello-world```

You should see something like this

![docker-hello-world-run](https://drive.google.com/uc?id=1Hht5ynW62pDqbJJQ8NBKeFZotXT9RJaN)

***If you see some error in connection restart your docker and try again***

Lets discuss what happened here. Docker daemon tries to look for the hello-world images in local repository. Doesn't find it and goes to docker hub repo to download. The output also explains this.

***If you reached this part then you have successfully installed docker***

## Now we will dockerize  nodejs 'hello world' app and run it locally


### Lets install nodejs and npm package manager if you don't already have it
1. Download nodejs from https://nodejs.org/en/

2. Select all the defaults mentioned by the installer.

 2.1 Make sure node installed properly by running the node command
 ```
 c:\ node --version
 ```
 Should see something like this :
 ![node version](https://drive.google.com/uc?id=160iwOvhJK7Kkx3H2IeUA1R0s5tMoOuJq)

### Setup the nodejs app in this repository

1. cd to *nodejs-hello-world* and run npm install command to download all the related node packages as specified in the package.json

```
cd nodejs-hello-world
npm install

```
Notice that it created a *node_modules* folder and installed all the necessary packages

2. Run the web app using node command
```node app.sj```

You should see output like this -
```Example app listening on port 3000!```

### Great!! Now lets dockerize the nodejs app.

Dockerfile defines what goes inside your image.
Read more here [Docker file](https://docs.docker.com/get-started/part2/)

1. Look at the content of the Dockerfile
```
FROM node:11-alpine
WORKDIR /nodejs-hello-world
COPY . /nodejs-hello-world
CMD ["node", "app.js"]
```
Lets break it down

```FROM node:11-alpine```

What this saying is that use an official nodejs 11 as parent images

docker daemon first looks at local repo else will fetch this parent image from dockerhub.

```WORKDIR /nodejs-hello-world```

Set the working directory in the container to /nodejs-hello-world

```COPY . /nodejs-hello-world```

Copy the content of the current directory to /nodejs-hello-world folder in the container

```CMD ["node", "app.js"]```

Run ***node apps.js*** when the container launches

2. Build the docker image of the nodejs apps

```docker build  -t my-hello-world .```

Note the . in the command. -t will tag it with my-hello-world.

You should see activity like these

![docker build](https://drive.google.com/uc?id=1TqQL50tJ1SxjtylQqHE73LxNb_n8mZ0g)

This should create an image of your application and stored on local repository.

3. Verify that the image is created and stored in the local repository

```docker images```

Should see something like this

![docekr images](https://drive.google.com/uc?id=14kG_e-WcbbYvKVTizWTkt2v-yXyjPE5w)

4. Run the image to create a container that will run the nodejs app

```docker run -d  -p 3000:3000 my-hello-world```

-d runs it in detached mode so that you can use command prompt on host machine
-p will map the TCP port on the container to the port in the host.
That way when you type http://localhost:3000/, the request will actually go to port 300o on the conatiner where the nodejs app is listening.

5. On your browser go to http://localhost:3000/ and you should see 'Hello World' printed on the page.

## (Extra Bonus !!) Lets build a new nodejs webapp from scratch

1. Make directoty called *nodejs-hello-world* and cd to it.

2. Initialize your project
```
c:\>npm init
```
Select all defaults except for this -

  ```
  entry point: (index.js)
  ```

  change this to:

  ```
  app.js
  ```
This creates a package.json file  with references for the project.

![npm init](https://drive.google.com/uc?id=1tIB2MPeHPmcLEIQnS7bu_rzZc5x7k3Uh)

4. Install ***Express*** in *nodejs-hello-world* directory

  While in *nodejs-hello-world* run
  ```
  npm install Express
  ```

![install express](https://drive.google.com/uc?id=14OLp-jsn0CDKGxdc05Jl9gqno2LX6o-m)

Notice that it created a *node_modules* folder and installed all the necessary packages

![node moduels](https://drive.google.com/uc?id=1ZfGlmm22Y6G6ClbdG8syKq07_a5eNlxp)  

5. Start a text editor of your choice and create a file name *app.js*

  Add this code to it that will listen for http request at port 3000 and will display ***Hello World*** when a get request is called.

  ```
var express = require('express');
var app = express();
app.get('/', function (req, res) {
  res.send('Hello My World!');
});
app.listen(3000, function () {
  console.log('Example app listening on port 3000!');
});
  ```
6. Run the app
  ```
node app.js
  ```
7. Test the app by going to your browser at ***http://localhost:3000/***
You should see 'Hello My World!' being printed on the web page
