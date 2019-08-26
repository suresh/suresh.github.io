---
title: "Analysis using Notebooks"
description: 
layout: post-no-feature
tags:
- ml
category: articles
---

## Here are some reasons why you might want to keep an analysis notebook

* To provide yourself with a complete record of why experiments were initiated and how they were performed. You'll forget if you don't. Seriously, even in your youth your brain cells are fading, and even the exciting moments of your science will fade.* 
* To give yourself a central, physical place to record your data, to note statistical outcomes, and to paste graphs that show results. Data scientists who jot notes on Post-Its, paper towels, and palms are unlikely to be effective in the laboratory.
* To encourage sound thinking. Keeping a notebook gives you a forum to talk to yourself – to ask questions, to record important thoughts about the experimental design, and to speculate how your results might eventually be interpreted.
* To provide information to a person who is interested in continuing your research project, even if you deem that possibility hilariously unlikely. And if you're doing important research and die an early, gruesome death, your lab-mates might want to pick it up. 
* To get rich. Not everyone sets out with the goal of patenting a process or contraption, but you might stumble onto something actually important, and in such an event you must have a notebook that supports your claims. Your competitor in court will.

## What should go into your notebook:

* Include detailed notes on all discussions and thoughts on the experimental goals. This means, of course, that you should start making dated entries immediately rather than waiting until you get your experiments started. 
* Ensure each notebook has descriptive title, an evocative filename, and a first paragraph that briefly describes the aims of the analysis.
* Use the YAML header date field to record the date your started working on the notebook. Use ISO8601 YYYY_MM_DD format so that’s there no ambiguity. Use it even if you don't normally write dates that way.
* If you spend a lot of time on an analysis idea and it turns out to be a dead end, don't delete it. Write up a brief note about why it failed and leave it in the notebook. That will help you avoid going down the same dead end when you come back to the analysis in the future.
* Generally, you're better off doing data entry outside of R. But if you do need to record a small snippet of data, clearly lay it out.
* If you discover an error in a data file, never modify it directly, but instead write code to correct the value. Explain why you made the fix.
* Before you finish for the day, make sure you can knit the notebook (if you're using caching, make sure to clear the caches). That will let you fix any problems while the code is still fresh in your mind.
* If you want your code to be reproducible in the long-run (i.e. so you can come back to run it next month or next year), you'll need to track the versions of the packages that your code uses. A rigorous approach is to use packrat which store packages in your project directory, or checkpoint which will reinstall packages available on a specific date. A quick and dirty hack is to include a chunk that runs sessionInfo() - that won't you let easily recreate your packages as they are today, but at least you'll know what they were.
* You are going to create many analysis notebooks over the course of your career. How are you going to organize them so you can find them again in the future? I recommend storing them in individual projects, and coming up with a good naming scheme.
