---
layout: post
title: Authentication & Authorization
order: 135
---

One of the first serious issues that are usually not covered by a framework is an authentication. In Rails world people tend to take "well known" Devise lib, integrate it inside the app with `devise :database_authenticatable, :registerable`, and forget about auth. Forget till those awkward moment when you need to customize any tinny aspect of it. From template to auth logic (the latter is harder).

The truth is you can implement auth by your own very fast. Just create users table with login and password fields, encrypt password with smth. like `bcrypt-ruby` gem and store hased password in DB. Plus 3-5 controller actions to handle forms. And you User table is not cluttered with huge amount of the unknown data fields, and you have any idea what for are they (or can you rely on these fields for other business logic).

As a less obtrusive, but still more automated option is to use Sorcery. Or Tyrant gem (with Trailblazer philosophy) that tries to make just a single field entry point into Model.

The less hidden pieces of data flow would be in your app - the easier will it be track error or change the behavior. And in such sensitive part of the app as Authentication - it is very important.

* [Devise](https://github.com/plataformatec/devise)
* [**Sorcery**](https://github.com/NoamB/sorcery)
* [Tyrant](https://github.com/apotonick/tyrant)
* [rodauth](http://rodauth.jeremyevans.net)

When usera are identified inside the app, the second requirement is to distinguish their abilities. The firts idea could be to assign a marker for each user like `role = 'admin'` and check this model attr allover the app. But this is not flexible, when your pernission rules will change, it requires to change all checkpoints. Also permission logic could be quite complicated and it should be encapsulated. Good example of simple Authorization logic organization is Pundit.

Unfortunately I do not know good example of [RBAC](https://en.wikipedia.org/wiki/Role-based_access_control) implementation in Ruby. Something very close to it is [piece](https://github.com/ThoughtWorksStudios/piece) gem. When Roles contain sets of Permissions and all of them could be assigned to User dynamically + business rules (rules should be implemented as a code that check some restrictions).
 
* [**Pundit**](https://github.com/elabs/pundit)
* [CanCanCan](https://github.com/CanCanCommunity/cancancan)
