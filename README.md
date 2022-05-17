# product_server
https://surajproductdata.herokuapp.com/products


# Deploying Fake Back-End Server & DataBase Using JSON-SERVER, GitHub, and Heroku.

we will create and host a fake product db server that we can deal with it as a normal Back-End Server and use all the CRUD Operations using HTTP requests.

# 1.Creating the Fake Server.

> You can download the final result [HERE](https://github.com/mm-asraf/product-server), Or follow along with me.

- Create a folder and name it `fake-server`.
- Open the terminal and init npm, and make the entry point `server.js`

```
npm init
```

- install [json-server](https://www.npmjs.com/package/json-server).

```
npm i json-server
```

- Add a `start` script.

package.json

```
{
  "name": "product-server",
  "version": "1.0.0",
  "description": "product-server with fake database",
  "main": "server.js",
  "scripts": {  // <===
    "start": "node server.js" // <===
  },
  "author": "mm-asraf",
  "license": "ISC",
  "dependencies": {
    "json-server": "^0.16.3"
  }
}
```

- create `.gitignore` file and add `node_modules`.
  .gitignore

```bash
node_modules
```

- Create `server.js` file and paste the following

```js
const jsonServer = require("json-server");
const server = jsonServer.create();
const router = jsonServer.router("db.json"); // <== Will be created later
const middlewares = jsonServer.defaults();
const port = process.env.PORT || 5000; // <== You can change the port

server.use(middlewares);
server.use(router);

server.listen(port);
```

- init git and publish your repo to [GitHub](https://github.com/)

```bas
git init
git remote add origin https://github.com/<YourName>/<Repo-Name>.git
git add .
git push  origin master
```

> Download the final Repo from [HERE](https://github.com/mm-asraf/product-server)

# 2. Creating the DataBase

- Create `db.json` file
- Fill in any data you like, I used to fill some data you can use [Mockaroo](https://www.mockaroo.com/) to generate dummy data.

db.json

```json
{
  "categories": [
    {
      "id": 1,
      "title": "men",
      "img": "https://n.nordstrommedia.com/id/sr3/264878d1-083a-4b52-b13f-5cf490d8f501.jpeg?crop=pad&pad_color=FFF&format=jpeg&w=780&h=1196"
    },
    {
      "id": 2,
      "title": "women",
      "img": "https://n.nordstrommedia.com/id/sr3/caca27b4-e81a-4a59-81ca-81f2efe94c09.jpeg?crop=pad&pad_color=FFF&format=jpeg&w=780&h=1196"
    },
    {
      "id": 3,
      "title": "kids",
      "img": "https://s3.ap-south-1.amazonaws.com/tcsonline-live/catalog/category/land-boys_2.jpg"
    },
    {
      "id": 4,
      "title": "Beauty & Fragnance",
      "img": "https://thumbs.dreamstime.com/b/woman-perfumes-bottle-sexy-lips-pink-lip-close-up-sexy-plump-soft-lips-dark-red-lipstick-beautiful-girl-using-perfume-220313544.jpg"
    }
  ],
  "products": [
    {
      "id": 1,
      "img": "https://n.nordstrommedia.com/id/sr3/d74ef791-c49b-4364-882b-24945703da60.jpeg?h=365&w=240&dpr=2",
      "brand": "Fear of God Essentials",
      "title": "Cotton Jersey Short Sleeve T-Shirt",
      "price": 3285.14,
      "rating": 3,
      "categoryid": "men",
      "product_type": "clothing",
      "gender": "male"
    },
    {
      "id": 2,
      "img": "https://n.nordstrommedia.com/id/sr3/984bbc27-aa48-4663-93fc-450c81d58ee7.jpeg?h=365&w=240&dpr=2",
      "brand": "Fear of God Essentials",
      "title": "Long Sleeve Cotton Jersey T-Shirt",
      "price": 4106.43,
      "rating": 4,
      "categoryid": "men",
      "product_type": "clothing",
      "gender": "male"
    },
    {
      "id": 3,
      "img": "https://n.nordstrommedia.com/id/sr3/8169be50-81dd-4f49-80ca-9bd778a8fc59.jpeg?h=365&w=240&dpr=2",
      "brand": "7 Diamonds",
      "title": "Grant Slim Fit Solid Stretch Short Sleeve Button-Up Shirt",
      "price": 6488.16,
      "rating": 5,
      "categoryid": "men",
      "product_type": "clothing",
      "gender": "male"
    },
    {
      "id": 4,
      "img": "https://n.nordstrommedia.com/id/sr3/f8cc0af6-e933-4ad4-82f8-6dc29695d889.jpeg?h=365&w=240&dpr=2",
      "brand": "7 Diamonds",
      "title": "Eclipse Print Polo",
      "price": 2688.16,
      "rating": 4,
      "categoryid": "men",
      "product_type": "clothing",
      "gender": "male"
    },
    {
      "id": 5,
      "img": "https://n.nordstrommedia.com/id/sr3/7bfdefa6-56e3-4a9d-b2ba-ba5d8754f21f.jpeg?h=365&w=240&dpr=2",
      "brand": "adidas",
      "title": "Quarter-Zip Training Top",
      "price": 3026.44,
      "rating": 3,
      "categoryid": "men",
      "product_type": "clothing",
      "gender": "male"
    }
  ]
}
```

- Push your work

```bash
git add .
git commit -m "Adding some data to database"
git push
```

# 3. Creating the server

- Create account on [Heroku](https://heroku.com)
- Install the [Heroku CLI](https://devcenter.heroku.com/articles/heroku-cli) on your computer
- Open the terminal and log in then follow the instructions

```bash
heroku login
```

- Create a project

```bash
heroku create fake-server
```

- Push your app to Heroku

```bash
git push heroku master
```

- Open your created app

```bash
heroku open
```

You will see something like this:

![Heroku App](https://dev-to-uploads.s3.amazonaws.com/i/iwmhzzeqrkd74nvu8v3g.JPG)

Now, You can access and modify resources via any HTTP method
`GET` `POST` `PUT` `PATCH` `DELETE` `OPTIONS`

# 4. Creating a Pipeline.

A pipeline is simply a connection between your GitHub repo and your Heroku Project.
So, Whenever you update your `db.json` for example and push your changes to a specific branch Heroku will be listening to this branch and build your app with the updated database.

- Open your dashboard on Heroku and choose your app.

![Alt Text](https://dev-to-uploads.s3.amazonaws.com/i/i81x8oskjdhyj2oia2vh.JPG)

- Navigate to `Deploy` tap and create a pipeline, Connect your GitHub with the fake-server repo

![Alt Text](https://dev-to-uploads.s3.amazonaws.com/i/0pxjlxo43599kcehx82h.JPG)

- Configure auto-deploy and choose the branch of the Pipeline

![Alt Text](https://dev-to-uploads.s3.amazonaws.com/i/ns96n32z0csv0027twzi.JPG)

Now whenever you push the changes to the **selected branch**, the database will be updated and can be accessed via the same base API.
