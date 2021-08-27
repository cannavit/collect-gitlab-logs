# Gitlab pipeline logs collection for BigData analysis
[![NodeJS](https://img.shields.io/badge/-NodeJs-3CA80B?style=flat-square&logo=nodejs&logoColor=white&link=https://nodejs.org/en/)](https://nodejs.org/en/)
[![GitHub](https://img.shields.io/badge/-github-black?style=flat-square&labelColor=black&logo=github&logoColor=white&link)](https://github.com/cannavit/zipi-smkTest)

The analysis of large volumes of information can help determine where the most errors are found for a given project or thousands of projects. This information can be used to generate adequate tests and to mitigate the errors produced in the Pipelines.

The Gitlab-CI tool is being widely used for the ease they offer in the integration of automated deployment of projects. It offers the possibility to automate every step from the push of a new commit to the secure deployment on servers.

In this post I show how to perform a data collection using the gitlab and nodejs apis. This data can be used to create different types of big data analysis


## Content Index

- [Create Environment NodeJs](#create-environment-nodejs)
- [Run MongoDB from docker-compose](#run-mongodb-from-docker-compose)
- [Create Schema with logs structure](#run-mongodb-from-docker-compose)
- [Create function for collect logs from pipeline](#create-function-for-collect-logs-from-pipeline)


## Create Environment Nodejs. 

NodeJS is an excellent tool for collecting pipe logs because it has excellent performance. In this section we will install the nodejs packages.

### 1) Create the npm project:

```
    npm init
```

### 2) Install dependencies

```
    npm install dotenv mongoose express

```


### 3) Create the project structure 

 For this example we propose use one simple structure, composed by src/service and access file index.js

```
    |- src
        |- services
    |- index.js
    |- .env
```


### 4) Create file index.js


```
// Import dependencies
const express = require("express");
const mongoose = require("mongoose");
require("dotenv").config();

// Environment variables
let MONGO_URI = process.env.MONGO_URI || "mongodb://localhost:27017/logsGitlab";

// Connect with mongoDB

mongoose.connect(MONGO_URI, {
  useNewUrlParser: "true",
});

mongoose.connection.on("error", (err) => {
  console.log("err", err);
});

mongoose.connection.on("connected", (err, res) => {
  console.log("🟢 Mongoose is connected");
});

```