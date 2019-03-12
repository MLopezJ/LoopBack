# Leaning Loop Back

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
* Type yes to accept the dedault and expose the model via REST
* Press entender to accept the default plural name to the model 
* Use common model to be used in both sides (server and client)
* Define the model properties  
* Type "node  . " in cmd to run the program




### Installation errors

#### cannot open input file 'C:\OpenSSL-Win64\lib\libeay 32.lib'

In windows, this error is solved dwonloding C:\OpenSSL-Win32\lib folder from here (https://github.com/ReadyTalk/win32/blob/master/msvc/lib/libeay32.lib) and add it to C:\OpenSSL-win64\lib folder