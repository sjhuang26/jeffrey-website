---
title: Easy HTML Editor
link: https://easyhtmleditor.netlify.com/
code_link: https://github.com/sjhuang26/html-editor
timeframe: 10th grade
team: mostly me
status: not-ongoing
description: online HTML tutorial for beginners
---
{{% slide %}}
Easy HTML Editor is an online HTML tutorial for beginners.

![Screenshot](/s/easy-html-editor/screenshot.png)
{{% /slide %}}

{{% slide %}}
There are ~10 pages in the tutorial, which teach the basics of HTML.

![Screenshot of tutorial panel](/s/easy-html-editor/tutorial-panel.png)
{{% /slide %}}

{{% slide %}}
Tutorials contain example code that can be modified in the code editor.

![Screenshot of examples panel](/s/easy-html-editor/examples-panel.png)
{{% /slide %}}

{{% slide %}}
Interactive line-by-line explanations can be activated for any code the user enters by clicking "show explanation" in the code editor. When a tag is clicked in the explanation, a definition with examples appears in the bottom panel.

![Screenshot of interactive explanations feature](/s/easy-html-editor/explanation-panel.png)
{{% /slide %}}

{{% learnings %}}
* It's important to make sure that the website layout is reasonably robust to screensize changes and long pages of content. My previous projects often had major layout bugs, so this time I wrote  my own collection of CSS utilities to handle flexbox layout, which is used by marking certain parts of the page as "h-layout", "v-layout", etc. This makes the layout cohere much better.
* I needed to write a clear spec for the project, articulating my ideas clearer than usual.
* Overall, it required careful planning to make sure that the code architecture during the prototyping stages was extendable to a variety of more advanced tutorial features in the future.
{{% /learnings %}}
