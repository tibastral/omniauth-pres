!SLIDE

# Omniauth
## the simplest and most flexible authentication system ever.

!SLIDE

* Thibaut Assus, developer since 2007, notably with ruby + rails [http://github.com/tibastral](http://github.com/tibastral)
* Working for Milesrock, a ruby/rails/node/js consulting company.
* Developing [feedmehq.com](http://www.feedmehq.com)
* I will talk about Omniauth and why it's worth it

!SLIDE

## What is authentication ?

Wikipedia says :

Authentication is the act of confirming the truth of an attribute of a datum or entity. This might involve confirming the identity of a person, tracing the origins of an artifact, ensuring that a product is what its packaging and labeling claims to be, or assuring that a computer program is a trusted one.

!SLIDE

## Authentication == identity ?

No => I can have multiple ways of authentications (digital, password, etc.), but I only have one identity (during the day at least)

!SLIDE

## What is omniauth ?

Omniauth is a simple ruby gem that let your users authenticate through a growing list of webservices, including

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
* and you want to let users have an identity on the website
* and let them authenticate
* and these users already have a facebook/twitter/google/... account.

!SLIDE

### With the omniauth gem, you just have to create an initializer file :

Let's concentrate on facebook right now

@@@ ruby
Rails.application.config.middleware.use OmniAuth::Builder do
  provider :facebook, APP_ID, APP_SECRET
end
@@@

And in your view, you just have to add a link to the auth through facebook
@@@ ruby
link_to "/auth/facebook"
@@@

!SLIDE

Then you just have to handle the callback from facebook through a little controller method:

<script src="https://gist.github.com/961744.js"> </script>

!SLIDE

## Model method :

@@@ ruby
def self.create_with_omniauth(auth)
  create! do |user|
        user.provider = auth["provider"]
        user.uid = auth["uid"]
        user.state = "just_created"
  end
end
@@@

!SLIDE

## Why omniauth ?

* Only domain specific fields in your user/identity model
* Not any other nasty routes to manage in your router
* No more controller code you don't control
* NO MORE NASTY VIEWS YOU HAVE TO STYLE WHEN YOU WANT TO CONCENTRATE ON THE DESIGN OF YOUR APP...

!SLIDE

## Authentication is something you SHOULDN'T worry at the very beginning of an application.

!SLIDE

## It always takes a LONG TIME to figure out the simplest way for users to get on board in a website.

!SLIDE

## Password gems are an always evolving quest and you don't want to get stuck with some encrypted data you didn't encrypted yourself in the database.
If you migrated from restful_authentication to authlogic or clearance to devise, but you think about coming back to authlogic which is now rails 3 compatible, you know what I'm talking about ;)

!SLIDE

## But, you need something to let these users have their personnal space !

How to do it the simplest way possible ?

## KISS ? Yes, better code is no code

Why not beginning an app with omniauth ? and completely get out of the way all that authentication code / sessions / password retrieval you don't want in (at first at least) ?

!SLIDE

All of that is cool, but you also want to do BDD with cucumber / rspec / steak, to test first, and you'll tell me : mocking stuff of the cloud is ALWAYS painful...

!SLIDE

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

And now you just have to add the @omniauth tag to all your scenarios that require omniauth integration
testing.

Omniauth does the shortcut for you, and it's enough for you to test the authentication without headaches.

@@@ cucumber
@omniauth
Scenario: Connecting through facebook
  ...
  When I follow "Facebook auth"
  Then I should be authenticated
  ...
@@@

!SLIDE

## Bonus stuff AKA flexibility

As omniauth is a rack middleware, you can easily store the last location to redirect the guy where he was before clicking on the authentication link.

<script src="https://gist.github.com/961740.js"> </script>

!SLIDE

## Little summary :

Omniauth is :

* SIMPLE and FAST to integrate
* FLEXIBLE, you can do whatever you want with it, because it is
* DECOUPLED from your app
* TESTABLE really easily
* GREAT for prototyping

In one word : AMAZING

!SLIDE

* We use it at http://www.feedmehq.com !
* Our cooks already sold 285 meals in one month WITHOUT basic password authentication !

!SLIDE

# Questions ?

!SLIDE

## Don't hesitate to email me for everything you didn't understand, I'm happy to help !

[thibaut@milesrock.com](mailto:thibaut@milesrock.com)

## If you want to use / fork these slides, help yourself :

[github.com/tibastral/omniauth-pres](http://github.com/tibastral/compass-pres)

!SLIDE

# Credits :

## Presentation done with :

[github.com/nakajima/slidedown](https://github.com/nakajima/slidedown)

Sassly hacked


!SLIDE

# Thank You !
@tibastral
