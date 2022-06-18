# project-manage-app

## Table of Contents

## Project Management App

An application to manage clients and project data that can make CRUD functionality with simple web page.

- Built backend with expressjs and handled by using graphQL mutation.
- Used graphiql for checking graphql schema on the browser.
- Made cloud-based database by using mongodb atlas and controled with mongodb compass.  
- Build client side with React and apollo, graphql, react-router-dom, react-icons packages.

## Initialize application
- initialize project: ```npm init -y``` -> ```package.json``` created
- install dependencies: ```npm i express express-graphql graphql mongoose cors colors``` -> ```node_modules``` folder and ```package-lock.json``` file created.
- install dev mode dependencires: ```npm i -D nodemon dotenv```
- change ```package.json``` scripts setting.

```json
"scripts": {
        "start": "node server/index.js",
        "dev": "nodemon server/index.js"
    }
```
Now you can start server by using ```npm run dev``` command inside of working directory.

## GraphiQL

[GraphiQL](https://www.npmjs.com/package/graphiql) is the GraphQL integrated development environment (IDE). We can make query and check data with GraphiQL on the ```localhost:5000/graphql```.

<img width="450" alt="image" src="https://user-images.githubusercontent.com/39740066/173705575-ea712ccd-ea11-4a0b-944a-6535696004f3.png">
<img width="450" alt="image" src="https://user-images.githubusercontent.com/39740066/173706238-6238939f-7725-4423-b310-4f0499efbb3b.png">

## Initiate Mongodb - Mongodb atlas, Mongodb compass
### 1. Mongodb atlas

[Mongodb atlas](https://www.mongodb.com/cloud/atlas/lp/try2?utm_source=google&utm_campaign=gs_americas_canada_search_core_brand_atlas_desktop&utm_term=mongodb%20atlas&utm_medium=cpc_paid_search&utm_ad=e&utm_ad_campaign_id=12212624311&adgroup=115749704343&gclid=CjwKCAjw46CVBhB1EiwAgy6M4oIvFcJ5cjdYixiQOZl9QAf-ot3E0qVDwE8g9m5PAYi_qoTZL4yKvBoCdOwQAvD_BwE) is a cloud-based Mongodb service that don't need to install any program on the local machine.

Sign up with google acount and build a database. 

<img width="450" alt="image" src="https://user-images.githubusercontent.com/39740066/173707549-81ef9192-a24a-491f-94c6-154a829d3c27.png">

Select share version and create cluster.

<img width="450" alt="image" src="https://user-images.githubusercontent.com/39740066/173707693-417d35b7-98dd-48ce-867c-d1313e925f6d.png">

Add my local ip address and finish

<img width="450" alt="image" src="https://user-images.githubusercontent.com/39740066/173708325-5272284c-49aa-4728-9967-9871150844f4.png">

Create database with own name ```mgmt_db``` and ```clients```.

<img width="450" alt="image" src="https://user-images.githubusercontent.com/39740066/173708913-09631f48-902f-4e1a-babf-b55798ba0e77.png">

### 2. Mongodb compass

Download and install [Mongodb compass](https://www.mongodb.com/products/compass). 
On the mongodb atlas, choose overview menu and click ```connect```.

<img width="450" alt="image" src="https://user-images.githubusercontent.com/39740066/173714243-abaa5f33-180a-43a0-a4ab-1db2abd6dc3a.png">

Select connect to the compass and copy the connection string. And change ```<username>``` and ```<password>```. After that, you can see database connected with atlas on the compass.

<img width="450" alt="image" src="https://user-images.githubusercontent.com/39740066/173715042-bd998125-c900-4c67-987c-e0e8c852de3c.png">

To connect with application, select ```go back``` and make a choice ```connect your application```. Copy connection string inside of ```.env``` file as a ```MONGO_URI``` variable. (Change <username>, <password> and add ```mgmt_db``` after ```mongodb.net/``` )

<img width="450" alt="image" src="https://user-images.githubusercontent.com/39740066/173715510-f5195abf-ce3d-4078-b69d-4f5fb079f73b.png">

### 3. Connect to the database

By using ```mongoose``` module, you can connect MongoDB with application. Inside of ```config``` folder, ```db.js``` have a ```connectDB``` as a module.

```javascript
const mongoose = require('mongoose');

const connectDB = async () => {
  const conn = await mongoose.connect(process.env.MONGO_URI);

  console.log(`MongoDB Connected: ${conn.connection.host}`.cyan.underline.bold);
};

module.exports = connectDB;
```

If you want to anticipate message as specific color and underline, we can use ```colors``` module.
        
<img width="450" alt="image" src="https://user-images.githubusercontent.com/39740066/173841498-528a746b-a72e-4453-a86c-52ea993dc972.png">

### 4. Fetch MongoDB data

In order to fetch data from MongoDB after connected with, we need to make new schema for MongoDB again not for GraphQL. In this project, ```Client.js``` and ```Project.js``` file was made inside of ```models``` folder. And changed ```schema.js``` return values of each client and project.

### 5. CRUD client and project with GraphQL and MongoDB
       
For handling MongoDB database with GraphQL, ```mutation``` object type can be added inside of ```schema.js```. Name of object is ```Mutation``` and you can add client data by using GraphiQL like below.
        
<img width="450" alt="image" src="https://user-images.githubusercontent.com/39740066/173851950-e0af3177-4f97-4a69-ad00-297e51bfb986.png">

And you can find new client data was added successfully on the MongoDB client database with MongoDB compass. Object ID is automatically created by MongoDB.
        
<img width="450" alt="image" src="https://user-images.githubusercontent.com/39740066/173852820-c59d88cc-605b-4379-bcec-2bbad4f4cfbe.png">

In the same way, we can add ```deleteClient``` field to delete a client data with GraphiQL on the browser.
        
<img width="450" alt="image" src="https://user-images.githubusercontent.com/39740066/173854727-1176dbba-d678-499c-b4eb-ef7064f5ae9f.png">

```project``` database also can be added, deleted and updated by ustin ```mutation``` object type. This code is added into ```schema.js```.

## Build client side with React framework.

### 1. Create react application

We can initialize react app in the ```client``` folder with ```npx create-react-app client``` command. After that, some packages should be installed by ```npm i @apollo/client graphql react-router-dom react-icons``` command.

#### apollo/client
Apollo Client is a comprehensive state management library for JavaScript that enables you to manage both local and remote data with GraphQL. Use it to fetch, cache, and modify application data, all while automatically updating your UI. Apollo Client helps you structure code in an economical, predictable, and declarative way that's consistent with modern development practices. The core @apollo/client library provides built-in integration with React, and the larger Apollo community maintains integrations for other popular view layers.
        
- Whenever Apollo Client fetches query results from your server, it automatically caches those results locally. This makes later executions of that same query extremely fast.
- Apollo Client stores the results of your GraphQL queries in a local, normalized, in-memory cache. This enables Apollo Client to respond almost immediately to queries for already-cached data, without even sending a network request.

#### react-router-dom
The react-router-dom package contains bindings for using ```React Router``` in web applications.
        
React Router includes three main packages:
- ```react-router```, the core package for the router
- ```react-router-dom```, which contains the DOM bindings for React Router. In other words, the router components for websites
- ```react-router-native```, which contains the React Native bindings for React Router. In other words, the router components for an app development environment using React Native

React Router DOM enables you to implement dynamic routing in a web app. Unlike the traditional routing architecture in which the routing is handled in a configuration outside of a running app, React Router DOM facilitates component-based routing according to the needs of the app and platform.

#### react-icons
Include popular icons in your React projects easily with react-icons, which utilizes ES6 imports that allows you to include only the icons that your project is using.
        
## References
- https://www.youtube.com/watch?v=BcLNfwF04Kw
- https://www.apollographql.com/docs/react/
- https://blog.logrocket.com/react-router-dom-tutorial-examples/
- https://github.com/react-icons/react-icons
