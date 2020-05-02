---
title: "Publishing Jupyter Notebooks on Github Pages"
category: articles
tags:
 - jupyter
 - ml
---

## Publishing Jupyter Notebooks on GitHub

### Converting Jupyter notebooks into markdown

I've been looking for ways to publish Jupyter notebook based analysis into this blog. This post explains a process that I've come to use in creating these blog posts.

This method allows inclusion of styled cell input and output, including graphs. Whe you have completed your iPython notebook (sample_notebook.ipynb in this case), run the following command in your terminal to convert your notebook file into markdown.

```sh
$ jupyter nbconvert sample_notebook.ipynb --to markdown

```

### Add markdown to Jekyll

For notebooks with text and code this approach works fine. There are couple more steps to get images and plots incorporated into these posts. The Markdown doc expects these PNGs so be in the same folder as the doc, but Jekyll works with a separate /assets/... folder, as is more common for websites. It would need a some scripting to fix this path difference. I also do like the Jupyter Notebook style, so it would be nice not to go through Markdown and lose all that.

