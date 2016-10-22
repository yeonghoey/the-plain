---
title: Streamlining your search with Chrome Omnibox
image: /assets/omnibox-usage.jpg
---
**Omnibox** is a nickname for Chrome's address bar.
As you know, you can search on Google in there
when you put text other than URLs.

Incidentally, **did you know that you can search on whatever search engine
you like in there?** Let me explain how.


## Search Engines configuration

Open *Search Engines* menu:  
![Guide1]({{ site.url }}/assets/omnibox-guide1.jpg)


A window like following will show up:  
![Guide2]({{ site.url }}/assets/omnibox-guide2.jpg)


## How it works

There are 3 columns in the *Other search engines*[^1].
Each column signifies **Name**, **Keyword** and **Search String** respectively.

Let's take a look at how each element cooperates:

![Usage]({{ site.url }}/assets/omnibox-usage.jpg)



## Find out Search String

To find out **Search String**s for your favorite search engines,
you need to do simple experiments.

1. Enter search words into the search engine.
1. Recognize the words you just entered from the result URL.
1. Replace them with `%s`

Here is an example: (featuring [SymbolHound](http://symbolhound.com/))

> http://symbolhound.com/ (default)  
> http://symbolhound.com/?q=yeongho (searched 'yeongho')  
> http://symbolhound.com/?q=%s (**Search String**)  


## My Search Engines configuration

I listed my *Search Engines* configuration for those who feel frustrated with
finding out **Search String**s:

```
bookmarks     b   chrome://bookmarks/#q=%s
history       h   chrome://history/?#q=%s
github        gh  https://github.com/search?q=%s
google        g   http://www.google.com/search?q=%s
google image  i   http://www.google.com/search?tbm=isch&q=%s
naver         n   https://search.naver.com/search.naver?query=%s
naver endic   e   http://endic.naver.com/search.nhn?query=%s
naver krdic   k   http://krdic.naver.com/search.nhn?query=%s
symbolhound   s   http://symbolhound.com/?q=%s
thesaurus     t   http://www.thesaurus.com/browse/%s
youtube       y   https://www.youtube.com/results?search_query=%s
```


## Bookmark Search Chrome Extension

[Bookmark Search] is an extension using **Omnibox**.
Like other custom search engines, you can trigger it by the **Keyword**, `bm`.

The best thing about it is **auto-completion**.
You can open your bookmarks in a single step
without knowing the exact bookmark that you desire for.

![Bookmark Search]({{ site.url }}/assets/omnibox-bookmark-search.jpg)
I put `pyth` in there, and
it shows the list of my bookmarks related to **Python**.
I can open reference documents just a single step by this extension.


## Summary

It may seem that 
all these works are just for saving a single step.

However, How many times do you search in a day?
One step save for every single search would be a huge save.
In addition to there, ease to search makes you look things up more,
which leads you to working more effectively.

Happy search!


[^1]: You may have some search engine definitions in there, because Chrome  automatically identifies and registers search engines there.
[Bookmark Search]: https://chrome.google.com/webstore/detail/bookmark-search/hhmokalkpaiacdofbcddkogifepbaijk
