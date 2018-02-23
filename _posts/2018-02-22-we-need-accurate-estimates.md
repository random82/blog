---
layout: post
title:  Ok, but we need more accurate estimate
date:   2018-02-22 01:00:00 +1100
category: software delivery
tags: [agile, stats, estimates, delivery, project, management]
---

# We need more accurate estimates

## Why this range is so wide?

I guess that's something that most of us heard at least one time. We got a new work, we haven't clue about, we looked at a pile of work in front of us with no single point of reference and were asked about how long it's going to take. Regardless of the answer, there is one that is universally wrong and terrible and doesn't help anyone: **I don't know**

Most of us when working would need to give some estimates. I believe that we can always provide an estimate if we apply a method and in most cases we have more information about a situation that it seems in the first glance. Also, I've never met a single person who was interested in a single dollar accurate estimate. Doesn't matter if they came from waterfall or agile world, we always spoke ranges.

But sometimes, even if we have a clue or apply some estimation technique, the results might not be very compelling to your team or stakeholders.Especially when the estimate range comes wider than expected (sic!). Some people might offer you a witty advice to look at the work complexity and learn more about the requirements - but the complexity is only one of many factors that drives time and budget estimates. There are far many more variables and finding them and approximating can be done only by doing the work. That's also the best way to learn more about the complexity itself.

I'm a big fan of Monte Carlo simulations when it comes to estimation. Regardless if you apply Monte Carlo method or use other statistical method to provide a range of time which in most cases become a budget of a your project. And this range might come quite wide.

## _"A more accurate estimate"_

### Computer said - _"7 to 14 sprints"_

Let's walk through a sample scenario of estimating a delivery time of imaginary 46 user stories. We go through the backlog, do the relative sizing, run simulated sprint planning to get velocity distribution and plugging data into a simulation deck. We look with the hope on the screen and computer says - 7 to 14 sprints.

![Computer said 7 to 14 sprints](../img/2018-02-22-estimates/chance-deliver-stories.PNG)

What? 7 to 14 sprints? that's a wide range... and it will take a lot of explanation... We've checked the numbers, fixed few of them manually to look better. No changes. Probabilities moved slightly but the verdict remains - 7 to 14 sprints. We bring the result with the full story about our estimation method to client and what we hear is:

_-"That's nice... but... can you give us a more accurate estimate?"_

_-"Sure, we can do everything on the paper. The question is what do we want to achieve. Do you want me to tell you something that sounds nice so we can have few nights of sleep before the death march starts or should we talk about potential risks while we have time to react?"_

_-"But what if project sponsors don't agree?"_

_-"How about - what if project sponsors agrees and we miss the target by 100%?"_

_-"Oh...."_

### Beware of average

My stats teacher use to say - people keep drowning in lakes that are of 1m deep on avergae.

The big temptation in our situation is to figure out an acceptable contingency and narrow the range. Possibly bu using all the available power of a wishful productive group thinking. We could come with a reponse that will look like the one below if we tried really hard, right?

![A nice narrow estimate](../img/2018-02-22-estimates/chance-deliver-stories-smaller-range.png)

_-"Ah... 3 sprints range... now we're talking. Great job!"_

Hold on! What about the nasty tails of the estimate? Let's take a step back - when I told you that I'm going to deliver the scope we know today between 7 and 14 sprints what I was really saying was:

_-"I'm 99.999% confident the work will be done between 7 and 14 sprints"-_

when I narrowed the range I'm saying:

_-"I'm 61% confident the work will be done between 9 and 11 sprints"-_

_-"61%?! But that's not what we discussed!"_

_-"You wanted a nice and narrow estimate - there you go..."_

### What about the risk?

![40% risk on both sides](../img/2018-02-22-estimates/chance-deliver-stories-risk.png)

See the tails outside of the nice and narrow estimate - that's where remaining 39% sits, and guess what - that's a risk.

_-"What about the left side? You can finish earlier right?"_

![22% risk of not getting job done](../img/2018-02-22-estimates/chance-deliver-stories-risk2.png)

You're right, there is a 16% chance that it's going to happen according to the model. But fair enough, let's just talk about the right hand side only.

When I give you 3 sprints wide estimate around the average, we begin to bet on a game in which you can win in 4 out of 5 times. How much money could you put on that if I gave you only one chance? 

Let me demonstrate it differently.

![Cumulative chances](../img/2018-02-22-estimates/chance-deliver-stories-cummulative-risk.png)

If we missed the top bar of estimated time or budget, which can happen in 22% of times after sprint 11,there would be work not delivered. There are many ways of dealing with this situation, we could actually remove something from the scope, but for the sake of the argument, let's pretend the backlog consist only from must-have-compliance-or-we-get-sued items. Has to be delivered.

In a scenario like this I would look at the model differently. Instead of looking at chances or cumulative chances of delivering the scope, let's look at the risk of not delivering scope by sprint:

![Not delivering stories](../img/2018-02-22-estimates/chance-not-deliver-stories-cummulative.PNG)

Does it help with estimating chances? Even though average says we should deliver it in around 9 sprints - it's close to 50/50. How much money would you put on a flip-coin bet?

### Better narrow range?

One approach would be to move the nice narrow range to the right side (because we need to give ranges, right) and present an estimate 11 to 13 sprints with 4% of risk. Theoretically it's a nicer approach but in practice we're bloating the estimate in the old waterfall style: team says $X. Project manager (with experience) knows it will be closer to $2\*X and while project sponsor reaches for 4\*$X to the pocket because it's not the first time when the team and project manager got it wrong.

![Better narrow range](../img/2018-02-22-estimates/chance-deliver-stories-range-better.png)

### What to do?

Yes, we have an ugly, wide estimate. It doesn't make anyone happy and delivering such news is not easy. But we can deal with it.

First of all - don't be afraid of the ugly estimate - explain your estimation approach, complexity, known factors and potential sources of risks. There is alway a good opportunity to review both model and the method. If both of them pass the review, probably you'll end up with few more people on board and supporting you. Wise person wrote ***"Project management 101: bad news don't get better with time."*** Delivering ugly estimate is much easier in the beginning rather than end of the project.

Secondly - yes, today the estimate is ugly, but guess what, more we learn about the project, we can update it with actual values and it will become more narrow. It's might change it's parameters and move to the left or the right but with cycles short enough we will have enough time to react on these changes. Good news, it doesn't look like it's going to be longer than 14 sprints... There's only 0.0001% chance.

### And what about the scope creep?

What if the scope changes from 46 to say 60 stories?

Well the initial model tells you how much time you need to deliver 46 out of 60 stories in the original order. Also, it works at a any given point in time - by saying that, today we know about 46 stories and their initial priorities. When we add another 16 there are few possible scenarios:

- Add them to the tail - not very likely - in this scenario nothing changes in terms of the estimation done for the first 46 stories in the order we agreed on.

- Trade - likely when in fixed budget/time scenarios - we have to estimate complexity of the new scope and trade it for a part of similar complexity from the original scope

- We add and change priorities - almost every time - no problem, let's crunch the numbers one more time. That's the whole point, fixing estimates is like fixing a scope, doesn't help anyone. They have to be reviewed and monitored and updated to represent our best understanding of goals.

Regardless what is the scenario, it's much easier to engage in discussion when a model that tracks our estimates is implemented as part of the delivery process, in a similar way we implement a model that helpss tracking requirements in a form of a living artefact - a backlog.