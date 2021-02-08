---
date: 2021-02-08T20:38
tags: 
  - stub
---

# Stocks trading service using volatility decomposition

Instead of looking at a [[stocks-trading-service-using-functional-decomposition]],
let's instead look at doing some #[[volatility-decomposition]] to design a
stock trading system.

Let's investigate the volatilities.

## Volatilities

- Types of users: Power users, casual users, sysadmins, robots, executives
- Authentications
- Notifications
  - Delivery: Email, SMS, fax
  - Recipients: Boss, coworkers, custom list of emails, department
  - Fallback procedures
- Storage of data
  - Local DB / remote DB
  - Data replication (redundancy)
  - Caching
- Connectivity, async vs sync
  - Recovery
  - Out of order
- Jumping platforms
  - Work comp. -> phone on train -> PC at home
  - Duration of interactions
- Locality
  - Rules per locales
- Stock provider
  - Data feed
  - Content
  - Real vs simulated
  - Frequency
  - Format
- *And much, much more...*

This is a non-exhaustive list of the volatilities. This is just to give some
concrete samples of volatilities.

## References

- J. Löwy (January 27, 2021), *"Righting Software - System Design"* [Workshop],
  NDC London 2021.
