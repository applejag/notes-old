---
date: 2021-02-17T19:29
tags:
  - code design/how to be a good designer
  - code design/how to do volatility decomposition
  - code design/finding use-cases
---

# Getting good at volatility decomposition

Designing by #[[volatility-decomposition]] is miles more difficult than designing
by [[functional-decomposition]].

It's a skill. And as which any skill, practice makes perfect.

> "You can never be good at something that you spend 2% or less of your time on."
> --- J. Löwy (at 53:11, Dolittle, J., 2020, April 24)

## Practice on corpses

As a customer, you never want to be patient number 1 from a doctor.

Like how doctors practice on corpses, you shall practice on dead systems.

Analyse and try identify the volatilities, use-cases, and components. Ask
yourself:

- **What use-cases can you identify:** An old project will have all of its
  use-cases already defined. Much simpler to seek out the existing ones than to
  identify the unknown use-cases in a planned project.
  
- **What *core* use-cases can you identify:** What is actually the core use-case
  of this system? What counts as *fluff*?

- **How did it segregate the use-cases:** Which components was created to
  separate the different concerns? How was it decompositioned? No answer is
  absolute. Some parts will have been made better than others.

- **What went wrong:** What could have been changed that would've been benefitial
  for the system? 

- **What went good:** What did the project do right; that you can take
  inspiration from in future projects?

## Not only past projects

Designing the architecture (or in this case, analysing existing architectures)
is not restricted to software. It can be found everywhere.

Try to practice [[finding-a-systems-volatilities]]# on systems such as a grocery
store, a car, your house, a game, etc.

You should practice on:

- Past software systems
- Current software systems
- Systems from other companies
- Non-software systems

## When you are ready

The biggest issue you will have is your [[issues-with-the-manager]]#. You will
have to fight the manager, and your coworkers, with designing the system in any
other way than [[functional-decomposition]].

This is a losing battle. You won't have managers that are kind hearted and trust
you to get a good design out in a year, while no one is allowed to write any
code. You won't get that time! They want their product!

You need to be so good at [[volatility-decomposition]] that you can do it so
quickly so that no one notices, and more importantly so quickly that no one has
any time to argue against you.

By the time they want to argue about your orthodox design procedure, there will
already be a design in front of them that they can start working on.

## References

- J. Löwy (January 27, 2021), *"Righting Software - System Design"* [Workshop],
  NDC London 2021.

- Doolittle, J. (Host). (2020, April 24). *Juval Löwy on Righting Software*
  (No. 407) [Audio podcast episode].
  In *Software Engineering Radio*. IEEE Software.
  <https://www.se-radio.net/2020/04/episode-407-juval-lowy-on-righting-software/>
