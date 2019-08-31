---
title: Euler Project - Problem 1
date: '2009-10-09T12:34:00+05:30'
tags:
- misc
tumblr_url: https://sureshshanmugam.com/post/208243701/euler-project-problem-1
---

```ruby
# Project Euler: Problem 1
# Use Module:Enumerable
# Sum some numbers (5..10).inject { |sum,n| sum+n }
# find the sum of all multiples of 3 and 5 below 1000
puts (1...1000).select { |n| n % 3 == 0 or n % 5 ==0 }.inject { |sum,n| sum+n }
```
