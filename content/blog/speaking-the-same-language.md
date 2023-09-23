+++
title = "Speaking the Same Language (Model)"
date = "2023-06-05T22:19:23-04:00"
author = "alexb"
cover = ""
tags = ["ai", "ide", "copilot"]
description = ""
showFullContent = false
readingTime = false
hideComments = false
+++

Most of the consensus around AI pair programming lately has been that it's not worth your time.
Bertrand Meyer [put it pretty bluntly](https://cacm.acm.org/blogs/blog-cacm/273577-ai-does-not-help-programmers/fulltext) regarding ChatGPT. Perhaps in the narrow scope of his use-case it didn't help him, but I've already seen plenty of evidence to the contrary.

## What it's Not (Yet?)
Copilot and ChatGPT haven't yet formulated a business idea, created an MVP, deployed it, and garnered seed revenue for scaling. Oh wait, [they absolutely have](https://mashable.com/article/gpt-4-hustlegpt-ai-blueprint-money-making-scheme). Snark aside, many of the most talented and well-respected minds in software seem to have a major blindspot when it comes to AI's capabilities with code. The LLM's we're using are still superpowered sentence finishers, so they're predictably off-target when solving high-complexity prompts. In the case of Bertrand above, even though a binary search is a relatively-simple algorithm, it's still a level of complexity that our current models will answer incorrectly plenty. Missing the forest for the trees in his example though, I think Bertrand has already taken for granted that he's chatting back and forth with a language model about some code he wrote. Imagine traveling back in time just a few years ago, and telling developers they'd be able to use [SmarterChild's](https://en.wikipedia.org/wiki/SmarterChild) cousin to help them hack. It'd sound pretty outlandish.

## What it is
- ChatGPT and Copilot remove the most terrifying barriers of software.
If you've ever tried to explain your pet project to an even mildly-interested friend or coworker, you know how quickly you can either start speaking Greek or put them to sleep. Software can be intimidating, which is why most people think we have superpowers. Several of my coworkers have been able to ship small projects that they were completely stuck on with the help of a language model's explanation. It's amazing to think how accessible low-complexity code will be to everyone with an internet connection.

- ChatGPT is great for helping Junior-level engineers access Mid-level knowledge.
Whether it's explaining a SQL statement, getting different approaches to new challenges, or just writing CSS rules, LLM's are like a personal Slack channel for any given discipline that is always willing to help.

- Copilot is great for autocomplete and discovery.
The amount of time I save just in character entry is enough justification for the subscription price of Copilot. If I write a method that removes an attribute from an object, Copilot is pretty fantastic about inferring the opposite adding method.
It's also great for suggesting elegant methods and approaches in my code that I wouldn't have otherwise uncovered. A great way to test this is to get Copilot running in your IDE of choice, and try some [Exercism problems](https://exercism.org/). You'll run into some cool ones like Ruby's `each_line` String method that splits a string into an Array on `\n` characters. Contrived example below. I like #2.

{{<highlight ruby>}}
my_haiku = "Unending wisdom,\n
            ChatGPT's eternal aid,\n
            Indispensable."
#1
my_haiku.split("\n").each{ |line| line.validate_syllables }

#2
my_haiku.each_line(&:validate_syllables)
{{</highlight>}}


## What it will be
In the coding space, retrieval and augmentation will be the ultimate productivity increase. For engineers that spend their time in codebases implementing feature requests, an augmented model will be able to keep entire projects in their "attention" span. This will be like combining the best parts of ChatGPT and Copilot. Instead of just getting suggestions for methods in context, your AI pair can tell you how to relate your many `ToDo`'s to one `ToDoList`. [Copilot X](https://github.com/features/preview/copilot-x) will be a near-future option, but [Sourcegraph's Cody](https://about.sourcegraph.com/cody) already exists if you're champing at the bit.

## Summary
To say nay on AI for coding seems a bit out-of-touch to me. We're less than a year in, and already have tangible value-generating benefits. Whether you think it's going to replace your job is up for debate, but there is no doubt that AI pairs are here for the long haul.
