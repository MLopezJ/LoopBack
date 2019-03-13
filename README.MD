# Learning Loop Back

## About


## Main goal
> get familiary with Loop back

## Install 
> npm install -g loopback-cli

## Tags

### Version 0
Only readme file 

### Version 1: Simple API

This is the first step in the tutorial. Its about a simple API with 1 model, this model is a CoffeeShop with two properties (name, city). More information can be found in this link: https://loopback.io/doc/en/lb3/Create-a-simple-API.html

#### How to


* Use the Loop back aplication generator. Type the next command in console:
    > lb
* Choose the application name
* Choose hello-world as a kind of application to create
* Create models typing the follow command
    > lb model
* Attach the model to any data source. in this case, choose:
    > db (memory)
* To eventually connect this model to a persistent data source in a database, choose PersistedModel
* Type yes to accept the default and expose the model via REST
* Press entender to accept the default plural name to the model or type one
* Use common model to be used in both sides (server and client)
* Define the model properties  
* Type "node  . " in root folder to run the program


### Version 2: Use API explorer
We just have made a REST API in the previous step. So, now we goint to explorer the LoopBack tools. 

LoopBack provide us `API Explorer`, who is a document of our API. It can be checked after running the next command in root folder:
> node .

Then, go to the following link:
> http://localhost:3000/explorer/

You will found yours modals and his end points. Also, if you clicked into an specific end point, it show you details like an example of the return value, the data type, parameters, and so on. 

More information can be found in this link: https://loopback.io/doc/en/lb3/Connect-your-API-to-a-data-source.html

### Version 3: Connect API to a data source

Its time to connect our API to a data source, in this case we are goint to use MySQL. 

We can use a MySQL server provide by LoopBack which is hosting in demo.strongloop.com, but it will only works for us for testing. For that reason, its preferable to use your own server, so, lets create our database and server first

In my case, I have an image of MySQL 5.7 in Docker, so, I proceed to create a container of it typing the next command:

> docker run -e MYSQL_ROOT_PASSWORD=admin --name=loopback -d -p=3306:3306 mysql:5.7

Then, I create a new MySQL connection using Workbench with the following information:
* Connection name: __mysqlDs__
* Hostname: __127.0.0.1__
* Port: __3306__
* Username: __root__
* Password: __admin__

Next, I create a schema of the database called __loopback__

When you already have it all, you can type the next command in the root folder to define the data source:
>lb datasource

And then, type the name of the data source. In this case, it will be __mysqlDs__ but could be whatever you want. When you already type the name, select the type of data source, in this case __MySQL__

When you already entry this data, the generator will ask you about connections settings like port, host, database and so on. You can provide it in URL or individually. If you want to set it individually, type enter when generator ask for the connection string URL.

Next, you have to response many questions about the connection:

* Host: The same host input in MySQL connection
* Port: The same port input in MySQL connection
* User: The same username input in MySQL connection
* Password: The same password input in MySQL connection
* Database: The same name of schema input in MySQL connection
* Do you want to install loopback-connector-mysql: yes

This information will generate a json file called datasource in server folder, if you want change something you can do it in */server/datasource.json*

Now, we have created a data source and a model, you just need to connect both. For that, we are goin to model-config.json in server folder (*/server/model-config.json*) and change the default data source (db) for our data source name (mysqlDs)

If you want to add some test data you can add it automatically by server boot. For that, go to *server/boot* and then, create a new file called *create-sample-models.js* and type the following code

```
module.exports = function(app) {
  app.dataSources.mysqlDs.automigrate('CoffeeShop', function(err) {
    if (err) throw err;

    app.models.CoffeeShop.create([{
      name: 'Bel Cafe',
      city: 'Vancouver'
    }, {
      name: 'Three Bees Coffee House',
      city: 'San Mateo'
    }, {
      name: 'Caffe Artigiano',
      city: 'Vancouver'
    }], function(err, coffeeShops) {
      if (err) throw err;

      console.log('Models created: \n', coffeeShops);
    });
  });
};
```

It will generate test data any time the serevr is up


## Installation errors

#### cannot open input file 'C:\OpenSSL-Win64\lib\libeay 32.lib'

In windows, this error is solved dwonloding C:\OpenSSL-Win32\lib folder from here (https://github.com/ReadyTalk/win32/blob/master/msvc/lib/libeay32.lib) and add it to C:\OpenSSL-win64\lib folder