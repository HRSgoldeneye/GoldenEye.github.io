# Table of Contents

* [About GoldenEye](#about-goldeneye)
* [Inspiration](#inspiration)
* [Features](#features)
* [How will it look](#how-will-it-look)
* [Installation](#installation)
* [Application design](#application-design)
  * [Directory structure](#directory-structure)
  * [Import conventions](#import-conventions)
  * [Naming conventions](#naming-conventions)
  * [Data model](#data-model)
  * [CSS](#css)
  * [Routing](#routing)
  * [Authentication](#authentication)
  * [Authorization](#authorization)
  * [Configuration](#configuration)
* [About Us](#about-us)
* [Development History](#development-history)
    * [Milestone 1: Data and ElasticSearch](#milestone-1-data-and-elasticsearch)
    * [Milestone 2: Front End and Other Improvements](#milestone-2-front-end-and-other-improvements)
    * [DigitalOcean and Laravel Forge Deployment](#digitalocean-and-laravel-forge-deployment)

## About GoldenEye

As part of ICS-491, our group participated in the 2017 Hawaii Annual Coding Challenge as GoldenEye and took on the challenge of making the Hawaii Revised Stautes easily accessible. Goldeneye comes from the James Bond movie of the same name. But rather on being a Soviet super weapon, it's an app made to simplify the process of accessing and updating Hawaii's laws.

## Inspiration

Besides a great challenge, the current problems with accessing the statutes is that it's very tedious looking through the statutes. With over 20,000 sections, there is no database and no way to search for a particular statute or section. There's also no way to cross reference another statute if it's listed in another staute. 

On the official Hawai’i Government [Website](https://portal.ehawaii.gov/government/hawaii-legislature/hawaii-revised-statutes/), the statutes are on a file server. This means that it's another obstacle to update or edit statutes. Currently, the statutes are officially updated once a year. With this slow process, there is no consistency and typos are common for some statutes.

## Features

With our team, we plan to use the laravel framework as our foundation to creating a dynamic web application that can be accessed on ac computer or a smart phone. With mysql as our database and using the ElasticSearch package, we wanted to make a common sense search engine that will query results a user expects to see. To increase the long term support of the app, we want to create an easy to use administrative side that allows a layman to maintain the statutes within our app. Along with the other teams creating similar solutions, we collaborated on making a free and open source scrapper that allows other developers to have all the statutes or some parts of it in a simple JSON file.


![image](/images/homepage.png)

At the home page, a user can start searching for sections that realate to their input.

![image](/images/socialmedia.png)

Because HRS Goldeneye is a dynamic web app, users can share a statute to someone by email and facebook.

![image](/images/search.png)


![image](/images/search-results.png)

Relevant searches show their section name and the respective section number.

![image](/images/statute.png)

When a user clicks on a search result, it'll take them to the whole statute, allowing the user to read the entire statute or particular sections they find interesting. 

![image](/images/sections.png)

All the sections are nicely collapsible (as some sections are very lengthy) allowing a user to easily manuver through a statute. 

# Installation/Contributing to The Project 

For a free visual guide on installing laravel and developing on it: use [laracasts](https://laracasts.com/series/laravel-from-scratch-2017).

## Setting Up Your Dev Environement

### Downloading VirtualBox
Download the free Oracle VirtualBox Application [here](https://www.virtualbox.org/wiki/Downloads)
### Downloading Vagrant
Download Vagrant [here](https://www.vagrantup.com/downloads.html)
### Installing Laravel Homestead
Clone the latest version of [Laravel Homestead](https://github.com/laravel/homestead/releases) and be sure to keep track of what version you downloaded. 
```
$ git clone https://github.com/laravel/homestead.git homestead
```
The last part of the command is the name of directory the repo will be cloned into. Go into that directory and checkout the latest version number.
```
$ cd homestead
$ git checkout v7.1.0
```
As of writing this, version 7.1.0 was the newest one.

After checking out homestead, initialize it using:
```
$ bash init.sh
```

Then edit your Homestead.yml file:
```
---
ip: "192.168.10.11"
memory: 2048
cpus: 1
provider: virtualbox

authorize: ~/.ssh/id_rsa.pub

keys:
    - ~/.ssh/id_rsa

folders:
    - map: /Users/MarkCummins/Desktop/github/ics-491-goldeneye
      to: /home/vagrant/Code/ics-491-goldeneye

sites:
    - map: ics-491-goldeneye.app
      to: /home/vagrant/Code/ics-491-goldeneye/public

databases:
    - goldeneye

# blackfire:
#     - id: foo
#       token: bar
#       client-id: foo
#       client-token: bar

# ports:
#     - send: 50000
#       to: 5000
#     - send: 7777
#       to: 777
#       protocol: udp
```

The only line that will be different in your Homestead.yml file is the folders map. That will be where ever you want to put the repo of the project on your local machine.

To make it so that the virtual machine points toics-491-goldeneye.app, simply do (For Mac):
```
$ sudo pico /etc/hosts
```
Add a line relating the ip address we had in Homestead.yml to the site mapping:
```
##
# Host Database
#
# localhost is used to configure the loopback interface
# when the system is booting.  Do not change this entry.
##
127.0.0.1       localhost
255.255.255.255 broadcasthost
::1             localhost
192.168.10.11 ics-491-goldeneye.app
```
### Configuring Vagrant
Once you're done editing the files, the next step is to add laravel homestead to Vagrant with:
```
$ vagrant box add laravel/homestead
```
This will download the LAMP stack into your virtualbox, giving you all the things you need to develop your laravel app in the virtual machine. Be sure to press whichever button that says virtualbox when it's installing.

Our machine is all set, now we have to bring it up using the command:
```
$ vagrant up
```
Then ssh into your vagrant box using the command:
```
$ vagrant ssh
```
### Enabling Port Forwarding On The VirtualBox
Since we'll be using port 9200 and 5601 for ElasticSearch and Kibana, we need to enable port forwarding for them. Open the VirtualBox application, right click on the homestead virtual machine and go to settings. Go to the network tab, click on the down arrow for advanced, and click on port forwarding:

![image](/images/advanced-settings.png)

Then add the ports 9200 and 5601 to the list by pressing the green plus button

![image](/images/add-ports.png)


### Installing ElasticSearch
The first step to installing ElasticSearch is to get the public key:
```
$ wget -qO - https://artifacts.elastic.co/GPG-KEY-elasticsearch | sudo apt-key add -
```

Then add the ElasticSearch repository:
```
$ echo "deb https://artifacts.elastic.co/packages/5.x/apt stable main" | sudo tee -a /etc/apt/sources.list.d/elastic-5.x.list
```
Then add the required repositories:
```
$ sudo apt-get update
$ sudo apt-get install default-jdk
$ sudo apt-get install elasticsearch
```
To start and stop ElasticSearch, type:
```
$ sudo systemctl start elasticsearch
$ sudo systemctl stop elasticsearch
```
Now we have to edit some settings in ElasticSearch. Simply edit the lines in:
```
$ sudo pico /etc/elasticsearch/elasticsearch.yml
```

```
cluster.name: elasticsearch_cluster
node.name: elasticsearch_homestead
network.host: 0.0.0.0
```
### Installing Kibana
Kibana is a web ui that allows you to easily manage your ElastiSearch cluster and nodes. To install it, simply type the command:

```
$ sudo apt-get install kibana
```

Then configure some settings in kibana by doing:
```
$ sudo pico /etc/kibana/kibana.yml
```
Then change the line:
```
server.host: "0.0.0.0" 
```
and add this line at the bottom:
```
xpack.securityenabled: false
```
Then run the commands:
```
$ sudo /bin/systemctl daemon-reload
$ sudo /bin/systemctl enable kibana.service
$ sudo /bin/systemctl start kibana.service
```

When you start ElasticSearch and Kibana, you should be able to type "0.0.0.0:5601" into your browser and the kibana browser interface should show up.

### Configuring ElasticSearch Mapping

With the kibana app running, go to the console in dev tools and put in:

```
PUT hawaii-statutes {
  {
    "mappings": {
      "sections": {
        "properties": {
          "id": {
            "type": "long"
          },
          "section_name": {
            "type": "text",
            "fields": {
              "keyword": {
                "type": "keyword"
              }
            }
          },
          "section_number": {
            "type": "text",
            "fields": {
              "keyword": {
                "type": "keyword",
                "ignore_above": 256
              }
            }
          },
          "statute_id": {
            "type": "integer"
          },
          "text": {
            "type": "text",
            "fields": {
              "keyword": {
                "type": "keyword"
              }
            }
          }
        }
      }
    }
  }
```

This is the basic mapping of the database, it's highly encouraged to edit and imporove the mapping. 

### Cloning The Repo
In the ics-491-goldeneye directory of the vagrant box simply type:
```
$ git clone https://github.com/HRSgoldeneye/GoldenEye.git
```

Once the repo is cloned, you'll want to add a local .env file like so. The .env file is in the ics-491-goldeneye directory:
```
APP_NAME=Laravel
APP_ENV=local
APP_KEY=base64:I9Pzssv/YOHVCbfgFOGu05DvFDp4x3x3Z8NSsnPhMNo=
APP_DEBUG=true
APP_LOG_LEVEL=debug
APP_URL=http://localhost

DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=goldeneye
DB_USERNAME=root
DB_PASSWORD=

BROADCAST_DRIVER=log
CACHE_DRIVER=file
SESSION_DRIVER=file
QUEUE_DRIVER=sync

REDIS_HOST=127.0.0.1
REDIS_PASSWORD=null
REDIS_PORT=6379

MAIL_DRIVER=smtp
MAIL_HOST=smtp.mailtrap.io
MAIL_PORT=2525
MAIL_USERNAME=null
MAIL_PASSWORD=null
MAIL_ENCRYPTION=null

PUSHER_APP_ID=
PUSHER_APP_KEY=
PUSHER_APP_SECRET=


SCOUT_DRIVER=elasticsearch
```

Once that's done, do a composer install and update so that all dependencies are installed and updated:
```
$ composer install
$ composer update
```

### Populating the Database

To populate the database with the JSON file already included, simply go to artisan tinker and run the function:

```
php artisan tinker
\App\Libraries\JSONPersister::persist()
```


### Final Steps

If all goes well, you should be able to go to ics-491-goldeneye.app, do searches, and start developing!

# Application Design

## Blade Files

Webpages are constructed as blade files. Blade files allow you to have your HTML call your PHP functions and have them interact with your models and routes while the logic is stowed away in your Controllers. All blade files are located in the /resources/views directory. For organization, it's recommded to put all the layout HTML into a separate layout directory and your web pages into a pages directory within the views directory.

## Eloquent Models

Eloquent models are simple ways to create an object that reflect something you store in your database. Models make it easy to query data and insert new records into your database tables. By convention, your model is the singular version of the class while your database will use the plural version for the table. For our project, models were made for the divisions, titles, statutes, and sections of the data while creating relationships for them.

## Database

By default, laravel uses mysql. Migrations are "version control" for your database tables, simplying the act of modifying the database schema. If changes need to be made to tables, the modification in the editor, and the backend mchange can be done with one artisan command.

## CSS

For this project, we used BootStrap 4 that comes by default in laravel. Bootstrap allows our project to satisfy usuability issues for both web and mobile app users. 

## Configuration

The config directory contains configuration settings for laravel packages like authentication, databases, and anything else you include in your application. 

# About Us
Team GoldenEye consists of two students: 

* [Mark Cummins](https://github.com/markrcummins)
* [Yohan Yang](https://github.com/yohanyang)

# Development History

The development process for GoldenEye conforms to [Issue Driven Project Management](http://courses.ics.hawaii.edu/ics314s17/modules/project-management/) practices. In a nutshell, development consists of a sequence of Milestones. Milestones consist of issues corresponding to tasks. GitHub projects are used to manage the processing of tasks during a milestone. 

The following sections document the development history of the UHM ICS BookMarket.

## Milestone 1: Data and ElasticSearch

This milestone started on October 2, 2017 and ended on November 6, 2017.

The goal of Milestone 1 was to implement the backend and data portion of our app. The first part was collaborating with other groups to create an free and open source [HRS scrapper](https://github.com/OpenHRS/openhrs-scraper-app). The second part was creating a relational database that could insert the JSON file that the scrapper generated. The third part was configuring the ElasticSearch package so that statutes and sections could be searched and relevant results would show. The final part was successfully deploying a live version of the app. 

## Milestone 2: Front End and Other Improvements

This milestone started on November 6, 2017 and ends on December 1st, 2017. This milestone consists of greatly overhauling every aspect of the app. This includes the front end and the back end of app. The first is utilizing the elasticsearch engine on the production version of the app and optimizing the search mapping. The second part is utilizing the CSS framework [materializecss](http://materializecss.com/table.html) and the front end framework [vue.js](https://vuejs.org/). The third part is to implement an administrative account that allows one user/account to make changes to the production version of the application. Finally, we want to implement sound software engineering principles like testing on both the desktop and mobile version of GoldenEye. 

## DigitalOcean and Laravel Forge Deployment

To test certain features and to meet the requirements of the class, our [app is deployed here](http://67.205.189.163/). Our deployment is made by creating our server on DigitalOcean and managing it with Laravel Forge. 

