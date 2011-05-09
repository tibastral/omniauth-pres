!SLIDE

# Omniauth
## the simplest and most flexible authentication system ever.

!SLIDE

* Thibaut Assus, developer since 2007, notably with ruby + rails [http://github.com/tibastral](http://github.com/tibastral)
* French here with a business visa
* Working for my company in France named Milesrock, a ruby/rails/node/js consulting
  company.
* Developing [feedmehq.com](http://www.feedmehq.com)
* I will talk about Omniauth and why it's worth it

!SLIDE

## What is omniauth ?

Omniauth is a simple ruby gem that let you authenticate through a growing list of webservices, including

* facebook
* twitter
* linkedin
* github
* foursquare
* ... (47 at this moment !!)

!SLIDE

## How it works ?

### Given

* You have an app
* and you want to let users have a private space
* and let them authenticate to this space through facebook.

With the omniauth gem, you just have to create an initializer file :

@@@ ruby
Rails.application.config.middleware.use OmniAuth::Builder do
  provider :facebook, APP_ID, APP_SECRET
end
@@@

And in my view, a link to the auth through facebook
@@@ ruby
link_to "/auth/facebook"
@@@

!SLIDE

Then you just have to handle the callback from facebook through a little controller method:

<script src="https://gist.github.com/961744.js"> </script>

!SLIDE

## And that's it for session / user / authentication.

* Only domain specific fields in your user model
* Not another nasty router you don't know how to manage in your router
* NO MORE NASTY VIEWS YOU HAVE TO STYLE AT FIRST...

!SLIDE

## Why omniauth ?

!SLIDE

* Authentication is something you SHOULDN'T worry at the very beginning of an application.
* It always takes a LONG TIME to figure out the simplest way for users to get on board in a website.
* Password gems are an always evolving quest and you don't want to get stuck with some encrypted data you didn't encrypted yourself in the database.
* If you migrated from restful_authentication to authlogic or clearance to devise, but you think about coming back to authlogic which is now rails 3 compatible, you know what I'm talking about ;)

!SLIDE

## KISS ? Yes, better code is no code

Why not beginning an app with omniauth ? and completely get out of the way all that authentication code / sessions / password retrieval you don't want in (at first at least) ?

!SLIDE

All of that is cool, but you also want to do BDD with cucumber / rspec / steak, to test first, and you'll tell me : mocking stuff of the cloud is ALWAYS painful...

It is, right, but the smart guys of omniauth made all that nasty work for you guys !

you just have to add a support file to your cucumber config :

@@@ ruby
Before('@omniauth') do
  OmniAuth.config.test_mode = true
end

After('@omniauth') do
  OmniAuth.config.test_mode = false
end
@@@

!SLIDE

And now you just have to add @omniauth to all your scenarios that require omniauth integration
testing.

Omniauth does the shortcut for you, and it's enough for you to test the authentication without headaches.

@@@ cucumber
...
When I follow "Facebook auth"
Then I should be authenticated
...
@@@

!SLIDE

## Bonus stuff

As it is a rack middleware, you can easily store the last location to redirect the guy where he was before clicking on the authentication link.

<script src="https://gist.github.com/961740.js"> </script>

!SLIDE

## Little summary :

Omniauth is :

* SIMPLE and FAST to integrate
* FLEXIBLE, you can do whatever you want with it, because
* DECOUPLED from your app
* TESTABLE really easily
* GREAT for prototyping

!SLIDE

* We use it at http://www.feedmehq.com !
* Our cooks already sold 285 meals in one month WITHOUT basic password authentication !

!SLIDE

# Questions ?

!SLIDE

## Don't hesitate to email me for everything you didn't understand, I'm happy to help !

[thibaut@milesrock.com](mailto:thibaut@milesrock.com)

## If you want to use / fork these slides, help yourself :

[github.com/tibastral/compass-pres](http://github.com/tibastral/compass-pres)

!SLIDE

# Credits :

## Presentation done with :

[github.com/nakajima/slidedown](https://github.com/nakajima/slidedown)

Sassly hacked

[]


!SLIDE

# Thank You !
