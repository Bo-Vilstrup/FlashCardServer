# ProjectFlashCardServerSeed

ProjectFlashCard Server Seed is my first attempt to make a useful seed to project flashcard.
The basic part of the seed is taken from the express-generator in webStorm.

## I have added the following things to the express-generator seed:

#### A new directory structure:

- app (new)
    - controllers (new)
    - models (new)
    - routes (moved)
    - views (moved)


#### Refactor -> Renamed app.js to server.js

#### Changes made to server.js

```javascript
 // view engine setup
    app.set('views', path.join(__dirname, 'views'));
```

Changed to:
 
```javascript
 // view engine setup
    app.set('views', path.join(__dirname, 'app/views'));
```


#### add gitignore file

#### change package.json

    By default, OpenShift does not start the server via npm start, so you need to add the following statement,
    "main": "./bin/www", to your package.json file as sketched below:
    "scripts": {
    "start": "node ./bin/www"
    },
    "main" : "./bin/www",
    
    
    "test": "node_modules/.bin/mocha -w"

#### Change bin/www

Open the bin\www file and replace these lines:
var port = normalizePort(process.env.PORT || '3000');
app.set('port', port);

with:

var port = normalizePort(process.env.OPENSHIFT_NODEJS_PORT || '3000');
app.set('port', port);
var ip = process.env.OPENSHIFT_NODEJS_IP || '127.0.0.1';
app.set('ip', ip);

Now localize the line that starts the server : server.listen(port); and replace it with this:
server.listen(port, ip);



