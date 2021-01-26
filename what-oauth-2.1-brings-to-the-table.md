---
date: 2021-01-26T20:12
tags: 
  - natural lang/advanced english words
  - security/securing authentication
  - security/managing login
  - security/oauth
---

# What OAuth 2.1 brings to the table

OAuth 1.0 was considered a highly secure protocol, but too convoluted so that
very few actually implemented it correctly, and some not at all.

OAuth 2.0 had removed some of the security features that OAuth 1.0 had in an
effort of making it simpler to implement (and it succeeded with that).

OAuth 2.1 is not as big of a jump from OAuth 2.0, as the versioning suggests,
but they still dropped some features and added in new ones to make it more like
OAuth 1.0.

## The wording

The sophisticated language and nomenclature used in OAuth 1.0 was unbearable for
the average developer. OAuth 2.0 did a much better job with its collection of
implementation samples, but it still had quite a learning curve in its language.

OAuth 2.1 is promised to use a more common wording scheme to better allow
non-native English speakers to have an easier time understanding what the
protocol actually does.

## Proof of possession

[[[oauth-1.0s-proof-of-possession]]] was one of the major regrets in OAuth 2.0 for
removing. It's an essential security feature that was just omitted, and the world
has taken a lot of damage thereof.

OAuth 2.1 is promised to let the proof of possession do a comeback, as well as
simplifying it to the point that it's easier to implement, yet still keep its
core security concerns.

## Removal of implicit and ROPCG flows

Resource Owner Password Credential Grant flow was based on sending the users
password around, something that OAuth aimed to remove from the world. It existed
in the specification as a fallback, though an insecure one at that.

Most authentication providers does not even support this flow considering its
obvious lack of security, and with the same tone OAuth 2.1 is promised to remove
it completely from the specifications.

Implicit flow, which is used by most Single Page Applications (SPA) today, is
promised to be removed as well. The way its implemented today has some serious
security holes, such as the token usually gets saves in the users browser history
and that it can easily be snagged by a malicious piece of software running one
the website.

## References

- Cambell, R. & Franklin, C.. (Hosts). (2021, January 14). *IdentityServer Update
  with Dominick Baier and Brock Allen* (No. 1722) [Audio podcast episode].
  In *.NET Rocks!*. vNext.
