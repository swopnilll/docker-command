### Node js App Web Application in Docker

### Steps

1. Create a node js web app
2. Create a docker file
3. Build image from docker file 
4. Run image as an container 
5. Connect to web app from browser

### Step 1: Creating node js web app

#### 1.a Create a package.json file 

```
{
   "dependencies": {
   "express": "*"
   },
   
   "script":{
   "start": "node index.js"
   }
}
```
#### 1.b Create index.js file

```
const express = require("express");

const app = express();

app.get("/", (req, res) => {
  res.send("Hello World");
});

app.listen(3000, () => {
  console.log("Listening on port 3000");
});
```
### Step 2: Create dockerfile

```
# Specify a base image
FROM node:14-alpine

WORKDIR /usr/app

COPY ./package.json ./

# Install some dependencies
RUN npm install

COPY ./ ./

# Default command
CMD [ "npm", "start" ]
```

### Step 3: Build image from docker file 

```docker build .```
```docker build -t tag/name .```
```docker build -t swop/express .```

### Step 4: Run Image as an container

``` 
docker run -p system_port:container_port <container_tag>
```

```
docker run -p 3000:3000 swop/express
```


