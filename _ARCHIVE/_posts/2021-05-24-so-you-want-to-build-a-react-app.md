---
layout: single
title:  "Sharing your analyses via the web - what happens when R Shiny and Plotly Dash aren't enough?"
date:   2021-12-31 11:08:01 +0100
categories: react django rest beginners framework
---

So you’ve written all these fabulous analyses, but there’s a problem - no one can use them because they don’t have Python or R on their computer, and they either don’t want to - or can’t - install it. What can you do next?

Well, the usual answer is to head to R Shiny, Plotly Dash or Streamlit. They’re fabulous frameworks that allow you to create a web-based dashboard in less time than you’d think. Then your work can be shared with anyone anywhere in a web browser. No software to install, no packages to wrestle with - from their perspective it just works.

But what happens when you need more than what Shiny, Plotly or Streamlit can offer? In my case, I had an app that seemed to have needs that they couldn’t easily fulfil.

* A way to enter multiple types of data that would be combined to perform calculations
* A way for that data to persist when people left the app and came back -- this data would take a while to enter, so I didn’t want it to disappear
* A user login system where some kinds of data belonged to subsets of users and would be shared between them
* No cost for the developer tools (so no premium versions of Shiny or Dash)

After considering a few options, I settled on seeing what Django - a Python web framework - could do when paired with React - a JavaScript frontend framework.

# Why bother with this instead of Shiny, Dash or Streamlit? Surely you can make it work in those.
There are a lot of very clever people out there managing to make both Shiny and Plotly Dash do a lot of things they weren’t originally designed to do.

However, my experience with trying to break the limits of those tools is that you will spend a lot of time fighting with them. I wanted to create an interface that was as appealing to the user as possible to maximise the chances of them wanting to keep using the tool - I didn’t want to be compromising and constantly using workarounds.

The act of working with Django and React has actually given me some cool ideas for how I could actually solve these problems pretty slickly in Shiny or Dash, but for the overall user experience rather than the developer experience, the Django/React app is probably going to win.

# Why should I avoid going down the Django/React route?
In short, the learning curve is steep.

There’s a lot to get your head around with Django - views, serializers, models. At first, it’s weird stuff that will feel quite different to other Python you’ve written. Shiny, Dash and Streamlit aren’t easy, and they will feel quite different to other R and Python code you’ve written, but for me, Django felt like another level of strangeness.

Then it’s time for React. React, being a JavaScript library, will need you to have some understanding of JavaScript syntax. Coming from Python with zero JavaScript experience, I didn’t find it too bad, but there have been changes to the ways React and JavaScript do things over the years so you might find tutorials and StackOverflow answers particularly tricky to follow if you’re trying to do if they do something you’re not used to. I found this happened a lot more than in Python or R!

Get a bit further in and you might need to start dealing with web sockets, polling, background processes, production servers like gunicorn, production-ready database engines like PostgreSQL. If you’re programming on Windows, you might find some of the things you need are only available on Linux.

Oh, and hosting! Compared to my experience with Shiny, trying to deploy my app to the hosting platform Heroku had me tearing my hair out. You need to be on top of your package management from the beginning.

Overall, it will be a bumpy ride and you have to be prepared to do a lot of debugging. On the plus side, some of the debugging tools are brilliant!

And actually, there really are some things that Shiny and Dash do a lot better than React does. Got a graph that you want to add some pickers to so you can subset the data? That’s going to be easier in Shiny or Dash. Want to get the user to upload a csv file that you manipulate? It’s going to be easier in Shiny and Dash too. The developers of both frameworks have done an incredible job of taking some really complex tasks and making them less painful for those using Shiny and Dash to do. But want to add a drag-n-drop sortable list? A completely custom-styled material UI interface? You’re gonna have a bad time in Shiny and Dash...


# So, tell me more about this Django thing...
Sure thing. Django is a Python based web framework. Web frameworks take away some of the complexity of creating a website by doing a lot of the work behind the scenes. In this case, you write Python code, and out comes a website.

There are two big players in the Python web framework world - Flask and Django. Flask is described as a micro-framework. It is lightweight and only contains the barest bones needed to make things work. However, this does have the benefit of meaning that you can get started with very few lines of code.

Django is described as taking a ‘batteries-included’ approach. It’s more opinionated than Flask - meaning more of the decisions about the way things have to be done have been baked into the framework. This can be a good thing or a bad thing depending on what you want. Getting your ‘hello world’ app up and running takes a lot more code than in Flask, but that complexity can serve you well later down the line.

If you know you want a NoSQL database rather than a SQL one, then you might lean towards Flask as Django is designed around SQL databases and it’s apparently a pain to make it work with NoSQL, though I haven’t looked into this too much so don’t take my word for it!

Django has a brilliant add-on called the Django REST Framework. What this does is help you to make APIs - application programming interfaces - that will play nicely with your React front end, while also being easily viewable and callable for anyone who wants to poke around behind the scenes. An API tends to spit out data in a format called JSON that’s readable to both humans and computers, and React deals with turning that data into something that’s nice for your end user to look at.

## And why should I go for Django or Flask rather than Ruby on Rails or Node.js?
If you’re going ‘what on earth are they?’ Then don’t worry - it doesn’t really matter.

In short, Django and Flask have the massive benefit of being able to use Python’s powerful data science and machine learning features. Heck, you could even pull in some R using r2py if you wanted to.

Basically, while there are certainly some parts of Django that will feel strange, if you’re happy with Python, a lot of it will feel familiar.

## What if I like to work in R rather than Python?
You might like the Plumber package! You can use it to create your API in R instead of Django, and then proceed with the same sort of front end. I’m not covering it properly in this article because I haven’t tried it myself, but there are tutorials out there for doing exactly that.


# Getting started
My personal route began with working through [this full 15 part tutorial series on YouTube](https://www.youtube.com/watch?v=JD-age0BPVo&list=PLzMcBGfZo4-kCLWnGmK0jUBmGLaJxvi4j).

There are a few issues with it, but I found the process of **coding along** invaluable.

The person making the videos makes mistakes too, and this gives you a great insight into the process of debugging and the tools available to you. If you get really stuck, there are often good discussions in the YouTube comments.

One criticism levelled at this series is that it uses class-based components instead of functional components until the last video in the series. Honestly, I think there’s good things to be said for learning to write both.

Some of it feels repetitive, but trust me - it’s worth writing it **all** out every time. You start getting to grips with the steps you need to go through each time you want to add something. When I then started my own project, I had something to refer back to.

This series also makes use of the fabulous material-ui library. This is a Google library of components - things like buttons, select dropdowns, menu bars - that helps you to quickly put together a very smart looking site.

# The next step…

The full series of blog posts that I'm hoping to write over the next few months will walk you through creating a Django and React app from start to finish. We will cover

* Setting up Django and React in your project
* Creating a Github repository to store your app
* Setting up a basic layout
* Navigating between parts of your app
* Using Material UI to quickly bolt together your app
* Creating a layout that works on different-sized screens
* Styling parts of your app with CSS
* Uploading files
* Manually entering data
* Managing app state across pages
* Displaying graphs and tables
* Creating user accounts
* Setting up automatic deployment of your app with the free tier of the Heroku hosting platform
* Creating a Docker container that will allow you to host your app elsewhere

I hope that this article has helped you decide whether React and Django might suit your use case, and I hope to see you back here soon to start working through the app with me.

# Further reading and watching in the meantime
Web development is a very fast-evolving world. You’ll find life easier if you try to stick to tutorials released in the last two years or so!

[Dennis Ivy’s React + Django to-do app](https://www.youtube.com/watch?v=W9BjUoot2Eo)
This is another good tutorial that walks you through setting up Django and React, but with a focus on getting data in and out of the app.

If you’ve got a little money to spare, drop $5 on a monthly subscription to Medium. A lot of good tutorials are behind their paywall - I found them to be easily worth the cost across the time I spent making this app.  
