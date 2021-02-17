---
date: 2021-02-08T19:38
tags: 
  - code design/how to do volatility decomposition
---

# Finding a system's volatilities

Figuring out which volatilities a system will have, is seeking the hidden.

Figuring out which feature/functions a system will have, is obvious.

> Reminder: A volatility does not equal a component/micro service.

This is the first step in designing the architecture of a system 
using #[[volatility-decomposition]].

## Start easy

Complexity emerges from simplicity.

Start with the volatilities you easily recognize, or have seen come up many times
throughout your experience with software.

Notifications is an easy starting point.

## List everything

Everything you can come up with, and then put some time in to review and come up
with some more. See the sample of a
[[stocks-trading-service-using-volatility-decomposition]]# to get an idea of the
scope of volatilities.

When you've done this, continue with [[finding-a-systems-components]]#.

## References

- J. Löwy (January 27, 2021), *"Righting Software - System Design"* [Workshop],
  NDC London 2021.
