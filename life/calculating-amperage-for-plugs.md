---
date: 2021-01-17T21:29
tags:
  - life/working with electricity
  - life/mathmatics of volts
---

# Calculating amperage for plugs

Given you know the wattage to be consumed, the voltage of your local home's power
grid (most commonly 230V in Europe, **but you should look it up! No space for
assuming here**), and the amperage of the plugs you have installed in your plugs
cabinet, you can then calculate which of the outlets you can use for your
power consumption.

## Prerequisite knowledge

- Amperage ($A$) of the already installed plugs. Good idea grasp the inventory of
  used plugs so you can map which outlets has a certain (shared) amperage to use.
  Common amperage of plugs are: $6A, 10A, 16A$

- Voltage ($V$) of your home's power grid. Common voltage in Europe is: $230V$

- Wattage ($W$) of the equipment you wish to power. Lights usually hover around
  the lower dussins of watts, while electric radiators usually use around $1000W$

## Calculating wattage

Wattage is calculated by $W = A \times V$.

So let's say you find in your plug cabinet three plugs that all take different
amperage. You also find a note besides the cabinet describing their use case.

| Description        | A     |
| ------------------ | ----- |
| Living room lights | $6A$  |
| Radiator, hallway  | $10A$ |
| Stove              | $16A$ |

How much wattage $W$ will the stove plug actually allow? Well. Let's take out our
formula again and plug in the numbers:

$$
\begin{align}
    W &= A \times V \\
    &= 16_{A} \times 230_{V} \\
    &= 3680_{W}
\end{align}
$$

If your stove's manual says it can use up to $1500W$, that means you can then
install another (identical) stove on an outlet that uses the same plug!

Calculating the wattage of all of the above listed $6A$, $10A$, and $16A$ plugs,
it would give us the maximum wattages of $1380W$, $2300W$, and $3680W$,
respectively.

## Can I just swap my current plugs?

Let's say I just want to install my new console (that for sake of argument
can use up to $1500W$) in the living room, and plug it in to an outlet that goes
to the living room lights, *can I just swap my current living room plug out for
a $10A$ plug?*

[No.](https://en.wikipedia.org/wiki/Betteridge%27s_law_of_headlines) Leave it to
the professionals. Read more on why you should [[never-change-a-plugs-amperage]]#
