---
layout: post
title:      "Sinatra MVC App: Adventure Bucket"
date:       2020-04-20 22:38:10 +0000
permalink:  sinatra_mvc_app_adventure_bucket
---


**Adventure Bucket List is an app that lets you keep track of all the adventures you want to go on.**

*Breakdown:*
# M
To create this app, I first started with the **Models**. 

1. User
2. Destination
3. Adventure

These models are responsible for connecting eachother using relationship associations: *has_many* and *belongs_to*.

* Users *"has_many"* Destinations.
* Destinations *"belongs_to"* Users and *"has_many"* Adventures
* Adventures *"belongs_to"* Destinations 


# V
The **Views** are responsible for displaying the data pulled from *Models*.

These views were written using HTML and Ruby. The *.erb* extension allows for the use of both languages in the same file.


## C
Last but not least, we have the **Controllers**.

The **Controllers** play a very important role. They are the "facilitators". The "workers". 

The *Application Controller* is responsible for setting some basic rules like which folder to find my views, to enable sessions - those are used to keep track on which user is currently logged in and to secure the session. The controllers are broken down into 3 for simplicity and organization. 

The *User Controller* creates a new user. It can also log-in and delete a user if requested. 

The *Destination Controller* creates a new destination along with its attributes that *belongs_to* a **User** and *has_many* **Adventures**.

This project has taught me so much! Now, I can expand on my knowledge and improve my application. Stay tuned for the updated version!

