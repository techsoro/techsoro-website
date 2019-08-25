---
layout: post
title: Singleton method in the ruby
subtitle: How to use a Singleton method in the rails. 
tags: [Ruby]
author: Shekhar Patil
comments: true
---

Today I attend Ruby Conference at Pune and Singleton method and metaclass in ruby was one of the talk discussed there So, I thought to write a blog about it.

In ruby, we create the class and class has many methods written into it. When we create an object of the class we can access those methods using that object. So, the question raise in my mind was as follows.

### 1. Who holds these methods? does class hold these methods or each object of the class holds this methods? 

Let us find it out.

```ruby
class User
  def role
    puts "Admin"
  end
end

user = User.new
user.role         // Admin

class User
  def role
    puts "sales"
  end
end

user.role         // sales
```

As we can see we have overridden the `User` class that is why second `user.role` prints `sales`. It means all class methods are implemented in the class and also it is store in the class definitions.

Now consider the situation where we want to create method only for a single object of the class not for all objects of the class. We can do it in the ruby using singleton methods for the class object.

## 2. Singleton methods

Singleton methods are the methods which are only available for a single particular object and not for all objects of the class.

Check the following snippet

```ruby
class User
  def role
    puts "Admin"
  end
end

first_user = User.new      
first_user.role              // Admin

// Add singleton method department for `first_user` object.
def first_user.department
  puts 'Admin department'
end
first_user.department        // Admin department

second_user = User.new
second_user.role             // Admin
second_user.department       // NoMethodError (undefined method `department' for #<User:0x000055a8b44b45d0>)
```

We can observe that department method is not available for object `second_user` because the department is singleton method for object `first_user` so it is stored on the metaclass of an object and they are independent of the parent class of the object.

So, Object in ruby only stores the state. Its behavior comes from the class definition. The metaclass is almost similar to a class but it can't be instantiated.
 
