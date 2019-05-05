### MEAN with FLEK

Welcome to Demo Application.

## MEAN stack

The mean stack is intended to provide a simple and fun starting point for cloud native fullstack javascript applications.   
MEAN is a set of Open Source components that together, provide an end-to-end framework for building dynamic web applications; starting from the top (code running in the browser) to the bottom (database). The stack is made up of:

- **M**ongoDB : Document database – used by your back-end application to store its data as JSON (JavaScript Object Notation) documents
- **E**xpress (sometimes referred to as Express.js): Back-end web application framework running on top of Node.js
- **A**ngular (formerly Angular.js): Front-end web app framework; runs your JavaScript code in the user's browser, allowing your application UI to be dynamic
- **N**ode.js : JavaScript runtime environment – lets you implement your application back-end in JavaScript

## FLEK stack

In order to monitor performance of your application or API, we will use FLEK stack for following

- **F**ileBeat : it will help to tail your log files without doing ssh to server
- **L**ogstash : it will help you to filter and parse the logs and transform them required format before loading it ES.
- **E**lastic Search : it will help to store and query logs for debugging
- **K**ibana : it will help you to understand your logs with better way than ever with help of beautiful Visualizations 

### Pre-requisites
* git - [Installation guide](https://www.linode.com/docs/development/version-control/how-to-install-git-on-linux-mac-and-windows/) .  
* node.js - [Download page](https://nodejs.org/en/download/) .  
* npm - comes with node or download yarn - [Download page](https://yarnpkg.com/lang/en/docs/install) .  
* mongodb - [Download page](https://www.mongodb.com/download-center/community) .  
* Sign up with [elastic.co](https://www.elastic.co/cloud/) for 14 days free trial 

### Docker based 
``` 
git clone https://gitlab.com/shaadi/hackfest2019/elasticstack-filebeat-demo
cd mean
cp .env.example .env
docker-compose up -d
```

### Credits 
- The MEAN name was coined by Valeri Karpov.
- Initial concept and development was done by Amos Haviv and sponsered by Linnovate.
- Inspired by the great work of Madhusudhan Srinivasa.
- elastic.co for 14 days free trial

### About Demo

It is very basic web application, which can help us to understand `how does FLEK stack works?`

Here is workflow to follow

1. Access a home page, [0.0.0.0:4040](http://localhost:4040/)
2. `mean/server/config/log` will hold maintain the `access.log` with help of morgan npm module
3. Filebeat will keep harvesting the `access.log` file which holding a log lines in json format
4. A mentioned in configuration file. logstash will decode json log lines and load it into the ES
5. With help of Kibana, you can query and debug the log lines and you can also form the visualizations

Importance of the following files

- `dockerconf/Dockerfile` : This file is responsible for main application which will be running on [0.0.0.0:4040](http://localhost:4040/)
- `dockerconf/filebeat.yml` : This file is responsible for configuration of filebeat. For current demo, we'll use it to define input style of logs and to mention logstash connection
- `dockerconf/logstash.conf` :  This file will hellp you to configure the logstash, in order to filter and transform the logs before loading it to elastic search.
- `dockerconf/docker-compose.yml` :  This is the composer file which will help you to configure your stack
- `dockerconf/logstash.yml` : Need to explore!!!

What's remaining to cover?

- How to collect docker container logs (using tags in filter) without breaking current working Application?
- Clean up logs by setting up the clean cron on application logs 


