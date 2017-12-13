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


# How will it look

PC View

![image](/images/pagemain.jpg)

![image](/images/pageabout.jpg)

Mobile View

![image](/images/picture1.png)

![image](/images/picture2.png)


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
### Cloning The Repo

### Populating the Database

### Installing ElasticSearch and Kibana

### Final Steps


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

