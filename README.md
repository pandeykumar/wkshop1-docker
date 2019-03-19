
# Docker

## Why is it getting so popular ?

### Good background in the presentations below

[Introduction to Docker](https://www.slideshare.net/Docker/introduction-to-docker-2017)

[Microsoft - Introduction to Containers and Docker](https://docs.microsoft.com/en-us/dotnet/standard/microservices-architecture/container-docker-introduction/)

### Some important takeway from these presentations :

>> Lean and thin in comparision to Virtuals Machines
![Containers vs VMs](https://drive.google.com/uc?id=1pBJ0L11_hTcn3De4RScfG8rlnj4r2r0H)

>> Streamlines development across different OS and tech stack
![Development lifecycle](https://drive.google.com/uc?id=1Hw3hLhDHqkvYVn4FdSnG9aOzieKlFgK9)

>> Supports full Continuous Integration /Continuous Deployment lifecycle
![Testing and deployment lifecycle](https://drive.google.com/uc?id=1qcucrz-V8Z5kcmHbeUCb1PYhC1lsQojy)




## Installation

### For window: Docker Desktop for Windows
> [Windows install](https://hub.docker.com/editions/community/docker-ce-desktop-windows)
>> ***Requires Microsoft Windows 10 Professional or Enterprise 64-bit***

> [Other windows versions](https://docs.docker.com/toolbox/overview/)

### For Mac: Docker Desktop for Mac
> [Mac Install](https://hub.docker.com/editions/community/docker-ce-desktop-mac)

## Obligatory hello world !!
  Lets run a docker hello world to make sure docker is installed properly on your machine.
> ##### Check if docker installed properly
>>> In command prompt type ```c:> docker images```

If everything is good then you should see something like this if this is your first install of docker as there should be no images.

![docker images](https://drive.google.com/uc?id=1WFNoi7Owk_mLpS5fhmd4rFUN0SZfEc7v)

Now lets run a docker container that just prints hello world.

```c:>docker run hello-world```

You should see something like this

![docker-hello-world-run](https://drive.google.com/uc?id=1Hht5ynW62pDqbJJQ8NBKeFZotXT9RJaN)

>>> If you see some error in connection restart your docker and try again.
Lets discuss what happened here. Docker daemon tries to look for the hello-world images in local repository. Doesn't find it and goes to docker hub repo to download. The output also explains this.

***If you reached this part then you have successfully installed docker***

## Lets build our own image.

### Next We will create a nodejs app, create a docker image of it and run it.

1. Download nodejs from https://nodejs.org/en/

2. Select all the defaults mentioned by the installer.

 2.1 Make sure node installed properly by running the node command
 ```
 c:\ node version
 ```
 Should see something like this :
 ![node version](https://drive.google.com/uc?id=160iwOvhJK7Kkx3H2IeUA1R0s5tMoOuJq)

3. Make directoty called *nodejs-hello-world* and cd to it.

4. Initialize your project
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

5. Install ***Express*** in *nodejs-hello-world* directory

  While in *nodejs-hello-world* run
  ```
  npm install Express
  ```

![install express](https://drive.google.com/uc?id=14OLp-jsn0CDKGxdc05Jl9gqno2LX6o-m)

Notice that it created a *node_modules* folder and installed all the necessary packages

![node moduels](https://drive.google.com/uc?id=1ZfGlmm22Y6G6ClbdG8syKq07_a5eNlxp)  

6. Start a text editor of your choice and create a file name *app.js*

  Add this code to it that will listen for http request at port 3000 and will display ***Hello World*** when a get request is called.

  ```
var express = require('express');
var app = express();
app.get('/', function (req, res) {
  res.send('Hello World!');
});
app.listen(3000, function () {
  console.log('Example app listening on port 3000!');
});
  ```
7. Run the app
  ```
node app.js
  ```
8. Test the app by going to your browser at ***http://localhost:3000/***
You should see hello world being printed

### Great!! Now lets dockerize it
