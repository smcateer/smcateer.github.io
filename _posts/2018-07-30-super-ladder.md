---
layout: post
title: "Enhanced AFL ladder"
date: 2018-07-30
tags: ["python", "afl", "ladder", "sport", ]
---

At the time of publication, [Essendon](http://www.essendonfc.com.au/) are clearly the best team in the AFL. Well maybe not clearly, but that's my claim. This is for two reasons:
1. Only recent form matters (and Essendon have been dominating recently), and
2. It's east to look good with a soft draw (I'm looking at you Collingwood).

[This code](https://github.com/smcateer/super_ladder) can be used to calculate a version of the ladder which takes these effects into account. It does this by allowing you to exclude all but the most recent rounds, and scaling the points you get for a win by the quality of your opposition (using the team's percentage as a proxy for quality).

The points you get for a win are \\(4 \times r^p \\) for a win, and \\(2 \times r^p \\) for a loss, where \\(r\\) is the opposition's percentage (as calculated for the standard ladder) and \\(p\\) is a parameter.

Setting \\(p = 0\\) corresponds to the standard ladder, setting \\(p = 1\\) means beating two teams with 50% is equivalent to beating one team with 100%. I think \\(p = 2\\) is a good value, it means that you need to beat 2 teams with 71% (or 4 teams with 50%) to get the points equivalent to beating one team with 100%.

Anyway, here are the results (at the end of round 19, 2018):

```
> super_ladder() # standard ladder

                TEAM  POINTS  SCORE  OPPONENT_SCORE  PERCENTAGE
0           Richmond    56.0   1754            1273  137.784760
1         West Coast    52.0   1619            1335  121.273408
2        Collingwood    48.0   1680            1422  118.143460
3      Port Adelaide    48.0   1476            1270  116.220472
4         GWS Giants    46.0   1524            1341  113.646532
5          Melbourne    44.0   1868            1467  127.334697
6           Hawthorn    44.0   1631            1329  122.723853
7            Geelong    44.0   1603            1333  120.255064
8             Sydney    44.0   1508            1372  109.912536
9    North Melbourne    40.0   1564            1414  110.608204
10          Essendon    40.0   1523            1482  102.766532
11          Adelaide    36.0   1502            1528   98.298429
12         Fremantle    28.0   1279            1593   80.288763
13  Western Bulldogs    20.0   1219            1737   70.178469
14          St Kilda    18.0   1289            1703   75.689959
15          Brisbane    16.0   1498            1666   89.915966
16        Gold Coast    16.0   1096            1694   64.698937
17           Carlton     8.0   1125            1799   62.534742
```

With opposition quality taken into account:
```
> super_ladder(scale_power=2) # ladder allowing for opposition quality

                TEAM     POINTS  SCORE  OPPONENT_SCORE  PERCENTAGE
0           Richmond  59.236194   1754            1273  137.784760
1         West Coast  52.770018   1619            1335  121.273408
2            Geelong  47.613679   1603            1333  120.255064
3             Sydney  45.272944   1508            1372  109.912536
4         GWS Giants  44.597565   1524            1341  113.646532
5           Essendon  43.314357   1523            1482  102.766532
6      Port Adelaide  42.953202   1476            1270  116.220472
7           Hawthorn  41.424336   1631            1329  122.723853
8        Collingwood  38.570038   1680            1422  118.143460
9    North Melbourne  35.218554   1564            1414  110.608204
10          Adelaide  34.827736   1502            1528   98.298429
11         Melbourne  32.130806   1868            1467  127.334697
12         Fremantle  20.992509   1279            1593   80.288763
13  Western Bulldogs  16.481467   1219            1737   70.178469
14          Brisbane  16.191667   1498            1666   89.915966
15          St Kilda  15.541328   1289            1703   75.689959
16        Gold Coast  14.524166   1096            1694   64.698937
17           Carlton   5.898765   1125            1799   62.534742
```
Note that Collingwood move from 3rd on the ladder to 9th - hard evidence that Collingwood suck. Melbourne also take a hit, and Essendon do quite well moving up to 6th.

Much has been made of Essendon's slow start to the season, here's what the ladder looks like when you only consider rounds 9 to 19 (i.e. 10 games when you allow for the byes):
```
> super_ladder(rnd_cnt=11) # ladder for rounds 9 to 19

                TEAM  POINTS  SCORE  OPPONENT_SCORE  PERCENTAGE
0        Collingwood    32.0    991             747  132.663989
1           Essendon    32.0    876             711  123.206751
2      Port Adelaide    28.0    784             596  131.543624
3           Richmond    28.0    932             723  128.907331
4         GWS Giants    28.0    884             762  116.010499
5          Melbourne    24.0   1087             777  139.897040
6           Hawthorn    24.0    888             697  127.403156
7            Geelong    24.0    894             757  118.097754
8             Sydney    24.0    827             733  112.824011
9         West Coast    24.0    822             740  111.081081
10   North Melbourne    24.0    921             843  109.252669
11          Brisbane    16.0    912             871  104.707233
12          Adelaide    16.0    725             884   82.013575
13          St Kilda    12.0    775             962   80.561331
14         Fremantle    12.0    655             931   70.354458
15  Western Bulldogs     4.0    593             982   60.386965
16           Carlton     4.0    568             999   56.856857
17        Gold Coast     4.0    526             945   55.661376
```
I like this even better, Essendon move to 2nd. But what about Collingwood? Surely nobody can deserve to be top of the ladder with their draw. (Why rounds 9 to 19? Well, that might be the choice that most favours Essendon ... never claimed to be unbiased!)

Okay, let's include both effects (recent form and opposition quality):
```
> super_ladder(scale_power=2, rnd_cnt=11)

                TEAM     POINTS  SCORE  OPPONENT_SCORE  PERCENTAGE
0           Essendon  33.368587    876             711  123.206751
1           Richmond  31.664983    932             723  128.907331
2         GWS Giants  30.972215    884             762  116.010499
3         West Coast  29.617419    822             740  111.081081
4        Collingwood  27.241834    991             747  132.663989
5            Geelong  24.612432    894             757  118.097754
6      Port Adelaide  22.520989    784             596  131.543624
7             Sydney  19.964535    827             733  112.824011
8    North Melbourne  19.382228    921             843  109.252669
9           Adelaide  16.358511    725             884   82.013575
10          Brisbane  16.258232    912             871  104.707233
11          Hawthorn  15.582871    888             697  127.403156
12         Melbourne  11.571230   1087             777  139.897040
13         Fremantle  10.905061    655             931   70.354458
14          St Kilda  10.360829    775             962   80.561331
15  Western Bulldogs   5.578832    593             982   60.386965
16        Gold Coast   5.091703    526             945   55.661376
17           Carlton   1.239275    568             999   56.856857
```
That's the result I wanted! But if this is a fair indication of the current form in the AFL, and Essendon end up not making the finals (looks fairly likely), what a wasted season! 
