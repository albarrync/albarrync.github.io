+++
title = "Technical Book Review - Sustainable Dev Environments with Docker and Bash"
date = "2024-05-09T22:00:00-04:00"
author = "alexb"
cover = ""
tags = ["docker", "bash", "technical"]
description = ""
showFullContent = false
readingTime = false
hideComments = false
draft = false
+++

Another great book by David Bryant Copeland.

#### Where I had trouble in the past
I purchased the PragProg book [Docker for Rails Developers](https://pragprog.com/titles/ridocker/docker-for-rails-developers/) several years ago. It was good, but a little dated considering recent docker practices, and I shelved it after running into some speedbumps (*it used some webpack/er/ tooling that was hard for me to get running*).

Not too long after that, I ran into some issues with a friend's legacy app. I'll spare you the war story, but suffice it to say that we had a hard time getting MySQL 5.7 installed on either of our machines.

[@davetron5000](https://twitter.com/davetron5000) to the rescue!

#### Why I liked this book
In the era of memeDevs&trade;, David's carefully crafted philosophy on software and tools are a breath of fresh air.

This book does not go into great depth about Docker or Bash. These tools are chosen for their stability and longevity. You learn enough Docker to build a dev environment, and no more. You learn enough bash to write a few elegant, durable scripts and no more.

As with his book on Sidekiq, the real value lies in the amount of time DBC has spent crafting the sandbox you interact with and learn from. In this book, you'll do very little editing of the included sinatra app. More time is spent building up Docker chops,  starting from a humble `docker run ...` typed directly into your command line - to including a `docker compose` command in your bash scripts that can run in any directory.

#### Key Takeaways
* Chain of Trust

There is a refrain throughout the book of "establishing a chain of trust". While it may seem obvious, he encourages the reader to source and cite reputable resources. This plays out mostly for selecting Docker images. Now that LLM's are generating prompt answers with such high levels of confidence, it's more important than ever to scrutinize the choices we're making.

* Your Dev Environment should be a Core Competency

This whole chapter is replete with examples of why it's so important to be deliberate about your tools. I actually plan on printing out the chapter in its entirety so the next time someone asks why I'm not using a new IDE with Telemetry and Logins (WHY?), I can just hand them these three pages. Assuming there aren't any major changes with computer interfaces any time soon, Vim, Bash, and Docker will remain useful and universally available.


Buy it! It's not expensive!

[Sustainable Dev Environments with Docker and Bash](https://devbox.computer/)
