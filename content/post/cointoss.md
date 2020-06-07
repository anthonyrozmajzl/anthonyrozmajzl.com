+++
author = "Anthony Rozmajzl"
categories = ["datacamp", "python"]
date = 2018-08-15T02:55:34Z
description = ""
draft = false
feature = "/images/cointoss-1.png"
slug = "cointoss"
tags = ["datacamp", "python"]
title = "A Simple Coin Toss"

+++


Plugging through the Python courses at DataCamp has been (for the most part) quite a bit of fun. Anyone who has gone through the process of learning a new coding language will understand why I included the parentheses. My last exposure to any sort of coding was a C++ class in high school, and I remember coming out of that class swearing to drop the whole coding thing forever. I hated how nitpicky the coding syntax was; and even if I had the syntax correct, there was no guarantee that my code would produce what I wanted . . . and it rarely did. I just couldn't believe that anybody would want to do this for a living.

Six years later and I am giving the whole coding thing another shot, this time with the much more engaging and interactive DataCamp. It hasn't been a walk in the park by any means, but I am definitely learning a lot more than I did in my textbook-style high school class. DataCamp's platform is super easy to use and does an excellent job of testing your skills with practical examples. 

Unlike my high school coding class, DataCamp's interactive platform nudges you in the right direction when your code needs to be tweaked. I vividly remember the frustration involved with having to walk up to my teacher time and time again to ask for help whenever I was stuck. I was just hoping that my teacher wasn't also backed up with other students who were stuck in the same boat as me. The point is, anybody who wants to learn Python, R, or SQL should definitely give DataCamp a try.

One of my favorite chapters from DataCamp's *Data Scientist with Python* career track was their introduction to `for` loops. After starting with the fundamentals, I eventually learned how to construct a `for` loop that builds a distribution for flipping a coin. I know that this is old hat for more experienced coders, but for me it was a gratifying challenge.

Below is the Python code and the steps I used to produce my coin flip distribution:

```python
import matplotlib.pyplot as plt
import random
import numpy as np

heads = 0
rounds = 10
tosses = 100

heads_per_round = []

for round in range (rounds):
    for flips in range(tosses):
        coin = np.random.randint(1,3)
        if coin == 1:
            heads+=1
    heads_per_round.append(heads)
    heads = 0
    
plt.hist(heads_per_round, bins =10, color="red", alpha=.5)
plt.show()
```
![Coin-Toss-graph-1](/images/Coin-Toss-graph-1.png)

Hmmmm.  That doesn't look that useful.  We'll fix that later.  For now, let's break down the code.

## Code Walk-Through

### Collect Number of Heads per Round
I created the empty list `heads_per_round` to track the number of heads that were recorded for each of the rounds of coin flips. 

### Need a Counter
The `heads` variable is initialized to 0 because it represents the starting number of heads that have shown up. It's reset to 0 at the end of each round. Obviously, you could also count the number of tails that appear. This is just a matter of changing the variable definitions.

### The Rounds
The outer `for` loop represents the number of *rounds* of coin tosses. Number of rounds is captured in the `rounds` variable. 

### The Tosses
The inner loop represents the number of coin flips per round. The number of tosses is set in the `tosses` variable. For every round of 100 tosses, we might get something like 40 or 53 or 65 heads. That number of heads is appended to the list `heads_per_round`. 

### The Coin
The variable `coin` captures the result of a virtual coin toss. Defining `coin` as 'np.random.randint(1,3)' produce either a 1 or a 2. If our virtual coin = 1, then we add 1 to the variable 'heads'.  Thus, our list `heads_per_round` might look like the following: `[44, 54, 48, 60, 55, 41, 48, 58, ... , 59, 65]`.

### Seeing the Results
The final step is to plot the list `heads_per_round`. A histogram will allow you to visualize your data as a distribution.

That histogram produced above looks a little sparse and not quite what we want. This is because our sample size of 10 rounds of coin tosses is pretty small. The more rounds we run, the more data points we can collect and the more closely the histogram will reflect a normal distribution. 

What follows are two histograms: the first illustrates 100 rounds of 1,000 coin tosses and the second illustrates 1,000 rounds of coin 10,000 tosses. What we should see are two histograms more closely resembling a normal distribution.

### 100 Rounds of 1,000 Tosses
```python
...
rounds = 100
tosses = 1000
...
```
![Coin-Toss-graph-2](/images/Coin-Toss-graph-2.png)

### 1,000 Rounds of 10,000 Tosses

![Coin-Toss-graph-3](/images/Coin-Toss-graph-3.png)

I could continue to increase `rounds` and `tosses` to achieve an almost perfectly-normal distribution. 

Now, good programmers are constantly looking for ways to improve their code, including simplifying it.  Here is a nicely-refactored version of code that produces the results of 1,000 rounds of 10,000 coin tosses:

```python
import matplotlib.pyplot as plt

heads_per_round = []
rounds = 1000
tosses = 10000
for round in range(rounds):
    heads_per_round.append((np.random.randint(0,2,tosses)>0).sum())

plt.hist(heads_per_round, bins = 20)
```

As before, we create the empty list to track the number of heads that showed up for each round of tosses. The loop cycles through 1,000 rounds, each of which will have 10,000 tosses. 

The magic occurs in the line of code just beneath the `for` loop. The code `np.random.randint(0,2,tosses)>0).sum()` randomly generates an array of 0's and 1's, filters out all the 0's (leaving only 1's remaining), and sums all elements, giving the total number of "heads" for that round. (Gotta love NumPy!).

So what does this look like?

![Coin-Toss-Simple](/images/Coin-Toss-Simple.png)

Again, it appears that 1,000 rounds appears to produce another distribution that closely resembles the normal distribution.

# Wrap Up

A little over a month ago, producing this kind of distribution would have been challenging for me. Looking back on how far I have come, this simple coin toss distribution boosted my confidence as a coder. I plan to share more examples of what I have learned with Python and am looking forward to broadening my knowledge with Data Camp's *Data Scientist with R* career track.

