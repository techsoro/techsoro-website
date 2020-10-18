---
layout: post
title: Scope in rails.
subtitle: Why we should use Scope instead of the class method in rails.
tags: [Rails]
author: Shekhar Patil
comments: true
---

Rails follow the DRY principle of software development and that is 'Don't Repeat Yourself'.
Scopes is are great to keep our code DRY and well organized. It's just a set of pre-defined SQL queries that we can use to write complex queries.

Suppose we want to fetch users who have status `active`. So, we can simply write the following query

```ruby

def index
  @active_users = User.where(status: "active")
end
```

But we may need to re-use this code multiple times in our project. So instead of writing the same code, again and again, we can define a scope for it.

```ruby
class user < ActiveRecord::Base
  scope :active, -> { where(status: "active") }
end
```

Now, we can simply use an active scope to fetch all active users as following:

```ruby
def index
  @active_users = User.active
end
```

## 1. Scope with parameter.

we can give parameters to scope.

```ruby
class Fruit < ActiveRecord::Base
  scope :color, -> (color_name){ where(color: color_name) }
end
```
now in our Fruit controller we can use

```ruby
def Index
  @red_fruits = Fruit.color("red")
  @yellow_fruits = Fruit.color("yellow")
end
```

## 2. Scopes Are Chainable

This is really interesting and it makes scope even more useful.

```ruby
class User < ApplicationRecord
  scope :active, -> { where(status: "active") }
  scope :recent, -> { where('created_at < ?', 1.week.ago }
end
```

we can use it in the controller as following;

```ruby
def index
  @users = User.active.recent
end
```

## 3. How exactly scope works in rails

look at the active scope once again

```ruby
class user < ActiveRecord::Base
  scope :active, -> { where(status: "active") }
end
```
we can achieve the same result using the following class method as given. Basically, instead of writing class method scope is syntactical sugar for writing queries.

```ruby

def self.active
  User.where(status: "active")
end
```

I would love to hear some of the interesting topics related to rails which I can explore and write a blog about it on [Twitter](https://twitter.com/Shekharpatil95).

Cheers!
