+++
title = "Exploring Rails delegated_type"
date = "2024-05-09T22:00:00-04:00"
author = "alexb"
cover = ""
tags = ["ruby", "rails", "technical"]
description = ""
showFullContent = false
readingTime = false
hideComments = false
draft = false
+++


# Intro
Modeling data can be the most challenging part of creating a new app. In fact, it's been suggested that it's totally acceptable to -*not*- fail fast when scoping your schema. Getting your data modeled correctly from your `Initial Commit` can save you hours of refactoring.

I was recently prototyping a new greenfield application for work, and as I mapped out my models and how they'd be associated, I started to experience some friction.

Just when I'd found my preferred way to use ActiveRecord queries that read like natural language, I'd throw off the conventional readability of my `schema.rb`.

Going in and fixing the schema would undo some of my intuitive AR queries, or require some convoluted controller actions.

I came to the conclusion that all of this back-and-forth was due to Object-Relational Impedence Mismatch. Don't worry if you've never heard of it, we'll use an example app to demonstrate what it is and how Rails `delegated_types` offers a solution.

# Example App Domain

Let's imagine we're creating an app for a fancy new generative coding assistant called....

....drumroll.... 

```
  .o    .oooo.                              o8o 
o888   d8P'`Y8b                             `"' 
 888  888    888 oooo    ooo      .oooo.   oooo 
 888  888    888  `88b..8P'      `P  )88b  `888 
 888  888    888    Y888'         .oP"888   888 
 888  `88b  d88'  .o8"'88b   .o. d8(  888   888 
o888o  `Y8bd8P'  o88'   888o Y8P `Y888""8o o888o
```

`10x.ai` !! Did we just nail our seed funding pitch in a blog post? Just by shoehorning "AI" somewhere into our business name? I think so!

Don't worry about the AI aspect of it, sadly we'll just be focusing on the subscriptions and payments.


We'll support a `monthly`, a `yearly`, and a `lifetime` subscription.

Let's also allow for users to have `stripe` payments or `paypal` payments.

# Thinking About the Data
Starting with subscriptions, how could we handle storing these in the database and using them?

### class-table inheritance
We could create a parent class and have a separate table for each sub-class. That might require us to duplicate quite a handful of attributes. Perhaps each subscription would have an `is_active` attribute. We'd need that column on each of our tables, and any other shared attributes would also need to be repeated on each table. Writing clean and optimized queries could become difficult with all that repitition.

### single-table inheritance (sti)
We could also try to create one table of `Subscriptions` and maybe even use an [enum](https://api.rubyonrails.org/classes/ActiveRecord/Enum.html) to determine the type of subscription. This definitely gives us fewer tables to track down, but we have to persist *any* attribute of *any* subscription to this single table. This could lead to our `Subscriptions` having a load of attributes that aren't relevant to a specific instance, e.g, a lifetime subscription would have no need for the `end_date` column, and might even cause some bugs when its value is `nil`.


Let's digest these two approaches for a moment. We'll come back.

# What *IS* Object-Relational Impedence Mismatch?

#### from 10,000 feet -

[Object-relational impedence mismatch \(wikipedia\)](https://en.wikipedia.org/wiki/Object%E2%80%93relational_impedance_mismatch) describes how objects you create in your code don't fit easily into database rows and columns.

#### from a bit closer -

Using inheritance and building classes in OOP languages allows us to perform operations in a way that's fundamentally disparate from how we want to persist information into a database. Imagine a UML diagram vs. an Excel spreadsheet - they don't exactly play nicely with one another.

#### up close and personal, back to our example -

Using only the limited scope of our two humble tables, we can get into a very inelegant predicament in no time. Suppose we want to get the payment information for a single `YearlySubscription`. How would we know whether a customer used a `stripe` or `paypal` payment?

I sure would hate to check for `.stripe_payment.present?` or `.paypal_payment.present?` every time we wanted to view billing history.

There is a better way!

# Implementing `delegated_types`

[ActiveRecord's Delegated Types](https://api.rubyonrails.org/classes/ActiveRecord/DelegatedType.html) offers a way to manage shared behavior from a parent class like one would with OOP inheritance, while still allowing for unique "subclasses" in the form of separate models. The caveat here is that this approach will require a bit more hands-on manipulation of data.

Since delegated types help manage shared behavior, they fit nicely into the pattern of a Rails concern. Let's `delegated_type`-ify our subscription.


###### the `Subscription` "superclass" from which the delegated types are derived-
```ruby
# app/models/subscription.rb

class Subscription < ApplicationRecord
    has_many :payments # Also a delegated_type!
    delegated_type :subscribable, types: [ "MonthlySubscription",
                                           "YearlySubscription",
                                           "LifetimeSubscription"
                                           ]
    # And some optional syntactic sugar
    accepts_nested_attributes_for :subscribable

    def discounted_cost
        subscribable.discount_amount * cost
    end
end
```

###### the Subscribable concern
```ruby
# app/models/concerns/subscribable.rb

module Subscribable
    extend ActiveSupport::Concern

    included do
        has_one :subscription, as: :subscribable, touch: true
    end
end

```

###### and an example of one of the Sub...Subscriptions
```ruby
# app/models/monthly_subscription.rb

class MonthlySubscription < ApplicationRecord
    include Subscribable
    has_many :payments, through: :subscription

    def discount_amount
        .1
    end
end
```

###### creating a subscription
And finally to create a subscription we can use the `accepts_nested_attributes_for` to build our super and sub class at the same time:

```ruby
Subscription.create(start_date: Date.today,
                    is_active: true,
                    was_couponed: false,
                    subscribable: 
                        MonthlySubscription.create(
                            expires_on: (Date.today + 31.days)
                        )
                    )
```


# Putting it Into Practice
This let's us use all kinds of helpful associations and queries between parent classes where the implementation details of the subclasses aren't needed:

```ruby
# Oh no, the stripe API was down. Retry them all
# without bothering the paypal customers
Subscription.payments
            .stripe_payments
            .where(was_successful: false)
            .each(&:retry_failed)

# Payment type doesn't matter if we use the same
# delegated_type pattern on Payments
MonthlySubscription.first
                   .payments
                   .stripe_payments #=> [StripePayment<#foobar>, ...]

MonthlySubscription.last
                   .payments
                   .paypal_payments #=> [PaypalPayment<#bazquux>, ...]

# Discounts
Subscription.first.subscribable.discount_amount #=> .2 // YearlySubscription
Subscription.last.subscribable.discount_amount #=> .1 // MonthlySubscription
Subscription.first.discounted_cost #=> 10099 cents
Subscription.last.discounted_cost #=> 999 cents

# What type of subscription was this charge for?
Payment.last.subscribable_type #=> "LifetimeSubscription"
```

There are many more niceties that come with using `delegated_types` so it's a pattern worth checking out. In fact, there are still plenty of optimizations that could be done to this setup.

I would caution against using this approach as a first-resort, but I'm happy to use it on smaller apps where maintainers are very familiar with the codebase.

Again, the cost of implementing this pattern into your codebase is that you'll have to do a bit more managing of some classes and concerns, but the big win is keeping your code clean, readable, and intuitive - things Rubyists love.

### thanks
Thanks to Remi Mercier and his [delegated_types blog post](https://remimercier.com/delegated-types/). Reading through someone's thought process really helps build understanding for topics. Cheers!
37signals also has a thorough [blog post](https://dev.37signals.com/active-record-nice-and-blended/) about delegated types

