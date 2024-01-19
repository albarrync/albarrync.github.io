+++
title = "Technical Book Review - Ruby on Rails Background Jobs with Sidekiq"
date = "2024-01-19T17:00:00-04:00"
author = "alexb"
cover = ""
tags = ["rails", "ruby", "sidekiq", "technical"]
description = ""
showFullContent = false
readingTime = false
hideComments = false
draft = false
+++


I recently picked up a short technical book by David Bryant Copeland to help understand Sidekiq a little better.
TL;DR - The dev environment made it the most efficient technical book I've ever read.

## Dev Setup
Technical books will never be the same for me.
Initially, I ran into a few issues with the docker compose setup. After very luckily finding [the forum post where Copeland himself responds and updates](https://forum.devtalk.com/t/bug-with-dx-build-how-to-workaround-until-fix-is-up/116612), I was able to get the environment setup. 

It was fantastic~

I believe the app you work on is running rails, and the mock app runs on a simple Sinatra server. The real beauty is that if your docker compose works, you get Redis, Sidekiq(after one setup step done manually for illustration), and a few other items for the whole ecosystem. It's rare for me to read a tech book with disparate services that has no friction after setup. The elegant architecture made it really easy to focus on learning and absorbing the concepts, and not worry about service versions.

## Technical Depth
The book itself is short and to-the-point, but I found it to be a perfect balance for what I needed. I learned quite a bit of material, significant information, even though I have setup and worked on Sidekiq and Redis before. I really enjoyed the way that the book presented a realistic problem, and walked you through how to practically solve it - instead of just saying "This is how Sidekiq works."

At a very digestible 64 pages, I will have no reservations about suggesting this book to absolutely anyone who dare mention "Sidekiq".
I really wish DBC would make a book exactly like this for all the main Rails-adjacent services.

## Takeaways

A well-written and informative book that you can finish in a weekend. I loved the perspective on practicality and the condensed pace.
It felt just like a good pairing session with an expert.

Favorite quote from the book:
> Not all tests are worth writing

Definitely worth your time!
[Buy on PragProg](https://pragprog.com/titles/dcsidekiq/ruby-on-rails-background-jobs-with-sidekiq/)


