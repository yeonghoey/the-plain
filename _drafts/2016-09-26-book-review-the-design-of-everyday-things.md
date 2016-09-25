---
title: "Book Review: The Design of Everyday Things"
---

![Title]({{ site.url }}/assets/the-design-of-everyday-things-title.jpg)

# Why read?
Faced lots of recommendations from programming books and blog posts,
even though it's a design book.


# The Paradox of Technology

> The same technology that simplifies life by providing more functions in each
> device also complicates life by making the device harder to learn, harder to
> use.  This is the paradox of technology and the challenge for the designer.


## Affordances, Signifiers and Constraints

Concepts for making things hard to fail.
Here are definitions about **affordances** and **signifiers**:

- **Affordances** are the possible interactions between people and the 
environment.
- Perceived **affordances** often act as signifiers, but they can be ambiguous.
- **Signifiers** signal things what actions are possible and how they should be
done.
- **Signifiers** must be perceivable.

> A door **affords** opening.  
> It also **affords** being smashed.  
> The door's knob **signifies** opening.  
> The knob **signifies** whether pushed, pulled, or slid.

**Contraints** work for making things hard to fail.  And **affordances** and
**signifiers** is essential for designing **constraints**.

> The iron plate on a door **signifies** opening by pushing.  
> The iron plate also places a **contraint** of pulling.

These concepts are reminicent of interfaces and encapsulations in programming.
A well designed interface **signifies** how to use the library properly.   It
also hides not intended **affordances** by encapsulations.  It places
**constraints** for making things hard to fail.


## Mapping, Feedback, and Conceptual Models

**Mapping** relates to layout of controls and displays.  Consider the situation 
that you must control stage lighting.  There are lots of light bulbs and you 
should turn  some of them on and off at an exact moment.  The problem is that 
most traditional stage lighting controls just place many control buttons on a 
panel in a row.  You have to memorize which button controls which light.  It 
can be a challenge and error-prone.

What if the buttons were arranged in the way the lights arranged?  You can just
map the buttons and lights.  It's relatively easier.

Let's see another example.  I'm writing this post in **Vim** editor.  It maps
`hjkl` keys on the keyboard to the movement of cursor. Each key stands for 
**LEFT**, **DOWN**, **UP**, **RIGHT** respectively. 

**Vim**'s way is for efficiency and I love it.  But it's a bad mapping from a
design perspective.  It's one of the reasons why people feel frustrated when 
they try to use **Vim**

Conversely, most traditional FPS games have `wasd` mapping for the player
character's movement.  It's very natural because the way of keys arranged
exactly stands for the direction of the movement.

**Mapping** alleviates the complexity of controls.  But by only great mapping 
can't do much.  The more complex the device is, the more harder we control.  We 
need feedback to understand how it works.  If you have used a iPod Shuffle, you 
may have felt what I mean.  It intentionally removed display, which causes lack 
of feedback.  It has a great mapping, but you can't select the exact play list 
you want.
