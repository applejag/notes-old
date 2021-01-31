---
date: 2021-01-30T21:19
tags: 
  - programming/why functional decomposition is bad
  - programming/when functions land in the frontend
---

# Stocks trading service using functional decomposition

By using #[[functional-decomposition]] to design a stocks trading service, in let's
lay a microservice architecture, then you might end up with the following
architectural diagram:

![stocks trading service diagram](static/righting-software-stocks-service-functional-decomposited.png){.ui .centered .large .image}

On the surface from the tainted perspective of someone who's only used to
functional decomposition, this may seem like a nice architecutre.

But let's get real. We've seen these kinds of projects before (not perhaps
strictly stock trading services, but this size of projects). *What's wrong with
this picture?*

## Business logic in the web

Say the user wants to setup rules for trading stocks.

- Buy 10 different stocks, and when the transactions have completed, generate a
  report and mail that to the user and their boss.
  
Where will this logic be placed? In the frontend, *"of course!"*
The frontend becomes the *glue* between the services.

What happens when we want to introduce another frontend? A more touch friendly
web perhaps, a desktop or mobile app, or maybe just a visual frontend to put on
some monitor to give some live feeds.

Because the usage of the services is defined in the frontend, the buissness logic
so to speak, then we have to duplicate that logic when creating another frontend.

The result is that either the team is discouraged from adding another frontend,
or there becomes so many frontends that the dev team finally throws their hands
up in the air and shouts *"We've had it with the frontends! No more frontends!!"*

## Introducing async

When a user clicks "Buy stock", they don't want to sit there and wait until the
stock is bought. That could take minutes, if not hours. They want to click it and
have it queued in the background.

Adding asyncronous processes into your system is never as simple as just adding
the `async` keyword here and there. You have to now consider things like:

- What if the user logs off? Does this task need to be processed on a server?

- How do we handle when tasks are completed out of the order that they were
  queued?
  
- How do we test the logic of race conditions?

Stock trading app is extreme example, because when it fails your customer can
easily get thrown out of buisness.

## Introducing localization

Not talking translations here. We're talking locale-based rules.

What's legal in US stock trading is perhaps not legal in the German stock trading
buissness. This is easy to mess up, and there will be a lot of legal struggles
you have to deal with when you do.

Where does this logic land? In the frontend, *"of course!" (&times;2)*

Maybe you're wiser than that. It should be placed in the microservices.
But where? In the "Buying" service? In the "Trade scheduling" service?

The answer is "all of them". As with the analogy of
[[using-domain-driven-decomposition-to-build-a-house]], *this is a case where your
users wants to eat dinner in the garage.*

To be more clear: This is yet another case where #[[functional-decomposition]]
fails.

## References

- J. Löwy (January 27, 2021), *"Righting Software - System Design"* [Workshop],
  NDC London 2021.
