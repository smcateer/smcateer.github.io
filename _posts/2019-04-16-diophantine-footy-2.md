---
layout: post
title: "Diophantine footy 2: generalised footy"
date: 2019-07-25
permalink: /diophantine-footy-2/
published: true
tags: ["footy", "australian rules football", "maths", "diophantine equations", ]
---

BTW, this is a follow up to [diophantine footy](https://smcateer.github.io/diophantine-footy/) ... read that first for context.

So I was thinking about what would happen if a goal was worth an arbitrary number of points (\\(p\\)) (rather than 6) - the number of solutions for \\(p = 6\\) struck me as a bit high. So I scratched together the following bit of Python to count solutions.

``` python
# we want to consider a range of points per goal (p) (regular footy is 6)
for p in range(1,15):
    print('Points per goal: {:d}\n----'.format(p))
    # a counter for the solutions
    cnt = 0
    # number of goals
    for g in range(1,100):
        # number of points
        for b in range(1,100):
            # this is the condition we want to satisfy
            if b*g == b + p*g:
                cnt += 1
                print('Soln: {:d}.{:d} ({:d})'.format(g, b, g*b))
    print('Number of solns: {:d}\n'.format(cnt))
```

And here are the results:

| \\(p\\)             | 1  | 2  | 3  | 4  | 5  | 6  | 7  | 8  | 9  | 10 | 11 | 12 | 13 | 14 |
| :---                |---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|
| number of solutions | 1  | 2  | 2  | 3  | 2  | 4  | 2  | 4  | 3  | 4  | 2  | 6  | 2  | 4  |


We now have two options. One, stare at the sequence and hope our brain clicks, or two, [to the OEIS!!!][1] (BTW, if you get too many results from the OEIS, just calculate more terms and search again). (BTW 2, if you ever generate a sequence that does not appear on the OEIS, submit it and go down in history).

The top hit in the OEIS was the number of divisors of \\(n\\), this is a great clue to what is going on. Let's look at the generalised version of the equation we are trying to solve:

\\[pg+b = bg\\]

[1]: https://oeis.org/search?q=1%2C+2%2C+2%2C+3%2C+2%2C+4%2C+2%2C+4%2C+3%2C+4%2C+2%2C+6%2C+2%2C+4&language=english&go=Search
