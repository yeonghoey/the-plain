---
title: Streamlining your search with Chrome Omnibox
image: /assets/omnibox-usage.jpg
---
Omnibox is a nickname for Chrome's address bar.
As you know, you can search on Google in there
when you put text other than URLs.

Incidentally, **did you know that you can search on whatever search engine
you like in there?** Let me explain how to.

## Search engines configuration

Open *Search engines* menu:  
![Guide1]({{ site.url }}/assets/omnibox-guide1.jpg)


A window like following will show up:  
![Guide2]({{ site.url }}/assets/omnibox-guide2.jpg)


## How it works

There are 3 columns in the *Other search engines*[^1].
Each column signifies `Name`, `Keyword` and `Search String` respectively.

Let's take a look at how each column works:

![Usage]({{ site.url }}/assets/omnibox-usage.jpg)



## Find out Search String

To find out `Search String` for your favorite search engines,
you need to do simple experiments.

1. Enter a search word into the search engine.
1. Recognize the word you just entered from the result URL.
1. Replace it with `%s`

Here is an example: (featuring [SymbolHound](http://symbolhound.com/))

> http://symbolhound.com/  
> http://symbolhound.com/?q=yeongho  
> http://symbolhound.com/?q=%s  


## My Search engines configuration

I listed my *Search engines* configuration for those who feel frustrated:

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

[^1]: You may have some search engine definitions in there, because Chrome  automatically identifies and registers search engines there.
