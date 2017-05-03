# DEPLOYMENT

## DEPLOYMENT GOTCHAS

* npm package name should not duplicate with other ones out there
* add dependencies that you run it as global on your local machine
* bundle.js, bundle.map.js should be uploaded to deploy

## DEVELOPMENT VS PRODUCTION
### Development 

* logging: terminal(console.log)
* 3rd-party app => every developer testing on their own accounts(individually)
* 1 person making request
* db address: localhost:5432
* session secrests, passwords hardcoded
* nodemon: modification, and restart

### Production
* one (centralized) account
* scalability and performance: Mass users(1,000 concurrent users)
* profile img => somewhere another service
* separate the db from node process(db is networked, coming from another hosted computer)
* session secrests, passwords hidden
* NO MODIFICATION => case of crashes, PROCESS PERSISTENCE

## DEPLOY TO HEROKU
```javascript

// first, download CLI tool, create and login your heroku account


// 1. git update
git remote add origin https://github.com/acct/gitreponame.git
git init
git add .
git commit -m "initial"


// 2. create heroku git
heroku create
git remote //now we have heroku git


// 3. heroku setting
heroku config:set NODE_ENV=production
heroku config:set SESSION_SECRET=anythingyouwant
heroku addons:create heroku-postgresql:hobby-dev //DB URL is automatically generated
heroku config //now we can see env variable


// 4. deploy to heroku server
git push heroku master
heroku open


// 5. error detection
heroku logs


```

## HEROKU DATABASE SETUP
```javascript
// 1. clone heroku git repository
heroku git:clone -a APP_NAME
heroku addons: create heroku-postgresql:hobby-dev —-DATABASE


// 2. heroku setup
heroku config -s | grep DATABASE
heroku pg:promote DATABASE_URL


// 3. reset and push local db to the database server
heroku pg:reset DATABASE_URL
heroku pg:push LOCAL_DB_NAME DATABASE_URL --app APP_NAME


```
