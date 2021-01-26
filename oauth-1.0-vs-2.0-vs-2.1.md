---
date: 2021-01-26T19:44
tags: 
---

# OAuth 1.0 vs 2.0 vs 2.1

If you ever need to implement a "Login via Google" feature to your website,
chances are you've heard about OAuth. Or rather, OAuth 2.0 in particular.

There was a time there was an OAuth 1.0, but things changed, people left the
OAuth team, new ideas was put into OAuth, old ideas was removed. Kind of a
natural flow for any project. But it OAuth 2.0 shouldn't maybe be as praised as
it is.

## OAuth 1.0 to 2.0

OAuth 1.0 is complicated. The specification was difficult to implement, and there
were some things left out of the protocol that meant it should only be
implemented by someone who had done the full research and understood what OAuth
suggests, and make informed decisions when implmenting the missing parts.

This was a major blow with OAuth 1.0. In OAuth 2.0, they simplified the protocol
and fleshed it out with a whole suite of samples of how to implement it
correctly. After all, most developers are both inadequately studied in security
to tackle this, and in most cases a developer is tasked with "just add login via
Google". An opinionated and clear protocol is much more secure when the people
who implement it all have regular deadlines.

To simplify, comparing OAuth 1.0 and OAuth 2.0 and roughly be done with the
following points:

- OAuth 1.0 is more secure than OAuth 2.0, some of which is thanks to the
  [[[oauth-1.0s-proof-of-possession]]]

- OAuth 1.0 is more convoluted (less simple), than OAuth 2.0

## OAuth 2.1

Development of OAuth has been at a standstill up until recently. OAuth 2.1 is at
the horizon and promises to resolve some of the issues with OAuth 2.0. It's wise
to study [[[what-oauth-2.1-brings-to-the-table]]] before it lands in our [developers]
hands, so we can properly prepare for this somewhat big change in how
authentication is dealt with over the web.

## References

- Cambell, R. & Franklin, C.. (Hosts). (2021, January 14). *IdentityServer Update
  with Dominick Baier and Brock Allen* (No. 1722) [Audio podcast episode].
  In *.NET Rocks!*. vNext.
