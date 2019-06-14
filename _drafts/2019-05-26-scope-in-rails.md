---
layout: post
title: Scope in rails.
subtitle: Why we should use Scope instead of class method in rails.
tags: [rails]
---

Rails follows DRY principle of software development and that is 'Don't Repeat Yourself'.
Scopes is are great to to keep our code DRY and well organized. It's just a set of pre-define SQL queries which we can use to write complex queries.

Suppose we want fetch users which have status `active`. So, we can simply write following query

```ruby

def index
	@active_users = User.where(status: "active")
end
```

But we may need to re-use this code multiple times in our project. So insted of writing same code again and again we can define scope for it.

```ruby
class user < ActiveRecord::Base
	scope :active, -> { where(status: "active") }
end
```

Now, we can simply use active scope to fetch all active users as following:

```ruby 
def index 
	@active_users = User.active
end
```

## we can also use parameter with scope

define scope as following

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

## Scopes Are Chainable

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

## How exactly scope works in rails 

look at the active scope once again

```ruby
class user < ActiveRecord::Base
	scope :active, -> { where(status: "active") }
end
```
we can write same thing in the class method as following:

```ruby

def self.active
  User.where(status: "active")
end
```

Basically instead of writing class method scope is syntactical suger for for writting queries.