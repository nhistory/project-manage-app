# project-manage-app


https://user-images.githubusercontent.com/39740066/176313841-a13de996-3b8e-411d-beab-620bca482eb0.mp4


## Table of Contents

- [Project Management App](#project-management-app)
- [Initialize application](#initialize-application)
- [GraphiQL](#graphiql)
- [Initiate Mongodb - Mongodb atlas, Mongodb compass](https://github.com/nhistory/project-manage-app/edit/master/README.md#initiate-mongodb---mongodb-atlas-mongodb-compass)
  * [1. Mongodb atlas](#1-mongodb-atlas)
  * [2. Mongodb compass](#2-mongodb-compass)
  * [3. Connect to the database](#3-connect-to-the-database)
  * [4. Fetch MongoDB data](#4-fetch-mongodb-data)
  * [5. CRUD client and project with GraphQL and MongoDB](#5-crud-client-and-project-with-graphql-and-mongodb)
- [Build client side with React framework.](#build-client-side-with-react-framework)
  * [1. Create react application](#1-create-react-application)
  * [2. Connect between GraphQL and React client](#2-connect-between-graphql-and-react-client)
  * [3. Fetch and display clients](#3-fetch-and-display-clients)
  * [4. Implement react-router-dom](#4-implement-react-router-dom)
- [Deploy with heroku](#deploy-with-heroku)
  * [1. Setup before deploy.](#1-setup-before-deploy)
  * [2. Deploy with heroku](#2-deploy-with-heroku)
- [References](#references)

## Project Management App

A MERN stack application to manage clients and project data that can make CRUD functionality with simple web page.

- Built backend with expressjs and handled by using graphQL mutation.
- Used graphiql for checking graphql schema on the browser.
- Made cloud-based database by using mongodb atlas and controled with mongodb compass.  
- Build client side with React and apollo, graphql, react-router-dom, react-icons packages.
- Deploy with PaaS service heroku application.
- Resource: [Git repo](https://github.com/nhistory/project-manage-app) | [Demo](https://mernappsh.herokuapp.com/)

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
        
### 2. Connect between GraphQL and React client
        
In order to use state management library Apollo Client, we need to import ```ApolloProvider```,```ApolloClient```,```InMemoryCache``` from ```@apollo/client```. And make new ApolloClient class with ```client``` variable.

- App.js
```javascript
import Header from './components/Header';
import { ApolloProvider, ApolloClient, InMemoryCache } from '@apollo/client';

const client = new ApolloClient({
  uri: 'http://localhost:5000/graphql', //backend graphql url
  cache: new InMemoryCache(),
});

function App() {
  return (
    <>
      <ApolloProvider client={client}>
        <Header />
        <div className="container">
          <h1>Hello World</h1>
        </div>
      </ApolloProvider>
    </>
  );
}

export default App;
```

### 3. Fetch and display clients
        
```src/components/Clients.jsx``` has a role to fetch and display clients data. For doing this, we need to import ```gql``` from ```@apollo/clients```. The query we want to execute by wrapping it in the gql template literal defined like below.
        
```javascript
const GET_CLIENTS = gql`
  query getClinets {
    clients {
      id
      name
      email
      phone
    }
  }
`
```
    
Whenever this component renders, the useQuery hook automatically executes our query and returns a result object containing loading, error, and data properties:

- Apollo Client tracks a query's error and loading state for you, which are reflected in the loading and error properties.
- When the result of your query comes back, it's attached to the data property.
        
At this project, we should show up client data like this.
        
```javascript
export default function Clients() {
  const { loading, error, data } = useQuery(GET_CLIENTS);

  if (loading) return <p>loading...</p>;
  if (error) return <p>Something Went Wrong</p>;

  return (
    <>
      {!loading && !error && (
        <table className="table table-hover mt-3">
          <thead>
            <tr>
              <th>Name</th>
              <th>Email</th>
              <th>Phone</th>
              <th></th>
            </tr>
          </thead>
          <tbody>
            {data.clients.map((client) => (
              <ClientRow key={client.id} client={client} />
            ))}
          </tbody>
        </table>
      )}
    </>
  );
}
```
Then we can see the Project Management App like below.

<img width="450" alt="image" src="https://user-images.githubusercontent.com/39740066/175552898-3a0d88cd-21f2-4301-a91f-1f6065e6fcdb.png">

### 4. Implement react-router-dom

In order to show up the project view page, we need to use ```react-router-dom``` on the ```App.js```.

```Javascript
import { BrowserRouter as Router, Route, Routes } from 'react-router-dom'
```

After that, you can add ```Router``` setting like below. Inside of ```<Router>```, we can make several ```<Route>``` another inside of ```<Routes>```. Each of route has their own path address and component directed to link. (```<Home />```,```<Project />```,```<NotFound />```).

```Javascript
    <>
      <ApolloProvider client={client}>
        <Router>
          <Header />
          <div className="container">
            <Routes>
              <Route path="/" element={<Home />} />
              <Route path="/projects/:id" element={<Project />} />
              <Route path="*" element={<NotFound />} />
            </Routes>
          </div>
        </Router>
      </ApolloProvider>
    </>
```

- ```useParams```: The useParams hook returns an object of key/value pairs of the dynamic params from the current URL that were matched by the <Route path>. Child routes inherit all params from their parent routes. In this project, ```Project.jsx``` uses ```useParams``` for parsing ```id``` data from <Route path> which is ```ProjectCard.jsx``` indicated.

- ```useNavigate```: The useNavigate hook returns a function that lets you navigate programmatically, for example after a form is submitted. If using replace: true, the navigation will replace the current entry in the history stack instead of adding a new one. In order to move home page after delete project by ```onClick```, we can take ```useNavigate()``` with ```onCompleted``` key value.

DeleteProjectButton.jsx
```javascript
export default function DeleteProjectButton({ projectId }) {
  const navigate = useNavigate();

  const [deleteProject] = useMutation(DELETE_PROJECT, {
    variables: { id: projectId },
    onCompleted: () => navigate('/'),
    refetchQueries: [{ query: GET_PROJECTS }],
  });

  return (
    <div className="d-flex mt-5 ms-auto">
      <button className="btn btn-danger m-2" onClick={deleteProject}>
        <FaTrash className="icon" /> Delete Project
      </button>
    </div>
  );
}
```

## Deploy with heroku

### 1. Setup before deploy.

Before start heroku deploy process, we need to add some codes on ```server/index.js``` for production environment.

```javascript
if (process.env.NODE_ENV === 'production') {
  app.use(express.static(path.join(__dirname, '../client/build')));

  app.get('*', (req, res) =>
    res.sendFile(
      path.resolve(__dirname, '../', 'client', 'build', 'index.html')
    )
  );
} else {
  app.get('/', (req, res) => res.send('Please set to production'));
}
```

Enter ```npm run build``` command inside of ```client``` folder. Then project will be built and ```build``` folder is ready to be deployed.

### 2. Deploy with heroku 

After sign in [heroku website](https://www.heroku.com), ```heroku login``` on the project folder root location. And create new app by using ```heroku create mernappsh```. (mernappsh is a name of heroku application).

You can check heroku app with ```https://mernappsh.herokuapp.com/```.

<img width="450" alt="image" src="https://user-images.githubusercontent.com/39740066/176570127-b7553987-1fe9-48df-8cc7-e50e51a3b4d4.png">

Go to the heroku dashboard, select ```mernappsh``` app and select ```Settings```. Add Config Vars like below.

<img width="450" alt="image" src="https://user-images.githubusercontent.com/39740066/176570643-614f040f-53d7-4bb8-b3e1-face74e170d6.png">
 
Then we can start git push process.
 
```bash
git add .
git commit -m 'Prepare Deploy'
git push heroku master
```

If there is H10 error, this [video clip](https://www.youtube.com/watch?v=68iCwSmSIvA) would be helpful. In order to use graphql in heroku, uri ```http://localhost:5000``` should be deleted related with ApolloClient. You can check this [video clip](https://www.youtube.com/watch?v=ok6bu-3XRA8). 
 
## References
- https://www.youtube.com/watch?v=BcLNfwF04Kw
- https://www.apollographql.com/docs/react/
- https://blog.logrocket.com/react-router-dom-tutorial-examples/
- https://github.com/react-icons/react-icons
- https://www.apollographql.com/docs/react/get-started/
