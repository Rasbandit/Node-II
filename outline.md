# Node II - Massive.js

## Slides

- We use axios to run HTTP requests between client and server.
- We use Massive to communicate between server and DB.
  - Massive is a tool that can run SQL queries and convert the results javascript objects.
- We also use postman to run HTTP requests.

- What is CRUD?
  - Go over CRUD for HTTP.
    - Post
    - get
    - put
    - delete
  - Crud for SQL.
    - Insert Into
    - select
    - update/set
    - delete

- How does SQL select become JS
  - response is an array.
    - rows are objects with properties being the column names.

## Heroku DB

- Talk about why we need to put our DB online.
- Go online and have them create a heroku account.
- Create a project and have them add in a portress app.
  - take the credentials and link it to PGAdmin.
- take the seed file from yesterday and have them paste it in so we have data to play with.

## Node

- Make a basic node server and get the app listening on port, what ever.
  - Take the time to be a basic review of node
- Make a single endpoint and make sure everyone can hit it from postman.
- Then connect massive to your DB.
  - You have to put `?ssl=true` to the end of the connection string.
- Talk about the issue we just introduced by having our connection string in the index.js file.
- Intro to `dotenv` and why its so cool.
  - now your secret info won't go up to github
- Create a DB folder inside of the root directory.
  - inside this create an SQL file with that runs select all from any table.
- now tie it to our endpoint and have it run.
- This will always be an array even if we get just one item.
- Go over other basic crud and do one of each.
- If you have time time going over params/queries.
- If you have even more time go over the issues with nodemon restarting when the frontend changes.
  - introduce nodemon.json
