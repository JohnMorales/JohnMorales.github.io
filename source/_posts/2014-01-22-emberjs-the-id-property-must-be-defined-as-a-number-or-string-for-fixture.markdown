---
layout: post
title: "EmberJS: the id property must be defined as a number or string for fixture"
date: 2014-01-22 18:09:45 -0500
comments: true
categories: EmberJS
---

I'm creating my first application using EmberJS and I recieved the follwoing error: 

`the id property must be defined as a number or string for fixture`.

When I was simply trying to save the model after the user clicks the action. 
I was a little confused by this error, because if you try to define an id property in the model EmberJS yells at you with this message:

`You may not set 'id' as an attribute on your model.`

I've read that it's the store's job to assign the id of the model record. 
It turns out that this is due to using `DS.FixtureAdapter`, instead of the `DS.RESTAdapter`. 

It turns out that the use case for the FixtureAdapter is when you want to build an app and don't want to be concerned with the backend. 
In other words, the RESTAdapter would actually send the restful requests to an endpoint for your crud and verb actions. Where as the FixtureAdapter is a stub.
For example, a front-end developer that is only in charge of the UI and doesn't want to setup the dependencies for the backend.
This way you could mimick the responses that you would get from a real backend. This is why EmberJS is asking for an id: 

### FixtureAdapter is faking a _real_ backend

And a real backend is required to set one.
