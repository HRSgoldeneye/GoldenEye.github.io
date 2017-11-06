# Table of Contents

* [About GoldenEye](#about-goldeneye)
* [Inspiration](#inspiration)
* [Features](#features)
* [How will it look](#how-will-it-look)
* [Installation](#installation)
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

As part of ICS-491, our group participated in the 2017 Hawaii Annual Coding Challenge and took on the challenge of making the Hawaii Revised Stautes easily accessible. Goldeneye comes from the James Bond movie of the same name. But rather on being a Soviet super weapon, it's an app made to simplify the process of accessing and updating Hawaii's laws.

## Inspiration

Besides a great challenge, the current problems with accessing the statutes is that it's very tedious looking through the statutes. With over 20,000 sections, there is no database and no way to search for a particular statute or section. There's also no way to cross reference another statute if it's listed in another staute. 

On the official Hawai’i Government Website, https://portal.ehawaii.gov/government/hawaii-legislature/hawaii-revised-statutes/, the statutes are on a file server. This means that it's another obstacle to update or edit statutes. Currently, the statutes are officially updated once a year. With this slow process, there is no consistency and typos are common for some statutes.

## Features

With our team, we plan to use the laravel framework as our foundation to creating a dynamic web application that can be accessed on ac computer or a smart phone. With mysql as our database and using the ElasticSearch package, we want to make common sense search engine that will query results a user expects to see. To increase the long term support of the app, we want to create an easy to use administrative side that allows a layman to maintain the statutes within our app. Along with the other teams creating similar solutions, we collaborated on making a free and open source scrapper that allows other developers to have all the statutes or some parts of it in a simple JSON file.


# How will it look

PC View

![image](/images/pagemain.jpg)

![image](/images/pageabout.jpg)

Mobile View

![image](/images/picture1.png)

![image](/images/picture2.png)


# Installation

# About Us
The team GoldenEye is one of the participants in [Hawaii Annual Code Challenge](http://hacc.hawaii.gov/) and 
the team is formed with two people.

* [Mark Cummins](https://github.com/markrcummins)
* [Yohan Yang](https://github.com/yohanyang)
