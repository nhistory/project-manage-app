# project-manage-app

## Table of Contents

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

## Mongodb atlas
[Mongodb atlas](https://www.mongodb.com/cloud/atlas/lp/try2?utm_source=google&utm_campaign=gs_americas_canada_search_core_brand_atlas_desktop&utm_term=mongodb%20atlas&utm_medium=cpc_paid_search&utm_ad=e&utm_ad_campaign_id=12212624311&adgroup=115749704343&gclid=CjwKCAjw46CVBhB1EiwAgy6M4oIvFcJ5cjdYixiQOZl9QAf-ot3E0qVDwE8g9m5PAYi_qoTZL4yKvBoCdOwQAvD_BwE) is a cloud-based mongobd service that should not install any program on the local machine.
- Sign up with google acount and build a database.
<img width="450" alt="image" src="https://user-images.githubusercontent.com/39740066/173707549-81ef9192-a24a-491f-94c6-154a829d3c27.png">
- Select share version and create cluster.
<img width="450" alt="image" src="https://user-images.githubusercontent.com/39740066/173707693-417d35b7-98dd-48ce-867c-d1313e925f6d.png">
- Add my local ip address and finish
<img width="450" alt="image" src="https://user-images.githubusercontent.com/39740066/173708325-5272284c-49aa-4728-9967-9871150844f4.png">
- Create database with own name mgmt_db and clients.
<img width="450" alt="image" src="https://user-images.githubusercontent.com/39740066/173708913-09631f48-902f-4e1a-babf-b55798ba0e77.png">
 
