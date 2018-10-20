---
title: Math Trainer
link: https://mathtrainer.netlify.com/
source code: https://github.com/sjhuang26/math-trainer
timeframe: 7th grade
team: myself
status: production ready
description: Browse math problems which are loaded from a wiki.
learned: Vue, sanitizing data, lots of best practices when writing applications
---
Math Trainer allows users to browse math problems which are loaded from the Art of Problem Solving wiki. This was one of my first big web apps.

There were several interesting components to this project:

* The wiki was user-edited, so it had some formatting issues that needed to be dealt with (missing headers, incorrectly positioned footer).
* I refactored my code structure multiple times to address issues of modularity, class inheritance structures, naming conventions, and documentation. This project taught me lots of best practices the hard way.
* I realized that I needed to optimize and minify code assets with Webpack to reduce loading times.
