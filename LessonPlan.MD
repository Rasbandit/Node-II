## Author(s)

Missy Beutler

## Last Objectives Review Date

If you teach this lecture review the objectives, and update this date if the objectives still match this document:

11/16/2017

## Lecture video

[3.3 Massive I / Node II](https://vimeo.com/248010455/94bf1acd86)

## Resources

[Links or references to images, slides, clips, etc]

- [Node 2 Review Kahoot](https://play.kahoot.it/#/?quizId=4fe599a5-2dd5-4861-a54c-b835b807170a)

## Flow

### Major goals/notes

- Make sure to explain how this fits into the big picture. I like to draw a computer, a server, and a database. With the computer I write React, with the server I write Node Express and with the Database I write postgreSQL. I then draw arrows between the computer and the server and ask what they use to communicate between the two (axios) and write it on the board. I then draw arrows back and forth from the server to the database and explain how Massive is how your server will be talking to your database.
- We used to install Postgres and PGAdmin on the student's computers so that they could use a local database but this caused so many issues that we decided to stop. Now we use heroku databases with SQL Tabs to make queries. Here is a great repo from Jason Staten with instructions on how to do so: https://github.com/statianzo/sql-setup
  - I try to have them set this up before the lecture with the mentors and make sure everything is good to go so that the lecture isn't held back from having issues.
- I also really try to emphasize the difference between queries and params and when to use each of them.

### Structure, timing, order
- What is Massive? 
  - It allows you to connect to your database so you can retrieve and manipulate data.
  - Make sure they know they are using V3, V2 has different syntax.
  - I then create a basic server with them walking me through the steps as a basic review. Once that's all set up, I have them install and require `massive`. The connection string will be coming from their heroku database that they should already have signed up for and set up.

  ```js

  massive( process.env.CONNECTION_STRING ).then(db => {
    app.set('db', db)
  })

  ```

  - When talking about the syntax...
    - Make sure they put their `.env` in their `.gitignore` and their connection string in their `.env`. This is where I teach about `.env`.
    - If they ask, this is the break down of what parts mean what on their connection string `postgres://[username]:[password]@[host]:[port]/[database]`. I usually only bring it up if it works in nice at the time or someone is curious.
    - Massive is just a function that is being invoked with the connection string to the database. You need to use `.then()` after. When it comes to explaining when to use `.then()` and when to not, I like to describe it simply. If you're doing something that is leaving your app (API call, connecting to your database, etc...) it's going to take a second and because it's taking a second, you need `.then()` to catch the response when it comes back. 
    - Once in the the `.then()`, they should understand that it takes a callback function. The parameter of the callback function will be the connected DB instance (object).
    - Inside the callback of the `.then()`, you need to put the DB instance on the the app object so we can access it later. `app.set('db', db))`. You only do this one time so you can reuse it over and over again.
  - I then make the db folder in the root of the project and start making `sql` files.
    - I first will explain the concept of seed files and make one in an `init` folder and set it up in the server file and run nodemon. This is a great opportunity to use SQL Tabs. Running the seed file will put data in the database which you can easily see in SQL Tabs so the student sees what's happening.
    - After, I create as simple sql statement and will make a simple endpoint that will make the database call with `req.app.get('db').someSqlQuery()`.
    - I make sure to emphasize that the method (someSqlQuery) is being made by massive from the files in the db folder. You can even look at the `db` object and see the method on the object.
    - I also point out that a very common error is `req.app.get(...).someSqlQuery() is not a function` which is usually one of two things:
      - The level of where the db folder is and where you run nodemon is very important and should be the same because it will break if you don't do it right and then `someSqlQuery` will in fact, not be a function.
      - The spelling between the sql file name and the method that's being invoked is wrong. They must be the same.
    - After the invocation of the sql statement function, because it's "going away from the app to somewhere else", we need a `.then()`. The response that will be the argument in the `.then()` callback is the data from the database which you then can do as you please.
- Inserting data to a DB with endpoints
  - Just like a function has parameters and arguments, so do the SQL statements. The parameters (or references to the arguments... postgres docs never define them as parameters but only say references to the arguments) in the SQL statement is defined as `$n` and the arguments are the information given when the SQL statement is invoked. `$1` referring to the first argument, `$2` to the second and so forth. 
  - If there is more than one argument, you need to place them in an array. Otherwise a single argument is good on it's own. I'll show one argument first and then how with more than one, you need the array.
  - I also point out destructuring from `req.body` to use with multiple arguments being passed.
- Go into queries
  - I do a quick refresher on params. I draw out the endpoint, the request url and the req.params object holding the data in a key value pair. I draw circles around each portion connecting them. The word after the colon in the endpoint url will be the key name in the req.params object. The value in the request url will be the value in the req.params object. Emphasize that the key value pair in the req.params object. I also emphasize that params are required, you can't hit the endpoint if you don't have data in the place you've specified.
  - I then introduce queries.
    - When they've used them before -- I show a search with amazon and the url with the query.
    - Queries are optional, you don't specify it in an endpoint like you do with params.
    - To make an HTTP request, you put in the url `?key=value&key=value`. I build an endpoint and make requests with postman to show how the key value pairs can be found on the req.query object.
    - I emphasize that they are controlling the reins and the only queries that are important are the ones that they are paying attention to. Someone could send in more queries but it doesn't matter because you'll only be using them if you're planning for it.
    - I like to show using queries with an exisiting endpoint to emphasize that they are in fact optional and that the endpoint can do other things if no queries are provided.
- Mini project!