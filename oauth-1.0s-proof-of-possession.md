---
date: 2021-01-26T20:08
tags: 
  - security/securing authentication
  - security/managing login
  - security/proof of possession
  - security/oauth
---

# OAuth 1.0's proof of possession

Best feature of OAuth 1.0 that was stripped from 2.0 was its concept of "proof of
possession" for tokens.

A token, such as a JWT, can easily be stolen when a SPA uses for example the
OAuth 2.0 implicit flow and then used elsewhere, for example by a hacker.

The concept built upon cryptography, where the authentication service on the
website could verify that the users token does in fact come from the user
themselves.

Without going into detail, the proof of possession sealed the attack vector of
getting your token into the wrong hands and used without your permission.

## References

- Cambell, R. & Franklin, C.. (Hosts). (2021, January 14). *IdentityServer Update
  with Dominick Baier and Brock Allen* (No. 1722) [Audio podcast episode].
  In *.NET Rocks!*. vNext. <https://www.dotnetrocks.com/?show=1722>
