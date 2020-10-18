---
layout: post
title: The const_get method in the ruby.
subtitle: Do you know how helpful the const_get method is?
tags: [Ruby]
author: Shekhar Patil
comments: true
---

First, we will understand how the const_get method works then I will explain how we can use it in different ways and what are the use cases.

```ruby
module Vehicle
  class Car
    WHEELS = 4
  end
end

puts Object.const_get 'Vehicle::Car::WHEELS'   # => 4
```

Here, we can see that we have passed the string 'Vehicle::Car::WHEELS' parameter to method const_get and it has given the outcome '4' which is the actual value of constant wheels.

We can also use some variable to store this string and get the constant's value bypassing this variable as a parameter to the const_get method.

We can also lookup the ancestor's constant using const_get method if the inherit flag is set as true.

``Note:`` ancestors of some module means a list of modules included or prepend in that module.

```ruby
module Vehicle
  class Car
    WHEELS = 4
  end

  class TeslaS < Car
  end
end

wheel_const = 'Vehicle::TeslaS::WHEELS'

# Here true is inherit flag which can be true or false
puts Object.const_get(wheel_const, true)  # => 4
```


Here we have given the inherit flag as true it means lookup the base class and the module Vehicle's ancestors as well. If we would have included/prepend some modules in our Vehicle module then the const_get method also would have lookup into those modules. 

Now, let's try to change that flag into false.

```ruby

module Vehicle
  class Car
    WHEELS = 4
  end

  class TeslaS < Car
  end
end

wheel_const = 'Vehicle::TeslaS::WHEELS'
puts Object.const_get(wheel_const, false)

#  Output:
#  Traceback (most recent call last):
#	  1: from random.rb:11:in `<main>'
#  random.rb:11:in `const_get': uninitialized constant Vehicle::TeslaS::WHEELS (NameError)
```

Now, we are getting an error uninitialized constant `Vehicle::TeslaS::WHEELS` because now we have set inherit flag as a false so const_get method will not lookup base class or modules ancestors for `WHEEL` constant. It will throw an error because the `WHEEL` constant is not defined in the TeslaS class.

``Note:`` If we do not mention the inherit flag then it is by default true.

I hope you loved it.
Please feel free to contact me on [twitter](https://twitter.com/Shekharpatil95).
