---
layout: post
title: "EmbjerJS is a more than just Model View Controller"
date: 2014-01-26 07:21:31 -0500
comments: true
categories: EmberJS, Patterns
---

I'm learning EmbjerJS, and it's a great framework. One of the things that I struggled with is that I thought it was a vanilla MVC javascript framework.
I said OK, I know MVC so this is great..then I read a few docs about how Ember view binding works and tried to create a quick prototype. 
I could not get a simple form post working. Why?

## I assumed it was just an MVC framework.

The View (in MVC) is in charge of presentation, is uses the attributes/methods from model to make determinations on how to render the UI. 
Therefore the view reads from the model and sends events/commands to the controller. 
The Controller (in MVC) is in charge of dealing with those commands, it handles requests and input from the user and makes things happen.

In the strict MVC pattern, Controllers are not responsible for is acting as a facade over the model. 

Here's a diagram of how I understand vanilla MVC:

{% img center /images/mvc.png %}

##Back to my problem 
So I created a model object to match the form data, and the view pulled properties from it to show on the form as expected.
I have read about [Ember's view binding](http://emberjs.com/guides/templates/binding-element-attributes/), so after the user edited the form and clicked save, I expected my model to have those attributes automatically reflected on my model from the form, but it wasn't working. 
obvisously I wasn't _getting_ it.

## So I started working through their walkthrough.

After 2 hours I completed their walkthrough and it hit me. This is not just an MVC framework,
**it's a cross between a MVVM framework and a MVP framework.**

Let me explain..

In a [MVVM](http://en.wikipedia.org/wiki/Model_View_ViewModel) (Model-View-ViewModel) The Model object is **not** decorated with any properties that are view specific. (Which is true in EmberJS)
The View does not interact with the Model but instead interacts with a [decorated](http://en.wikipedia.org/wiki/Decorator_pattern) Model called the ViewModel.
These decorations are UI specific to help facilate the view.
In addition to having UI specific fields, The ViewModel object can also constructed in a way that it hides away all the complexities of dealing with UIs where you have multiple models in order to render a view.
Therefore the View just needs to communicate ViewModel and not have to know the relationships between models. 

But there is no concept of ViewModel in EmberJS. So the Controllers play that role.

In [MVP](http://en.wikipedia.org/wiki/Model%E2%80%93view%E2%80%93presenter), (Model-View-Presenter) The presenter does what normally the controller would do in MVC (handle commands from the user). 
It also has the added responsiblity of creating methods that help the presentation (thus presenter).
Methods like hiding/showing logic and handling staleness dependencies of controls can all be handled by the presenter to keep the view simple. 

But there is no concept of a Presenter in EmberJS. So the Controllers play that role.


In EmberJS it's more of a straight line:

{% img center /images/em_mvc.png %}

Note that the default controller implementation proxies 'gets' from the view to the backing model so that it feels more like the vanilla MVC.

Once I was able to understand that, it was clear what my problem was. I expected once the user issued the 'save' command the model would reflect the form data (via Ember's view binding). 
But it was the Controller that received all the form data. I needed to set the data on the model and was able to get a simple form post!

I hope this helps someone understand EmberJS better as it did for me.. 
