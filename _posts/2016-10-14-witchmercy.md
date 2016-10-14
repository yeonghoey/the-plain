---
title: Winning Mercy's Halloween Witch skin
---

![WitchMercy]({{ site.url }}/assets/witchmercy.jpg)

## Goal
Winning **Overwatch Mercy's Halloween Witch skin** at the minimum cost.


## Data
There are five bundle types:

| box count | cost(won) | per box(won) |
|----------:|----------:|-------------:|
|         2 |      2400 |        1200  |
|         5 |      6000 |        1200  |
|        11 |     12000 |        1091  |
|        24 |     24000 |        1000  |
|        50 |     48000 |         860  |


## Assumption
1. I can win a legendary skin every 10 boxes[^1].
1. The chances of winning Halloween skins are drastically higher than others during the event season.
1. I have **1/40 or slightly less chance**[^2] of winning the witch skin for each box.
1. I will **buy 50 boxes**[^3] at most.


## Solution
Calculate the expected cost for winning the witch skin.  
I can stop when I win the skin.  For example:

> When I buy `x` boxes for `y` won with the chance `p` of winning the skin:

```
count = x
cost = y
```

> The probability of not winning the skin `f` is `(1-p)^x`.  
> Buy another `xx` boxes for `yy` won with the same chance `p`:

```
count = x + xx
cost = y + f*yy
```

Calculate these until the `count` is greater than or equal to **50**.  
Calculate all possible cases by brute force algorithm[^4].


## Simplification
Ignore the order of buying bundles.  Consider the following cases:

- 2 5 11
- 2 11 5
- 5 11 2
- ...

These are all considered as `2 5 11`.  
With this simplification, the algorithm becomes easier and faster.


## Result
With `p = 1/40`, I got the following result:

```
34900.83, [2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2]
35051.39, [2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 5, 5]
35060.40, [2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 11, 11]
35062.75, [2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 5, 11]
35245.33, [2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 5, 5, 5, 5]
```

With `p = 1/60`, I got the following result:

```
40557.05, [2, 2, 2, 11, 11, 11, 11]
40769.93, [2, 2, 11, 11, 24]
40908.81, [2, 2, 2, 2, 2, 2, 5, 11, 11, 11]
40979.78, [2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 11, 11]
41110.21, [2, 24, 24]
```
Because buying 2 boxes for 25 times is cumbersome[^5],  
I decided to follow the best one of `p=1/60` case.

**I bought 2 bundles of 11 boxes and won the witch skin at the 22nd try!**  

[^1]: This is from a [Korean post](http://snaketeacher1.tistory.com/288).
[^2]: Because there are 4 Halloween legendary skin. By assumption 2, we can simply assume like that.
[^3]: I currently have 1100 credits, and probably get about 2000 credits after opening 50 boxes.
[^4]: The code is [here](https://github.com/yeonghoey/witchmercy)
[^5]: The best solution of `p=1/40` case.
