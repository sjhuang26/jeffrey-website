---
title: Math Trainer
link: https://mathtrainer.netlify.com/
code_link: https://github.com/sjhuang26/math-trainer
timeframe: 7th grade
team: myself
status: not-ongoing
description: browse math problems, loaded from the Art of Problem Solving wiki
---
{{% slide %}}
Math Trainer allows users to browse math problems which are loaded from the Art of Problem Solving wiki. Data from the wiki is fetched, and the user selects year, test, and question. I wrote this in seventh grade, mainly for my own personal use.

![Screenshot](/s/math-trainer/screenshot.png)
{{% /slide %}}

{{% learnings %}}
* The wiki was user-edited and had sporadic formatting issues (missing headers, incorrectly positioned footer), which I had to work around.
* I refactored my code structure multiple times to address issues of modularity, class inheritance structures, naming conventions, and documentation. This project taught me lots of best practices the hard way.
* I realized that I needed to optimize and minify code assets to reduce loading times, and eventually I learned how to do this by creating a custom Webpack configuration.
{{% /learnings %}}
