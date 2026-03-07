---
title: 'AI-Augmented Product Teams: 9 Months In'
description: 'We have been running AI-augmented product development seriously for nine months. Here is what actually changed, what did not, and what I wish I had done differently.'
heroImage: '/images/blog/ai-product-teams-01.jpg'
heroAlt: 'AI augmented teams'
pubDate: 'Nov 28 2023'
---

In March 2023 I wrote about how LLMs were changing my individual engineering process. Nine months in, the scope of the experiment has expanded: we've been systematically integrating AI tools across the product team — engineering, design, product management, and support.

This is what actually happened.

![Team collaborating around laptops with data visualizations on screen](/images/blog/2023-11-ai-augmented-product-teams-inline-01.jpg)
*Nine months of systematic AI integration across engineering, design, PM, and support*

## Engineering: Where the Gains Were Real

The productivity gains in engineering were real and measurable. We track features delivered per sprint, time from PR open to merge, and critical bug escape rate. After removing confounds:

- Feature delivery velocity: up ~35% from pre-AI baseline
- Code review cycle time: down ~25% (AI-assisted review flagging obvious issues early)
- Bug escape rate: no significant change, which was actually a concern (more on this)

The 35% velocity number gets people excited. The flat bug escape rate deserves more attention. We're shipping more features faster, but we're not shipping more correct features faster. The LLM assistance is happening mostly at the "write the code" layer, not the "ensure the code is correct and the design is right" layer.

This is an important distinction. Speed without quality is debt, not progress.

> Feature delivery velocity up **~35%**. Bug escape rate: **unchanged**. We're shipping more features faster — but not more *correct* features faster. Speed without quality is debt, not progress.

## Product Management: The Interesting Case

I didn't expect AI to matter much for product management. I was wrong.

The biggest impact was in synthesis work — taking large amounts of user feedback, support tickets, and usage data and extracting signal. Before: a PM would spend 3-4 hours reading through feedback, tagging themes, synthesizing into a document. After: the LLM does an initial synthesis pass in 10 minutes, the PM spends 45 minutes validating, challenging, and adding context that the LLM missed.

The LLM misses things that require domain knowledge or contextual judgment that's hard to articulate. But it catches patterns across large datasets faster than any human. The combination is better than either alone.

Where AI didn't help in PM: strategic prioritization, stakeholder alignment, and understanding the political dynamics of what gets built and why. These require human judgment, relationships, and organizational context that LLMs don't have.

![Data analyst reviewing patterns and insights on a large display](/images/blog/2023-11-ai-augmented-product-teams-inline-02.jpg)
*AI catches patterns across large datasets faster than any human — but the PM still provides the judgment the model can't*

## The Skill Distribution Question

The single most interesting observation from nine months: AI tools are compressing the skill distribution in our team.

Senior engineers' absolute advantage in certain tasks has decreased. Tasks that used to take a senior engineer 2 hours and a junior engineer 8 hours now take the senior engineer 1 hour and the junior engineer 2 hours. The senior is still faster, but the gap has narrowed.

This is good for some things: junior engineers are more productive, more capable, more confident. The floor has risen.

It creates challenges too. The tasks that remain clearly senior-level are fewer and less clearly defined. The signaling that used to distinguish seniority — typing speed, pattern memorization, syntax fluency — matters less. What remains is judgment, system thinking, and the ability to evaluate whether LLM-generated solutions are actually good.

We haven't fully worked out the implications for career development. How do you develop judgment if you skip the years of lower-level practice that used to build it? I don't have a good answer yet.

![Mentor and junior developer pair programming at a workstation](/images/blog/2023-11-ai-augmented-product-teams-inline-03.jpg)
*The tasks that remain clearly senior-level are fewer — what distinguishes seniority now is judgment, not syntax fluency*

## What I'd Do Differently

**Start evaluation frameworks earlier.** The quality assurance infrastructure should have been built before we let AI accelerate shipping velocity, not after.

**Be more explicit about "where AI is and isn't helping."** We talked a lot about AI tools in general without being specific about which tools, for which tasks, with which quality bar. More precision earlier would have reduced confusion.

**Spend more time on the judgment development question.** We got good at using AI to do tasks faster. We spent less time thinking about how to develop the judgment to evaluate AI output well. That's a gap I'm still working on.

The experiment continues. The team is more capable than it was a year ago. The nature of "more capable" has changed in ways I'm still figuring out.
