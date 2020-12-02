---
layout: post
title:      "Again: a Sinatra Web App"
date:       2020-12-02 14:45:39 -0500
permalink:  again_a_sinatra_web_app
---


The year 2020 has been such a crazy experience for everyone - learning to code and learning to cope has been the focus for much of mine. This year, I started my coding journey, I started a new job, I built my first CLI app, I experienced my first "lockdown", I transitioned to working from home, and then my husband got a work assignment halfway across the country - so we relocated to a new home in a new town (luckily safely and soundly). And now I can add building a web app to my list!

Being in a completely new place was disorienting at first but what I found to be one of the most helpful ways to adjust was creating new habits and routines. One of the best ways to keep track of my habits has been using a habit tracker.

For my project, I decided to build a simple habit tracker. I chose the adverb *again* as the app's name for both its definition and its phonetic spelling *a•gain* - a habit is something you do repeatedly until it becomes a gain. There is a lot of research published for how long it takes a habit to form and it is something I plan to keep track of as I work to improve my app's functionality.

**Again** is a web app that allows a user to sign up and create an account. Once an account is created, a user can log in and out with their chosen username and password. Their personal account gives them options to create habits with a name, date, and description; edit their previously created habits; or delete their previously created habits. It can be accessed by downloading the gem and running the program locally through localhost:9393. 

Check out the demo video here for detailed instructions: [Again: Habit Tracker Demo](https://youtu.be/g8Jnh7TSt50)

The code behind the app works with ActiveRecord, (which stores all the information the app uses in a database), and Sinatra (which uses that stored information and turns it into a functional web application). The app has two model classes: Habits and Users. A Habit belongs to a User, and a User has many Habits. The majority of its functionality is then handled by permissions and logic built into the views and controllers. Getting each of these pieces to communicate with each other correctly was challenging at first but ultimately became the most fun - especially watching it all happen in realtime using the shotgun gem. 

My next goal is to figure out how to save a user's progress - currently there are checkboxes as placeholders to represent the days of the week to allow a user to check off when they have completed a habit. I am continuing research to decide whether to stick with the weekly setup, create a simple calendar setup, or add in numbered boxes that represent a set number of days (i.e. 21 or 66 days - from research data on habit forming).
