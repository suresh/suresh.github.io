---
layout: single
title: "Generating blog posts from Jupyter notebooks"
description: "Github pages based jekyll blog posts from jupyter notebooks"
toc: true
toc_label: "In this page"
toc_icon: "cog"
category: articles
tags: [readability]
---
#

I've been looking for ways to incorporate Jupyter notebooks into this blog. This post explains a process that I've come to use in creating these blog posts.

This method allows inclusion of styled cell input and output, including graphs. Whe you have completed your iPython notebook (sample_notebook.ipynb in this case), run the following command in your terminal to convert your notebook file into markdown.

```bash
jupyter nbconvert sample_notebook.ipynb --to markdown
```
