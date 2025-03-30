---
layout: single
title:  "A comparison of web frameworks for data analysts in 2021"
date:   2021-08-04 11:30:33 +0100
categories: react django shiny dash dashboards websites frameworks healthcare nhs
---

# Introduction
In the last five or so years, there has been much development of tools that allow a data analyst with no experience of web development to create interactive web apps and dashboards that allow end users to interact with powerful analyses without having to deal with any of the technology that was used to create the underlying analyses, namely Python or R. This means that non-technical end users do not have to contend with installation of programming languages and the numerous pitfalls that often accompany this - if they are even able to obtain permission to attempt such an install - along with package management and version control woes.

This is where R Shiny, Plotly Dash, and some of the other options I will explore in this document come in (henceforth referred to as ‘web apps’). These tools allow R and Python scripts to be packaged into a webpage to be used by the end user. The end user is never exposed to the code and never has to deal with the installation of R or Python. They use it as they would use any other webpage.

However, with multiple options for a developer hoping to share their tools, it is not always simple to decide on the best tool for the job. For an experienced R developer, Shiny is perhaps the natural choice, but Plotly’s Dash or Streamlit are both options for Python developers, and Python web frameworks provide a more flexible option but are more complex to work with and require developers to branch it into Javascript as well. So which option should be chosen?

## The motivating example

This article was written as part of my MSc project where I was attempting to create a web-based version of an Excel model provided by the NHS E/I Demand and Capacity team. The Excel document uses various macros and VBA to provide an interactive tool that can be used by people with limited technical experience to model demand and capacity in emergency departments. However, due to some of the limitations of Excel - discussed below - there was interest in seeing what alternatives to Excel existed for a new version of this tool.
---

# The benefits of Python or R over Excel
But first, is the move to Python or R even necessary? Excel has been the tool of choice for the team I was working with thus far, and has served them well, allowing several models to be created and put into circulation. However, as the models grow in complexity, maintaining and extending them becomes harder. File sizes grow, operations slow down, and tracking the interaction between parts in a program that mostly relies on references to cells rather than named variables becomes difficult. R and Python can help with these issues, as well as a range of others.

## Version control
Unlike in Excel, when you upload a Python or R file to a version control tool like Github, you can see exactly which lines of code have changed between versions. This makes solving issues much easier.
Access to an extensive package library
Within the R and Python ecosystem, extensive packages have been written that will save the developer time. Access to complex time series forecasting packages is also available.

## Code reuse
Many features and patterns are repeated across apps. With Python and R, this can be written once and used across multiple apps with minimal modification.

## Easier bugfixing
In Python and R, bugs can be tracked down using everything from simple print statements to logging modules and breakpoints. The state of variables at different points in the program can be explored, making pinpointing the source of an error much easier.

## Code commenting and code flow
Programming languages always have a character that will be interpreted as beginning a ‘comment’ line, meaning the line will be ignored when the program is executed. This means that writers can do everything from providing extensive documentation for a function, specifying the format inputs must take and outputs will be produced in, to writing single comments in the middle of a function to explain why something is done the way it is. It is easier for new users to get up-to-speed with a well-commented Python or R file than an Excel file, making it easier for code bases to be worked on by multiple people inside or outside an organisation.

## Test development
Automated testing suites like pytest allow unit tests to be written for code. These are small tests that check the output of a function in a given case matches an expected value. These can then be automatically run after each update to a program, before the new version is made visible to users, ensuring breaking changes to the code are caught. This is particularly valuable in situations where the quality of the output absolutely must be assured and mistakes cannot be tolerated - a common situation in healthcare.


However, Excel undoubtedly has some benefits of its own:

## Ease of adoption
While some problems with the existing Excel models have been reported when users are not using the same version of Excel, by and large users will have access to Excel. They will not have to fight with their IT departments for the right to install it - often the case with R and Python - and, to my knowledge, it is generally available to a wide range of people within an organisation, not just analysts. On top of that, Excel proficiency is considered standard for many jobs, so while users may not be overly fond of it at times, they will not find it overwhelmingly intimidating.

Contrast this with R and Python. If you can get it installed, you then have to contend with package versions, cryptic error messages and the intimidation of a new software. If analysts are not all confident to get started with them, we cannot expect to foist them on management and operational colleagues. This is why the packages like Shiny and Plotly Dash have become so popular - a developer can share their analysis in days or weeks, not months.

## Easier control of the layout within a tab
While it is possible to make a well-laid out Shiny or Dash application, and the end result can look highly professional, getting items located in a precise place can prove difficult.

However, web apps do have the benefit of being able to be responsive, changing their layout to best suit a range of screen sizes. More knowledge of the range of devices we may expect users to use the app on may help to decide how useful this is.

---

# Summary
The article that follows goes into depth about the merits of each solution, but the conclusion of it is broadly as follows.

R Shiny, Plotly Dash and Streamlit are all excellent tools that make it possible for people with some experience in R or Python respectively to make web apps in a short space of time. However, they are better suited to performing calculations that require only a handful of inputs, or where the inputs already exist in a consistent format and can be imported in. They were originally designed as ‘dashboarding’ tools and that is what they excel at - allowing users to explore a dataset through visualisations, display of metrics, and drilling down to time periods or subsets of interest.

The demand and capacity team models I was working with all required large amounts of data to be input. For a single user of the model, the inputs may not change a huge amount week to week, making it inefficient to have to reenter this data from scratch regularly. But much of the complexity of these apps comes in non-local storage is required, either to facilitate the sharing of models through the web, to minimize the impact of long-running calculations by avoiding the requirement to run them multiple times, or, as said, to prevent users from having to reenter data. I think this is a very important part of the discussion and I have devoted a full section to talking about this.

Django (a Python web framework) and React (a JavaScript frontend framework) allow for the benefits of Python analytics libraries to be leveraged, as well as providing maximum flexibility to the developer. The app created with this technology combination has the potential to be more feature-rich, user-friendly and extensible than a Shiny, Dash or Streamlit app. These sorts of web apps are very good at allowing users to enter, store and retrieve data. While this is all certainly possible in Shiny or Dash, it is just not done as commonly and you are likely to be fighting against the tools, pushing them outside of what they were originally designed to be best at. That being said, if some sacrifices can be made to the slickness of the user experience - for example, making users save and load data files from the app to their computer rather than having the luxury of their data being stored on a central server - then development may be simplified significantly and allow a confident and motivated analyst with good knowledge of Python or R to do the work and get a good tool out of Shiny or Dash, rather than requiring someone with more web development knowledge. However, for an app that is the best experience for the end user, I do not think the Python backend/JavaScript frontend combination can easily be beaten. Whether the additional time and money required for that option is worthwhile is something to debate further; when it comes to allowing users to then interact with the data they have input, Shiny and Dash make this a lot easier than Django/React, where a lot more must be coded in from scratch.

Creating an app in React and Django is possible for an analyst who is a confident Python programmer. However, the learning curve is steeper than for Shiny (and most likely Dash, though I do not have direct experience of that myself). For Django and React, to upskill a reasonable Python programmer to a sufficient level when their starting point is zero or minimal experience with Django or JavaScript, I would recommend a minimum of six months. It was possible to create a partially working app in less time than this but there were many limitations and, most likely, many non-optimal bits of coding that a more experienced web developer would manage to avoid. However, if knowledge can be pooled through the creation of training material dedicated to the sorts of tools that health data analysts intend to create, bringing in experienced developers to ensure best practice is being followed, then this learning curve may be reduced and the full benefits of the flexibility of Django and React may be unlocked. In a team, what may be of more use overall is to bring in two distinct people - an analyst with Python and/or R skills who can work on the analysi, and a full stack web developer who can work on the database and front end logic, working closely with the analyst to translate the analysis into the format required by the web framework or perhaps enabling the analyst to do much of that work themselves.

I would suggest that the paid versions of R Studio Connect or Plotly Enterprise may provide sufficient benefits to pay their way if deciding to work with Shiny or Dash, and merit further investigation.

Finally, bringing in NHSX earlier in the project so that hosting options and limitations can be discussed at an early stage would be advisable. Even hosting of a prototype came with many unexpected pitfalls and limitations.



---

# Full Report

## Caveat
This document will have some focus on the features I was looking for when creating my own app. I have tried to highlight the benefits and limitations of each software thoroughly so an informed decision can be made about the best platform for each use case - not all may require the more complex and flexible solutions.

## Overview of Options
### R Shiny

R Shiny is a package that allows web apps to be built entirely with R.




Figure 1: Example Shiny App ([LEFT SOURCE](), [RIGHT SOURCE]())


It is typically associated with the creation of dashboards that allow users to explore datasets. More examples can be viewed [here]() and [here]().

With the use of the reticulate package, Python code could also be executed as part of the app. It is also possible to extend Shiny apps with JavaScript.

Both free and paid versions of tools used to develop and host R Shiny are available.

### Plotly Dash

Plotly is an interactive graph plotting library that can be used in both R and Python, and Dash is their offering for building analytic web apps. It can be used in Python, R, or Julia.



Figure 2: Example Dash Apps ([LEFT SOURCE](), [RIGHT SOURCE]())


More examples can be viewed [here]().

Plotly Dash is similar to R Shiny in many ways. It was initially restricted to Python, but in July 2019, it was also made available from within R, though this does not appear to have had much uptake by the community.

Until a couple of years ago, Plotly and Plotly Dash were quite restrictive in terms of licensing, with all data needing to run through Plotly’s servers, but this has now changed.

In Dash, you write HTML-like Python rather than pure HTML or JavaScript, though Plotly state that it is possible for developers with JavaScript experience to bring existing React libraries into the Plotly Dash world.

Both free and paid versions of tools used to develop and host Plotly Dash are available.

### Streamlit
Streamlit is a low-code Python-based app framework.

It has rapidly increased in popularity since its initial release in October 2019, with its popularity now approaching that of Plotly Dash (at least in terms of Github stars - the number of people who have favourited the Github repository) despite its later release.



Figure 3: Example Streamlit Apps ([LEFT SOURCE](), [RIGHT SOURCE]())


More examples can be viewed [here]().

At present, only free tiers exist, with various self-hosted options being supported. There is a beta programme called ‘Streamlit for Teams’ but registration for a spot is required and there is no guarantee that this would remain free in the future.

### Flask
Flask is a Python web micro-framework. It allows a website to be built in Python, assuming very little about what you want the final website to look or act like. It contains only the bare minimum of features required to make a website but is very extensible.   

It can be paired with the Jinja2 HTML templating engine to build the frontend, or with a JavaScript framework like React, Angular or Vue.js.

### Django
Django is another Python web framework. However, unlike Flask, it describes itself as taking a ‘batteries included’ approach. More features are included as standard, such as authentication and database schema migrations, meaning that it is less flexible in some ways because these decisions have been somewhat made but, especially for a beginner web developer, this can speed things up. While Flask is much simpler for a ‘hello world’ level of application, once you pass the initial hurdle of learning what all the different parts of a Django application do, it becomes a good framework to use.
The frontend can be handled with Django’s templating engine or, as with Flask, it can be paired with a JavaScript framework like React, Angular or Vue.js.

### Python Framework with React frontend
Many modern apps make use of JavaScript libraries to help build their user interfaces. JavaScript becomes necessary as soon as your app requires any level of interactivity between the user and the app past simple action like submitting a form, or if you wish for information to update without a full page reload being necessary. If you wish to make a different graph appear depending on the selection made from a dropdown without reloading the entire page, for example, JavaScript becomes necessary.

React, Vue.js and Angular are all popular frontend frameworks. The popularity of React and Vue.js are similar according to the 2020 Stack Overflow survey, with Angular being further down the list. In my app (and, as such, the rest of this document) I made the decision to focus on React because of its popularity - I suspected that finding training materials and support would be easier - but Vue.js looks very promising as well and is sometimes described as being easier for beginners as it makes use of a mixture of HTML templates and JavaScript, whereas React uses JavaScript alone.

Of Flask and Django, Django is well suited to working with front ends. It has a highly developed framework-within-a-framework called the Django REST framework. A rest API provides a consistent way of passing information from the Django backend to a frontend. The React frontend can deal with all of the display and interactivity while the Django backend performs calculations and returns the required data to the frontend through calls to specific URLs (API endpoints). These endpoints are highly flexible and easy to create. When loading a page or performing an interactive action, you can specify an endpoint to call, whether this is for getting data to display, updating what is already displayed, or making updates to your database - all of it is controlled through requests to API endpoints. It becomes a very intuitive and well-compartmentalised way to work.


## Pricing

### R Shiny
Cloud deployment on shinyapps.io. Tiers ranging from free to $299 a month. $99 month option needed to include user accounts.


Shiny Server allows apps to be hosted locally. This option is open source and free to use, but lacks features like user authentication (except through third-party libraries)


RStudio connect is the most fully-featured option and would allow powerful sharing of apps with end users. A brief guide to its capabilities is available here. However, it is expensive, at nearly $15,000 / year for 20 users. There does appear to be a discount available to the NHS (see this thread in the NHS R Slack group - chris.beeley@nottshc.nhs.uk appears to be the person to talk to about this) but I am not sure how large this is, or whether it is something that NHS England are perhaps already utilising.


A good comparison of the options are given [here]() by the Shiny team.


ShinyProxy is a free alternative to the paid RStudio options, offering many similar features and benefits while remaining open source.

### Plotly Dash
Open source version has basic features. Could be deployed on Heroku (which does have a free tier) or similar, or an internally managed server.


Enterprise licence is $50,000 a year, allowing 5 developers, but opens up options like background jobs for long-running tasks, authentication of users, a dedicated server for hosting, and enterprise IT integration.

### Streamlit
Streamlit itself is currently free
There is a beta program for 'Streamlit for teams’ which provides additional benefits like single sign-on, making repositories private, and secure connections to private data, but there is no information on their page about whether they would keep this tier free in the future, and I think it is likely that they will not.
Like Dash apps, Streamlit apps can be deployed on services like Heroku, which have free tiers as well as paid tiers..

### Django, Flask and React
The frameworks themselves are completely free to use
Some packages are paid, though the vast majority are free. The main examples of paid packages I came across concerned the creation of editable spreadsheet-like tables, though many had free tiers available that would suffice.
Hosting will generally incur costs, whether this is through maintaining an on-site server or deploying to a service like Heroku (although a free tier is available).





## Deployment Options

From the limited information I have gathered, Heroku is accepted for prototypes that will not make use of real patient data. For deployed apps, it would appear that the NHS has mostly chosen to work with Microsoft, and their Azure service.

Instructions for deploying a Django web app with a PostgreSQL database are provided by Microsoft here.

There also appears to be some promising content with regards to Azure blueprints for ensuring compliance with storage of NHS data. See here and here.

## The ED App - What was the Feature Set?
For the ED app, there were several key factors and features that needed to be taken into account.

Historical data needs to be imported
However, this historical data is not being obtained from identical sources across different trusts, so there is a risk that the data obtained will be slightly different across trusts.
Ideally we want this import process to be as seamless and user-friendly as possible.
There is too much historical data to re-enter it each time the app is loaded


Shift types, role types and rotas need to be created and edited
Users need to be able to enter these fairly complex data types.
They are dependent on some aspects of the historical data, so fields will need to be dynamically generated based on this data (e.g. role types need to reference the streams present in the daata)
These are data types that will differ between users - or, more likely, between organisations, which may contain multiple users - but may well remain consistent or very similar between runs of the model (e.g. if using the model weekly to check new rotas). Therefore it would be frustrating for users to have to enter these every time they load the tool.

Therefore we have something that is quite different to your standard Shiny or Dash app. In those tools, when we are entering data to perform a calculation, it is generally a one-off calculation or one with inputs that do not take too long to enter.





Figure 4: Example calculation apps ([LEFT SOURCE](), [RIGHT SOURCE]())



There were three main approaches I could see:
Have users enter their rotas into a template - most likely in Excel - and then upload this template to the app. The template would have to load in the data again when they refreshed the app or exited and returned to it.
With regards to updating data (e.g. trying out a different rota), either
users would have to make changes in the template and reupload
users would be able to make minor changes to the data once it was loaded in


Maintain session-based storage, but allow input directly into the session through packages which provide an Excel-like interface.


Allow input of data through a range of interfaces and store this data elsewhere (e.g. in a SQL database), allowing it to be accessed across multiple sessions in the app.

Option 2, and to a lesser extent option 1, was very reliant on a user’s data to be stored in the browser long enough for the user to not be frustrated by the experience. If they logged out to go for lunch, for example, and returned to find the data they entered had gone because of the app timing out (something that can happen with Shiny apps), then any goodwill or interest in the app could rapidly evaporate.

I also felt there could be issues with this approach when trying to implement user logons and sharing of apps. For example, within a normal Shiny dashboard, a user logon is useful for preventing access to the app or subsets of data that the user should not have access to. However, without some sort of persistent storage, or an external dataset that is being pulled from, then this is of limited use.

### Shiny
Within Shiny, option such as ExcelR and rhandsontable, exist. This would allow option 2 to be achieved.

There are also options for persistent data storage - that is, data which will exist across multiple sessions - within Shiny, detailed in this article from RStudio. Dean Attali also expands on the options available here. Finally, this article goes into even more detail about creating a CRUD app in Shiny, and the company who wrote the blog post - Tychobra - have implemented CRUD in multiple Shiny apps (see e.g the T3 app here). However, overall information about entering data into Shiny seems to be quite limited, which could make it difficult to find help if problems are encountered.

### Plotly Dash
In Dash’s documentation, there is an entry about creating an editable datatable. The ‘Uploading Data’ section gives an example of how a user could upload data and then lightly modify some of it - this could perhaps work nicely with users uploading a template containing their role and shift types and wanting to slightly modify some aspect of this.

Overall the functionality in Plotly looks fairly promising and would definitely be worth exploring further.

An example CRUD app written in Plotly Dash is available in this Github repository, with a Youtube tutorial available here.

Django or Flask with React
Django uses ORM (object to relational mapping) that makes storing data simpler. It allows data to be received from the frontend and then easily converted between manipulable Python objects and stored SQL database entries. In short, CRUD operations are relatively simple from within Django.

The React frontend is very flexible for data entry. A large number of editable JavaScript tables exist - I chose AG-Grid due to its very good free offering, but there were many other good candidates if a particular feature of interest was not available in AG-Grid. Due to time constraints I did not end up making the data in the tables editable, opting to only allow users to delete and reenter incorrect shift types, role types and rota entries, but I am confident that editable tables would be possible. However, it is also questionable whether they are the right choice when so many other options exist for data entry within React. For example, a repeatable pattern I chose to use was the opening of a pop-up box that allowed users to enter the relevant data and submit it to create the entry when this was done.





Figure 5: Data entry modal for shift types




Figure 6: Display of created shift types


From the table that displays created shift types it is currently possible to delete shift types. It would be possible to add an edit button that would reopen the modal, populate it with the data for the shift that was chosen to edit, and then allow modified data to be saved. This may be more intuitive for users than altering the values in the table.
A proposed middle ground
R and Python make use of the tbl and the dataframe respectively. Both may also make use of lists, and Python makes use of dictionaries, which can be stored as json files.

An option within the app could be made available to export a zip file containing a mix of json and Feather files. The app would then expect the same zip file to be uploaded when loading, and would load the relevant files into memory, allowing them to be used as if they had been generated within the new user session.

While this does not have the full flexibility and power that is possible with a React/Django app, it does have some benefits:
Source of truth
Downloads can be a snapshot at a given time, allowing users to keep historical models for referring to at a later date
Responsibility for storage shifted back to the user
Risk of data leaks is minimized as there is not indefinite storage of data in a centralised location
Repetition of long-running calculations is minimized
Generating a Prophet model takes 30 seconds - 1 minute per stream of data. While this isn’t a huge amount of time for most datasets, it can lead to a poor user experience, especially with Shiny which has a rather aggressive time-out policy by default (and which is sometimes difficult to overcome). By storing the outputs of these calculations (models as jsons, forecasts as Feather files), they only have to be run once for a given dataset.
Portability and extensibility
R has the strongest foothold in the NHS analyst community at present. Feather is a storage format designed to work equally well in R and Python, allowing users to load forecasts and other dataframes to further dig into as part of their own workflow. Dictionaries could be loaded in using the Reticulate package, and json files could be loaded as well. Overall, maximum flexibility is given to the user to make use of the data as they see fit. Even Plotly figures can be saved to json, potentially allowing users to import them directly into an R markdown report.

One thing to keep in mind with all model storage options is that any future updates have to be compatible with models people have stored already. Keeping versions the same for e.g. Pandas and Feather is important to maintain compatibility - or at least keeping a store of old models to test compatibility with before upgrading packages in production - is likely a good habit to get into. However, I am mostly speaking from experience of compatibility issues encountered with Pandas and Pickle, which is a similar concept but a different package, so whether this is something the developers of the Feather package attempt to resolve, I don’t know. Furthermore, if you move to requiring additional inputs in later versions of the app, you may once again run into issues if a user attempts to upload an older file that does not contain these.

Figure 7: Current storage in Django/React app

Figure 8: Proposed storage for R Shiny or Plotly Dash

## Other pros and cons of each approach

### R Shiny

I initially had expected that I would use Shiny for my MSc project, so I collated a range of resources relating to creating production-grade, scalable Shiny apps and watched several talks on good practice and workarounds for the features I envisaged needing. This collection of resources can be seen here.

#### Positive of R Shiny
##### NHS Analyst Community Support
Within the NHS, R has somewhat been adopted by the analyst community as the preferred language for analysis. The NHS-R community is larger and more developed than the equivalent NHS Python community. This is a key consideration with regards to allowing people to extend and maintain the software.

NHS R have also begun to offer beginner Shiny training, increasing the number of analysts in the community who will be able to work specifically on the Shiny elements rather than just the R code performing the calculations.

##### Very active development community
Shiny has exploded in popularity in the last few years, and with that comes an ever-increasing range of packages and resources for making bigger and better Shiny apps. This appears to show no signs of slowing down. The RStudio conference includes many talks on Shiny, and partners like Appsilon, whose main purpose as a company is making Shiny apps, create packages to help them with their work and then often release them to the community for free.

##### Focus of libraries on statistical packages
R was originally the language of statisticians, and for a long time was ahead of Python in its general support for data manipulation.

However, with Plotly Dash incorporating R support in 2019, R Shiny has lost this edge somewhat, although it seems that Dash’s support for R is not as well developed as its Python offering (going by community adoption, at least).

#### Issues
##### Single Threading
When running Shiny apps without the use of Shiny Connect or ShinyProxy, only a single operation can be performed at any one time, regardless of which user requested this operation. Therefore, while each user is experiencing an isolated session from their point of view, they may end up waiting for an extended period of time for the

This can be avoided by using one of Shiny Connect or ShinyProxy. For example, ShinyProxy dockerizes apps, so each user gets a new ‘container’, meaning that one user’s requests will not leave another user waiting.

##### Inactivity Timeout
One irritating limitation I have experienced with R Shiny is the timeout due to inactivity. If a user does not interact with the webpage for a certain length of time then the user’s session is ended. The same is true if they, for example, put their computer to sleep. This was a particular problem in a previous organisation I worked for: people were frequently taking laptops to and from meetings, putting them to sleep by closing them when doing so. It does appear possible to tweak the amount of time that passes before the app becomes idle, but potentially only for paid versions of R Shiny.

##### Codebase organisation
Organising code within a Shiny app can become quite an issue. In a previous app, in an attempt to modularise code as much as possible, I ran into some strange issues associated with loading in of modules. Since that time, some improvements have apparently been made, with the introduction of ‘Shiny modules’ in 2020 being a positive step.

The ‘golem’ package is also aimed at improving the quality of Shiny codebases, purporting to help developers make ‘a stable, easy-to-maintain and robust production web application with R’. This works in conjunction with Shiny modules. The freely-available book ‘Engineering Shiny’ covers the use of the Golem package in detail. Existing Shiny apps can be refactored to fit into the Golem framework, but it is apparently best to build them from the beginning with the framework where possible.

##### Garbage Collection
In my previous role, I created a Shiny which, due to data protection issues, had to request a large table and load it entirely into memory rather than being able to use any intermediate storage. This would largely have been fine if R had efficiently released memory at the end of user sessions. I was never able to completely resolve whether it was a memory leak that was causing the issue or some other issue with R Shiny, but overall, even running rm() on objects when the app closed, along with use of the gc() function, which stands for ‘garbage collection’ and should make R release memory back to the operating system, it never seemed to fully release all memory and led to the server the app was running on eventually locking up entirely. This could be somewhat ameliorated by using docker containers or similar, ensuring that only the app itself would break rather than causing issues with the whole server - important if multiple apps are running on a single server. The tables used in the ED app may not be big enough to run into this problem anyway, even at hourly or individual resolution for several years.

##### Debugging
RStudio themselves admit that debugging a Shiny can be challenging. There are limitations on where breakpoints can be set, though the browser() function serves a similar purpose and does work more widely. They do have some clever tools such as showcase mode, which highlights the running code as it executes. It seems that improvements have been made to Shiny debugging since my last experience with it, so my concern about this is not as great as it once was.

#### Extensions to be aware of

##### ShinyProxy
Shinyproxy is an unofficial option but is well thought of. It describes itself as being of use when ‘you need enterprise features but want to stay with open source’ and ‘you want to get all benefits offered by Docker-based technology’.

Docker ‘containers’ mean that each user of the app will get a different container, meaning each session is totally isolated from others. Long-running calculations will not impact other users, making the app feel more responsive.  

It also includes authentication and authorisation (user account) functionality.

##### ShinyAuthr
If not using ShinyProxy or a paid RStudio option, ShinyAuthr is a reasonable package for adding in user authentication.

##### Golem
As mentioned above, Golem is an “opinionated framework for building production-grade shiny applications”. The authors of this package have also authored a free book, ‘Engineering Production-Grade Shiny apps’.

##### Plumber
Plumber allows the creation of APIs (application programming interfaces) with minimal additional code. This could be a good way for advanced users to extend the application, allowing them to perform additional calculations or create additional graphs and retrieve the output without having to create additional frontend components.

##### ShinyTest
Shinytest is a package for running automated testing in Shiny. This can help ensure that existing features are not broken when making changes to your code.

##### ShinyLoadTest
The ShinyLoadTest package is designed for simulating concurrent users of the app, allowing you to determine where problematic bottlenecks and slowdowns are occurring.

### Plotly Dash

#### Claimed development speed
Plotly variously claim that development speed can be 2 times to 10 times faster with Dash than with a full-stack team, and also 3.75 to 21 times cheaper.


Figure 9: Comparison of development processes (SOURCE)

They fully detail their claims in the white paper available [here]().

These claims are likely to have some merit, though are likely to be overstated somewhat, particularly given that developer salaries in the UK are substantially lower than in the US (source, source). However, their main point - that you can produce stable, scalable apps relatively quickly with fewer people - certainly rings true to me, though very similar benefits are likely possible with Shiny or Streamlit, provided the features required of the app are not too far outside what these tools are designed for.

#### Limitations

##### State persistence
While Plotly apparently uses a Redux state store behind the scenes, it is currently not possible to access it from within the app. Therefore, reloading the webpage will lead to the stored state being lost.

Some components now have the notion of ‘persistence’, allowing things to be saved, but this is not true of all components and relies on component makers adding this feature in.

##### Callback limitations
Dash makes use of a notion of ‘callbacks’ to update the app when an input or output changes. In short, there are some limitations on what these callbacks can do which can lead to a frustrating experience for developers in more complex apps (anecdotally). Having not used Dash myself, I would not like to comment on this too much, but it would be worth investigating further before committing to Dash.

#### Streamlit
My overall impression of Streamlit when first looking at it was that it was designed for apps simpler than what we wanted to create.

However, I do think it’s worth keeping an eye on it as it continues to mature and develop. Even in the time I’ve been writing the app, changes have happened to the framework which would give me pause before discounting it in the future.

However, this quote is a succinct summary of the current state of the two.
“... if you are looking to build an enterprise-level app, if performance is of paramount importance, if you are looking to style the app to your liking (e.g. a corporate style guide), Dash is the way to go.” - JP Hwang, Plotly Dash vs Streamlit

Overall, because of its immaturity I have not delved into it too much.

##### Session State
At the point I was deciding on a framework, Streamlit had no official support for session state, though it was apparently possible with workarounds. This changed on 7/7/21, with the release of an official way of including states. This is potentially a gamechanger for Streamlit as an option, as it allows easy use of pagination - so no longer limiting the app to a single page - and many other things.  

##### Rerunning when any input changes
By default, any interaction with a widget causes the app to rerun. This initially struck me as a very limiting feature. However, it appears there is a way to batch interactions into forms, so this should not be a problem.

## Python Web Frameworks: Flask vs Django
“A web framework is a code library that makes web development faster and easier by providing common patterns for building reliable, scalable and maintainable web applications. After the early 2000s, professional web development projects always use an existing web framework except in very unusual situations.” -  Full Stack Python

It is possible to have the back end of your website written in something other than Python - for example, RubyOnRails, Angular or next.js - but as we were inevitably going to want to make use of some of the powerful data science features that are usable with Python, staying within the Python ecosystem seemed to make the most sense as far as I can see.

## APIs
API stands for application programming interface, and basically allows urls to act as a way to interact output data in a format that can be understood by both humans and machines. API endpoints can also be used to submit data from your frontend or trigger other actions.

Django can be used for both the backend and frontend of your website, but an alternative is using the Django Rest Framework to build a web API and pair this with a JavaScript frontend.

### Comparisons
My personal preference is for Django over Flask unless the website is very simple.

I found Django simpler to use once I understood the way it expects urls, serializers and views to be used together in conjunction with the Django Rest Framework.

Flask is a lightweight web framework, whereas Django is often described as taking a ‘batteries-included’ philosophy. Many decisions are already made for you, speeding up the development process. It is stable, with an active community and continued development, and is used in major projects around the world, including Instagram and Spotify. While there are good tutorials for Flask, the Django documentation is regarded as some of the best that exists.

Furthermore, the API created by the Django REST framework is browsable, making it easier to use in many ways than the Flask equivalent.

Overall, either option will work and there are pros and cons to both, but I would lean towards Django.

## Frontends
When I previously used Flask, I ran into issues with what I thought would be a very simple task. I had a long-running Python script, and I wanted to update the user on the progress of the script so they would wait for it to complete rather than assuming the page was broken. However, I was then catapulted into the world of websockets, JavaScript and ajax. It was confusing and demotivating.

Since then, I learned a little more about frontends, and in particular I started hearing about ‘React’ and single-page applications (SPAs).

### Single Page Applications (SPAs)
A single-page application is perhaps a slightly confusing name. What it isn’t is an app that only has a single page in the way you might be expecting. You can still have multiple URLs that you move between, sidebar navigation, and other features that you would expect in a normal website. However, in a SPA, when navigating around, you don’t reload the entire page when going to a new part of the website. Instead, the webpage makes requests to the server and dynamically updates the relevant parts of the page. This makes the website feel snappy and modern to use as you’re not experiencing frequent full reloads.

While there are a lot of arguments for and against SPAs, many of them did not feel particularly relevant for this situation (for example, they have poor search engine optimisation).

#### What drew me to React?
After some initial learning curve, I found React to be a very logical framework to work with. This was made even better after encountering the easy-peasy wrapper for Redux state management, making it much easier to pass state between different parts of the app.

#### The bad of React
React experienced something of a shift in 2018 with the introduction of React hooks. Previously, any complex components - those that needed to have a concept of a state - made use of Class-based components. However, the introduction of hooks allowed functional-based components, which are generally easier and cleaner to write, to be as fully-featured as class components. However, this means that tutorials, documentation and StackOverflow answers use a real mix of class and functional components and this can be very confusing when you are just starting out. When you are more confident, switching between the two is relatively simple, but it is useful to know how to write both so you can make use of all of the resources available to you, which does raise the barrier to entry.

Furthermore, something which isn’t unique to React but is common to any frontend framework is the need to understand and write JavaScript. I do think this is a valuable skill for an R or Python developer who is interested in web app development because both Shiny and Dash can be extended with JavaScript code, the latter specifically with React too. The syntax is more similar to Python than to R. JavaScript does suffer from a similar problem to React, with the release of the ES6 version of JavaScript in 2015 adding useful new features but adding more complexity. Defining variables is a strange thing to get used to if coming from R or Python, with let, const, var and their differences to get your head around. In short, it takes time and will mean there is an additional time cost to creating your first React app over a Shiny app as you are having to learn multiple things - JavaScript, React, and Django or Flask - at once. Whether that additional hassle is worthwhile does depend on the app. I think overall these JavaScript frameworks significantly reduce the difficulty of creating interactive apps so for the sorts of tools you are aiming to create, they are worth making use of.

## MaterialUI

MaterialUI is a React component library that is designed to make it quicker to build the frontend of a React app. It is an open-source project and follows Google’s Material Design guidelines. In short, it provides user interface elements like buttons, dropdown option pickers, menu bars, navigation bars, and more.

Material Design is a design ‘language’, developed by Google, that will be recognisable to many people who have used a website, in particular something from the Google stable, and also will be very familiar to the users of Android devices.


There are several benefits to using Material Design:
Users experienced reduced cognitive load because of the familiarity of the app, thus increasing the chances of them continuing to use the app.
Arguably, users subconsciously trust your app because they associate the app with the Google framework.
There are also benefits for both developer experience (DX) and speed of development. It means developers do not have to reinvent the wheel when creating common UI elements, making their lives easier and saving time.

Material UI makes use of a clever grid system. A material UI page is made up of 12 invisible columns. If you wanted to set up two elements to display side-by-side, you would specify each element to take up 6 of these column units using the syntax xs={6}. However, if you wanted the two elements to display above each other on a smaller screen, you could use the syntax xs={12} md={6}. This tells the app that on a screen above the predefined ‘medium’ screen size in terms of number of pixels, it should use the ‘md’ setting, and on anything smaller, it should use the ‘xs’ setting. There are predefined screen sizes that are considered extra large, large, medium, small and extra small (with the option to add custom sizes as well), and you can choose to set from one to all of them, making adding support for multiple screen sizes quick and easy.


Figure 10: Material UI Grid example (SOURCE)


## SQL vs NoSQL
When storing data that will persist between sessions, it becomes necessary to use a database (unless forcing the user to store their data by making them download/upload it to and from their own machine, as discussed earlier in this document). The main choice to make with regards to databases is between SQL and NoSQL.

The main difference between SQL and NoSQL is that SQL is relational (tabular) and NoSQL is non-relational.

All data in SQL is stored in tables, and these tables may have links between them. For example, a patient could be treated in a hospital, and their record would be linked to the ‘hospital’ table to get information about the hospital, which could then be linked to a ‘trust’ table to get information about the trust. Each row in the respective tables relates to one entity: one patient, one hospital, one trust. This minimizes the duplication of data. The tables, and the columns they contain, are predefined/pre-planned before being populated. This is called a database schema.

In a NoSQL database, there is no predefined schema. If you later decide you need to store additional data, you can do this without disrupting previous data.

The general consensus I found was that if you’re not absolutely sure you will benefit from a NoSQL database, it is safer to go with SQL. However, if I were to

A good explanation of relational vs non-relational databases can be found [here](), and a good explanation of NoSQL can be found [here]().

### Frameworks and NoSQL support
Officially, Django does not support the use of NoSQL databases.

It is possible through some forks of Django - for example, django-nonrel - but using forks of the project may lead to issues down the line (for example, the fork may cease to be updated or not be updated quickly after updates are made to the main version of Django) and should be avoided if not entirely necessary.

It is much easier to use NoSQL with Flask than with Django.
Pros and cons of each

#### SQL

##### Pros

* Developers and analysts are more likely to be familiar with working with it
* Works out of the box with Django

##### Cons
* Can reach a ceiling of scalability due to vertical scaling - so once you max out your CPU/RAM etc. then there’s not very far you can go
* More difficult to change the schema once data exists than in a NoSQL database.


#### No SQL

##### Pros
* Can deal better with larger datasets due to being horizontally scalable
* Easy to change the kind of data you are storing as your needs develop
* Copes well with non-tabular data
* Works well when not all entries will contain the same data (saving you from having lots of empty entries)

##### Cons
* Doesn’t work natively with Django
* Not ACID compliant (explanation here)





### Flavours of SQL
SQLite is used as a development server. When working with Django, it allows for rapid prototyping without needing to set a separate server running. However, it does not allow multiple users attempting to read from it or write to it at once, so is generally not regarded as suitable for use once an app enters production. However, it may be sufficient if an app is not receiving much traffic, so may suffice. However, if trying to use SQLite in conjunction with Heroku, you will be unable to use SQLite as files - including the database file - do not persist when the dyno resets.

MySQL and PostgreSQL would both be suitable production-ready databases.

### Conclusion on databases
Given that the models already exist, we are quite clear on what data needs to be stored, which makes SQL schemas not too difficult to define. That being said, if it weren’t for Django’s lack of native support for NoSQL, I would be very tempted to try a NoSQL database out as I think it would provide more flexibility. The debate about the benefits of each seems to continue raging in the development community - in reality, you are likely to be able to make a functioning app regardless of which you choose.

## Miscellaneous comments

### The difficulty of creating a foolproof interface
One of the big difficulties I encountered was creating a user interface that would handle errors gracefully and not leave users stuck. It is difficult to think of every possibility of how a user may interact with the app and test all of them. Testing with a range of real users will help to iron out many of these problems.

Because historical data processing has to be handled in the background, I found that it was possible for tasks to become out of sync, with Prophet models attempting to be generated for datasets that had already been deleted, for example, or trying to generate a new model from a request that was triggered and put to sleep due to failing, only to return after models had successfully been generated and then attempt to regenerate the models again. Trying to write logic to make sure that users don’t get stuck because of this was tricky but not something I’m sure it’s easy to avoid.


## Further Reading

### Comparisons of Frameworks
[Shiny vs Dash - R King Data - June 2019]()
[Streamlit vs Dash - Medium - July 2020]()
[Python and Dash vs. R and Shiny - Appsilon - December 2020]()
[Streamlit vs. Dash vs. Shiny vs. Voila vs. Flask vs. Jupyter - Medium - October 2020]()
[Gradio vs Streamlit vs Dash vs Flask - Medium - February 2021]()
[Shiny vs Dash vs Streamlit vs Django/Flask - Reddit - April 2021]()

### Rest APIs
[Creating a RESTful API: Django REST Framework vs. Flask]()


### Resources for Flask and Django
[Full Stack Python - Introduction to full-stack development with Django, Flask and other frameworks]()

[Free Tutorial Series for Django & React (making use of material UI)]()

[Another free tutorial series for Django & React (focus on creating, updating and deleting items from databases)]()

[Miguel Grinberg’s Flask Mega-tutorial.]() This link is to the free blog version of the tutorial, which is a good starting point. However, a better option would be his newly updated (as of July 2021) course. However, note that this all is pure Flask with a hint of Javascript, not Flask with a JavaScript frontend library like React/Vue.js.

### Resources for Shiny
[Developing a complex R Shiny app – the good, the bad and the ugly]()

[My Trello board of Shiny resources]()

### Design Principles
[Reducing cognitive load]()


### SQL and NoSQL
[IBM explains SQL vs NoSQL]()
