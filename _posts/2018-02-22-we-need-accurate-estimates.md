---
layout: post
title:  Ok, but we need more accurate estimate
date:   2018-02-22 01:00:00 +1100
category: software delivery
summary: We need more accurate estimates - dealing with wide an ugly estimate
tags: [agile, stats, estimates, delivery, project, management]
---

# We need more accurate estimates

## Why this range is so wide?

This is something that most of us have heard at least one time. We received new work, we haven't a clue about it, we looked at the pile of work in front of us with no single point of reference, and have been asked how long it would take. Regardless of the answer, there is one that is universally wrong and terrible, and doesn't help anyone: **I don't know**

Many of us are often requested to provide some estimates to help people understand how much time or money they will need to invest. Regardless of how bad the intial situation might seem, I believe that we can always provide an estimate - there are estimation methods we can apply, and usually we have more information about the work that we thought we had. I also haven't met anyone who was interested in down-to-the-dollar accurate estimate. It doesn't matter whether they've come from waterfall or agile world, we always spoke in ranges.

But even if we have a good understanding and apply an estimation technique, the results might not be very compelling to our team or stakeholders, especially when the estimate range comes in wider than expected (sic!). Some people might offer you witty advice to look at the work complexity and learn more about the requirements, but the complexity is only one of many factors that drive time and budget estimates. There are far more variables, and uncovering and approximating them can be only achieved by doing the work - this is also the best way to learn more about the complexity itself.

I'm a big fan of Monte Carlo simulations when it comes to estimation. Regardless of whether you apply Monte Carlo or another statistical method, you're most likely going to end up providing a time range. In most cases, this range will become the basis for your project budget, and this range might come in quite wide.

## _"A more accurate estimate"_

### Computer said: _"7 to 14 sprints"_

Let's walk through a sample scenario of estimating a delivery time for 46 imaginary user stories. First, we go through the backlog, do the relative sizing, run simulated sprint planning to get velocity distribution and plug data into a simulation model. We look with hope at the screen, and the computer says - 7 to 14 sprints.

![Computer said 7 to 14 sprints](../img/2018-02-22-estimates/chance-deliver-stories.PNG)

What? 7 to 14 sprints? That's a wide range... and it will take a lot of explanation... We've checked the numbers, fixed a few of them manually to make them look better. No changes. The probabilities moved slightly, but the verdict remains - 7 to 14 sprints. We bring the result and the full story about our magnificent, yet slightly overwhelming estimation method to the client, and what we hear is:

_-"That's nice... but... can you give us a more accurate estimate?"_

_-"Sure, we can do everything on paper. The question is what do we want to achieve. Do you want me to tell you something that sounds nice so we can have few nights of sleep before the death march starts or should we talk about potential risks while we have time to react?"_

_-"But what if project sponsors don't agree?"_

_-"How about - what if project sponsors agrees and we miss the target by 100%?"_

_-"Oh...."_

### Beware of the average

My stats teacher used to say - _'People keep drowning in lakes that are 1m deep on average.'_

The big temptation in our scenario is to figure out an acceptable contingency and narrow down the range near the average (possibly by using all the available power of wishful productive group thinking). We could return with a response that looks like the one below if we tried really hard, right?

![A nice narrow estimate](../img/2018-02-22-estimates/chance-deliver-stories-smaller-range.png)

_-"Ah... 3 sprints range... now we're talking. Great job!"_

Hold on! What about the nasty tails on both sides of the estimate? Let's take a step back - when I told you I'm going to deliver the scope between 7 and 14 sprints, what I was really saying was:

_-"I'm 99.999% confident the work, as we know it today, will be completed between 7 and 14 sprints."-_

And when I narrowed down the range, I'm saying:

_-"I'm 61% confident the work will be done between 9 and 11 sprints."-_

_-"Only 61%?! But that's not what we discussed!"_

_-"You wanted a nice and narrow estimate - there you go..."_

### What about the risks?

See the tails outside of the nice and narrow estimate - that's where remaining 39% sits, and guess what - that's a risk.

![40% risk on both sides](../img/2018-02-22-estimates/chance-deliver-stories-risk.png)

_-"What about the left side? You can finish earlier right?"_

You're right, according to the model there is a 16% chance that it's going to happen. But fair enough, let's just talk about the right hand side.

![22% risk of not getting job done](../img/2018-02-22-estimates/chance-deliver-stories-risk2.png)

When I give you a 3 sprints wide estimate around the average, we're betting on a game in which you can win 4 out of 5 times. How much money would you put on that if I only gave you one chance?

Let me demonstrate it in a different way.

![Cumulative chances](../img/2018-02-22-estimates/chance-deliver-stories-cummulative-risk.png)

If we missed the top bar of our estimated time or budget, which can happen 22% of the time after the 11th sprint, part of the work would not be delivered. There are many ways of dealing with this situation - we could actually remove something from the scope - but for the sake of the argument, let's pretend the backlog consists only of must-have-compliance-or-we-get-sued items. The scope has to be delivered.

In a scenario like this I would look at the model differently. Instead of looking at chances or cumulative chances of delivering the scope, I would look at the risk of not delivering the scope by each sprint:

![Not delivering stories](../img/2018-02-22-estimates/chance-not-deliver-stories-cummulative.PNG)

How does it help with understanding the chances? According to our nice and narrow estimate, there is still a 22% chance we won't finish the project on time. And even though the average says we should deliver in approximately 9 sprints, it's close to 50/50. How much money would you put on a coin-flip bet?

### Better narrow range?

One approach would be to move the nice narrow range to the right side (because we need to give ranges, right) and present an estimate 11 to 13 sprints with a 4% risk. Theoretically, it's a better approach, but in practice we're bloating the estimate in true waterfall fashion: Team says $X; project manager (with experience) knows it will be closer to $2\*X while project sponsor reaches for 4\*$X to the pocket because it's not the first time when the team and project manager has gotten it wrong.

![Better narrow range](../img/2018-02-22-estimates/chance-deliver-stories-range-better.png)

### What to do?

Yes, we have an ugly, wide estimate. It doesn't make anyone happy and delivering such news is not easy. But we can deal with it.

First of all, don't be afraid of the ugly estimate - explain your estimation approach, complexity, known factors and potential sources of risks. There is always a good opportunity to review both the model and the method. If both of them pass the review, you'll probably end up with few more people on board, ready to support you. A wise person once wrote ***"Project management 101: bad news doesn't get better with time."*** Delivering an ugly estimate is much easier in the beginning rather than end of the project.

Secondly. Yes, today the estimate is ugly, but guess what, as we go through the project, we learn more about it. Base on this we can update the estimate with actual values and it will become more accurate (yay!). With cycles short enough, we will have enough time to react on these changes. Good news, it doesn't look like it's going to be longer than 14 sprints... There's only 0.0001% chance.

### And what about the scope creep?

What if the scope changes from 46 to 60 stories?

Well the initial model tells how much time we need to deliver 46 out of 60 stories in the original order. Also, it works at any given point in time - by saying that, today all we know is we have 46 stories in their initial priorities. When we add another 16 there are a few possible scenarios:

- Add them to the tail - not very likely - in this scenario nothing changes in terms of the estimation  for the first 46 stories in the order we agreed on.

- Trade-in/out - likely for fixed budget/time scenarios - we have to estimate complexity of the new scope and trade it for a part of similar complexity from the original scope

- We add and change priorities - almost every time - no problem, let's crunch the numbers one more time. That's the whole point, fixing estimates is like fixing a scope - it doesn't help anyone. They have to be reviewed, monitored and updated to represent our best understanding of the goals.

Regardless what your scenario is, it's much easier to engage in a discussion when you have a model that tracks your estimates, and it is implemented as part of the delivery process. In a similar way we are  implementing a model that helps track requirements in a form of the living artefact - a backlog.
