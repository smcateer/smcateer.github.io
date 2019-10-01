---
layout: post
title: "Commando python envs"
date: 2019-10-01
permalink: /commando-python-envs/
img: https://upload.wikimedia.org/wikipedia/commons/thumb/8/83/PEO_ANAVS-6_NVG.jpg/640px-PEO_ANAVS-6_NVG.jpg
published: true
tags: ["coding", "python", "environments", ]
---

Just a quick note on my approach to environments for data analytics (without undies). Here I'm using Python, Jupyter, and Conda, but the approach could be adapted to different languages or package managers.

There *are* two very good reasons to use envs for your analytics work:

1. **Known environment**: To make sure your code runs again when you come back to it after some time has passes (and some packages have changed). To make sure that your results are reproducible.
1. **Safe environment**: To have a sandbox in which you can screw around with your Python environment without the risk of ruining your entire life.

Known environment
---

This is really important for production or critical code, but in the context of data analytics it's mostly just a potential source of annoyance. Usually you will just need to adjust your code to make it work again. But then again, that might take a lot of time. It may also have an impact on the reproducibility of your results, which is a more serious concern.

But if you are doing envs *right* to deal with this, you will find yourself maintaining lots of envs (perhaps > 1 per project you have *ever* worked on). Also, at what point does scratching out a quick calculation become something more, and you need to *do the env thing*? Ever had the oh-crap-I-better-set-up-an-env-for-this thought?

Here's my commando workaround. Just work in the same dev env for all your code, but occasionally run the following but of code (I have it as a separate cell just after `import ...`).

```
import datetime as dt
import os
env_name = os.environ['CONDA_DEFAULT_ENV']
env_file = dt.datetime.now().strftime('%Y%m%dT%H%M%S') + '-env.yml'
!conda env export --name $env_name --file $env_file
```

(The last line is the Jupyter way of running a command in the shell).

This dumps the current version of all packages to a YAML file (in your working directory). If you come back to your code after a year and it won't run in your dev env (due to some pesky update in the interim), this file can be used to create a new env where the code *will* run.

This approach is very light-touch, but provides a way of making sure your code will work, and your results can be reproduced in the future.

Safe environment
---

For experimentation with new packages, or odd versions of packages, or packages with strange dependencies, I would recommend spinning-off a new sandbox env. Once you are confident the packages are not going to bork everything, you can consider rolling them into your main working dev env.
