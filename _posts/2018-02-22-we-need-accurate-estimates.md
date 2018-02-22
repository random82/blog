---
layout: post
title:  Ok, but we need more accurate estimate
date:   2018-02-22 01:00:00 +1100
category: software delivery
tags: [agile, stats, estimates, delivery, project, management]
---

# We need more accurate estimates

## Why this range is so wide?

I guess that's something that most of us heard at least one time. We looked at a pile of work with no point of reference and were asked about how long it's going to take. There is an answer which is always wrong and doesn't help anyone: **I don't know**

But sometimes even if we have a clue or apply some estimation technique the results might not be very compelling to your team or stakeholders when the estimate range comes wider than expected (sic!). Some people will come with a witty advice to look at the work complexity - but complexity is only one factor that drives time and budget estimates. There are far more variables and finding them and approximating can be done only by doing the work.

I'm a big fan of Monte Carlo simulations when it comes to estimation. Regardless if you apply Monte Carlo method or use other statistical method to provide a range of time that, in most cases, become a budget of a project or initiative, the range might come quite wide.

Recently I was in the situation when the most accurate estimate I was able to offer was between 7 and 14 sprints. Correct, I could be off twice. That's asking customer: _"I'll need between N and 2*N dollars to get the backlog finished"_. Also, it's a fixed scope job that adds its own twist to the whole story.

Probably, something like _"hold on, that's if you assume there are no changes to backlog"_ might cross your mind. Yeah, fixed scope jobs can bite both ways.

## _"A more accurate estimate"_

### Computer said - _"7 to 14 sprints"_

Let's walk through a sample scenario. I put numbers to my simulation deck and computer said it will take between 7 to 14 sprints to deliver agreed scope.

![Computer said 7 to 14 sprints](..\img\2018-02-22-estimates\chance-deliver-stories.PNG)

Yup, that's a wide range and it takes a lot of explanation why it comes to that. Regardless of the reasons - it is what it is..

_-"but can you give us a more accurate estimate?"_

Sure, we can do everything on the paper. The question is what do we want to achieve.

### Beware of average

My stats teacher use to say - people get drowned in an average of 1m depth lakes.

The big temptation in our situation is to ask a question about the level of acceptable contingency and narrow the range using all possible powers of a wishful productive group thinking. It would look something like that:

![A nice narrow estimate](..\img\2018-02-22-estimates\chance-deliver-stories-smaller-range.PNG)

_-"Ah... 3 sprints range... now we're talking. Great job!"_

Hold on!

What about the nasty tails of the estimate? Let's take a step back - when I told you that I'm goping to deliver the scope between 7 and 14 sprints what I was really saying was:

_-"I'm 99.999% confident the work will be done between 7 and 14 sprints"-_

when I narrowed the range I'm saying:

_-"I'm 61% confident the work will be done between 9 and 11 sprints"-_

_-"61%?! But that's not what we discussed!"_

_-"You wanted a narrow estimate - there you go..."_

### What about the risk?

![40% risk on both sides](..\img\2018-02-22-estimates\chance-deliver-stories-risk.PNG)

See the tails outside of the nice and narrow estimate - that's where remaining 39% sits, and guess what that's a risk.

_-"What about the left side? You can finish earlier right?"_

![22% risk of not getting job done](..\img\2018-02-22-estimates\chance-deliver-stories-risk2.PNG)

You're right, there is a 16% chance that it's going to happen, but fair enough, let's just talk about the right side - when I give you 3 sprints wide estimate around the average, we started to bet and you can win in 4 out of 5 games. Let me demonstrate it differently.

![Cummulative chances](..\img\2018-02-22-estimates\chance-deliver-stories-cummulative-risk.PNG)

If we missed the top bar of estimated time or budget, which can happen in 22% of times after sprint 11. There will be part of ork not delivered. There are many ways of dealing with this situation, we could actually remove something from the scope, but for the sake of the argument, let's pretend the backlog consist only from must-have-compliance-or-we-get-sued items. Has to be delivered.

In a scenario like this I would look at the model differently. Instead of looking at chances or cumulative chances of delivering the scope, let's look at the risk of not delivering scope by sprint:

![Not delivering stories](..\img\2018-02-22-estimates\chance-not-deliver-stories-cummulative.PNG)

Does it help with estimating chances? Even though average says we should deliver it in around 9 sprints - it's close to 50/50. How much money would you put on a flip-coin bet?

### Better narrow range

![Better narrow range](..\img\2018-02-22-estimates\chance-deliver-stories-range-better.PNG)