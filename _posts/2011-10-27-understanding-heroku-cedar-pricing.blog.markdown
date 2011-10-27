---
layout: post
title: Understanding Heroku's Cedar Pricing Scheme
tags: heroku
summary: Recently I have read a lot about Heroku's new "Celadon Cedar" stack. For the most part people are happy about the flexibility the new stack gives developers. However, one new characteristic that strikes a nerve with loyal users is the pricing scheme that comes along with it. Here is why it's not as bad as you think it is (and why it's actually better).
---
Recently I have read a lot about Heroku's new "Celadon Cedar" stack. For the most part people are happy about the flexibility the new stack gives developers. However, one new characteristic that strikes a nerve with loyal users is the pricing scheme that comes along with it. Here is why it's not as bad as you think it is (and why it's actually better).

Before cedar, Heroku was known for being a free hosting platform for Ruby on Rails apps. Each deployed app automatically got a free web service "dyno". If a developer wanted to run any sort of worker, however, they would have had to pay for each additional "worker dyno".  With the new process model that is implemented in the new stack, a new pricing scheme had to be developed. So instead of charging for whole web and worker dyno's, Heroku started charging by aggregated, elapsed runtime, prorated to the second. This means you only get charged for the summation of the time that all your processes are running (You can start and stop processes by using the new scaling function). 

To continue with the free model that Heroku is known for, each app is given 750 hours a month of runtime free. However, running common tasks such as `rake db:migrate` or using the rails console now count as "one off" processes. This means that technically, the runtime of each of these tasks counts towards your bill. Here in lies the supposed problem that people are complaining about.

> You mean I have to pay to migrate by DB?!?!?

What many people fail to realize is that 750 hours is more than what's needed for a process to run non-stop for a month. During the longest month of 31 days, you only need 744 hours. Which means the 10-15 seconds a month that you run "rake db:migrate" is still free!  What this also means is that if you micromanage your worker process' runtime, you can actually get a free worker too! (i.e. scale your worker to 0 when not in use.)