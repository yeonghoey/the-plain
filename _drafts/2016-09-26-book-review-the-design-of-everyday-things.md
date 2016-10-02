---
title: "Book Review: The Design of Everyday Things"
---

I finally made my mind to write a personal programming blog in English.
To my surprise, the first post is about a design book, not programming things.

![Title]({{ site.url }}/assets/the-design-of-everyday-things-title.jpg)

# Why read?
I faced lots of recommendations of this book from programming books and blog posts,
although it's a design book.  Finishing the book, I totally agree 
that it's a must-read for every programmer.

For those who wonder how it matters for programmers, I quote a passage
about **the paradox of technology**.

> The same technology that simplifies life by providing more functions in each
> device also complicates life by making the device harder to learn, harder to
> use.  This is the paradox of technology and the challenge for the designer.

I think it makes sense to both the application and the code itself.

I'll show important concepts from the book, with some programming-related examples
I conceived.


## Affordances, Signifiers and Constraints

These concepts are about making things hard to fail.
Here are definitions about **affordances** and **signifiers** from the book:

- **Affordances** are the possible interactions between people and the 
environment.
- Perceived **affordances** often act as **signifiers**, but they can be ambiguous.
- **Signifiers** signal things what actions are possible and how they should be
done.
- **Signifiers** must be perceivable.

> A door **affords** opening.  
> It also **affords** being smashed.  
> The door's knob **signifies** opening.  
> The knob **signifies** whether pushed, pulled, or slid.

**Contraints** work for making things hard to fail.  **Affordances** and
**signifiers** is essential for designing **constraints**.

> The iron plate on a door **signifies** opening by pushing.  
> The iron plate also places a **contraint** of pulling. (Because there is no handle to grip)

These concepts are reminicent of interfaces and encapsulations in programming.
A well designed interface **signifies** how to use the library properly.  It
also hides not intended **affordances** by encapsulations.  It places
**constraints** for making things hard to fail.


## Mapping and Feedback

**Mapping** relates to the layout of controls and displays.  Consider the situation 
that you must do stage lighting.  There are lots of lights and you should continuously turn
some of them on and off at exact moments.  The problem is
that most traditional stage lighting controls simply place many buttons on a panel in a row.
You have to memorize which button controls which light.  It's a challenge and error-prone.

What if the buttons were arranged in the way the lights arranged?  You can just
map the buttons and lights.  It's relatively easier.

Let's see another example.  I'm writing this post in **Vim** editor[^1].  It maps
`hjkl` keys to the movement of cursor. Each key stands for 
**LEFT**, **DOWN**, **UP**, **RIGHT** respectively. 

**Vim**'s way is for efficiency.  You will love it once you get used to.
But it's a bad mapping from a design perspective.  It's one of the reasons
why people feel frustrated when they try to use the editor.

Conversely, most  games have `wasd` mapping for the player character's movement.
It's very natural because the way of keys arranged exactly stands for 
the direction of the movement.

> `hjkl` *NOT* naturally **mapped** to the movement of *cursor*.  
> `wasd` naturally **mapped** to the movement of a *character*.  

**Mapping** alleviates the complexity of controls.  But a great mapping alone
can't do much.  The more complex the device is, the harder we control.  We 
need **feedback** to understand how it works.

If you have used a iPod Shuffle, you may have feelings what I mean.
It intentionally removed display, which causes lack of **feedback**.
Even though it has a relatively great **mapping**, you can't select the exact songs and play lists you want.

**Feedback** plays an important role in understanding.
When people made a mistake and were notified at an appropriate moment, they learn. 
**Feedback** enhances understanding of the product.

The amount of **feedback** should be adequate.  Poor **feedback** makes people frustrated.
It makes people hard to understand what's happening.  It's simply a root of error.
Too much **feedback** is also a problem.  It makes people annoyed.  What's more, 
it makes people ignore some feedback which is important.

Let's see the programming example.  The nature of **feedback** exactly makes sense on
writing error messages.  Many programming books suggests that we should not simply
ignore warning messages.  Lots of warnings messages can conceal important errors.

Lack of detailed information is also a problem.
What if you get a simple message `error occurred`?  You get lost.


## Conceptual Models
> **Conceptual models** are valuable in providing understanding,
> in predicting how things will behave, and in figuring out what to do
> when things do not go as planned.

Consider traditional watches.  Most of them have relatively many features for
their buttons.  As a result, they tend to have many modes without proper conceptual models.
A button is mapped for starting timer on the timer mode and for increasing number on 
the time resetting mode.  Because there is *no* **conceptual model**,
I always forget the mappings and feel frustrated.

I recently tried to use a pebble watch[^2].  I noticed that it has a nice conceptual model with proper mappings.

![PebbleButtons]({{ site.url }}/assets/pebble-watch-conceptual-model.jpeg)

Based on these simple mappings, every application follows the conceptual model
of scrolling up and down with `Up` and `Down`, pushing and popping contexts with `Back` and `Select`.

I immediately understood how it works.  I enjoyed the experience.


## requests and urllib2

If you used `python` for web client, you probably wrote the program with `requests` library,
which is a *de facto* standard in python community.  By the way, did you know `urllib2` which is 
a standard library for doing the almost same thing?  Let me explain why `requests` is more popular
on the ground of the preceding concepts. 

```python
import requests
requests.get('http://google.com')

import urllib2
urllib2.urlopen('http://google.com')
```

So far, there seems almost no difference.
But with considering **mapping**, `requests` is better,
Because it directly maps `HTTP GET` requests to `requests.get()` method.

I could construct the **conceptual model** of `requests`.
I can expect `requests.post()` method, which will make a `HTTP POST` request.
And, actually it has the method.

On the other hand, `urllib2` enforces a different model (*what is **urlopen**ing?*).
It was hard to find out how to make a `HTTP POST` request with `urllib2`.
After wading through its document, I found an example code:

```python
import urllib
import urllib2

url = 'http://www.someserver.com/cgi-bin/register.cgi'
values = {'name' : 'Michael Foord',
          'location' : 'Northampton',
          'language' : 'Python' }

data = urllib.urlencode(values)
req = urllib2.Request(url, data)
response = urllib2.urlopen(req)
the_page = response.read()
```

Notice that the term `post` is not in the code.
Here is the explanation:

> you can use a POST to transmit arbitrary data to your own application.
> In the common case of HTML forms, the data needs to be encoded in a standard way,
> and then passed to the Request object as the data argument.
> The encoding is done using a function from the urllib library not from urllib2.  
> ...  
> If you do not pass the data argument, urllib2 uses a GET request.

It's wordy.  Here is the same code using `requests`.

```python
import requests
url = 'http://www.someserver.com/cgi-bin/register.cgi'
data = {'name' : 'Michael Foord',
        'location' : 'Northampton',
        'language' : 'Python' }

response = requests.post(url, data=data)
```
It reads naturally, as expected.  It seems obvious which one is better.

I'm showing this neither for blaming `urllib2` nor flattering `requests`.
But for showing how the the design concepts make sense to the programming world.


## Summary
Technology is getting complicated.
The speed of change is far faster then the speed of human capacity improvements.
The design concepts in this book are all for keeping things simple, less error-prone.

Programming is no exception.  In some sense, programming is nothing but a logic design.
With the concepts in mind, we would become a better programmer.


[^1]: It's actually [Spacemacs](http://spacemacs.org/), which is a plugin-powered *Emacs* with *Vim* key mappings.
[^2]: It's a newer than the one in the following picture.
