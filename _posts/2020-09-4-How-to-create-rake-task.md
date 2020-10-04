---
layout: post
title: What is Rake task and how to use it?
subtitle: How to create and use Rake task in ruby and use it in the Rails?
tags: [Ruby, Rails]
author: Shekhar Patil
---

# Introduction
Sometimes, We need to have a task that can be executed at regular basic at some time. In ruby, we have a rake task to define and execute this task at any time.  We can use rake tasks in Rails for various purposes.

Rake is inspired by Linux [make utility](https://en.wikipedia.org/wiki/Make_(software)). Its name comes from the `Ruby Make`. Rake is a task management utility that reads and executes the tasks defined in the ruby language in the 'Rakefile`. It was written by the late [Jim Weirich](https://en.wikipedia.org/wiki/Jim_Weirich).

# How to create a Rake task.

Create a file with the name 'Rakefile' and write the following content in it.
` $ touch Rakefile`

```
desc 'print hello world'
task :hello_world do
  puts 'Hello world from Rubyist'
end
```
Here `desc` command defines the description of the task and `task` command defines the actual task that needs to be executed. Here we are defining a simple task which is printing "Hello world from Rubyist.".

If you are in the directory containing the Rakefile then you can execute the following commands:
```
$ rake --task              This command will show all the tasks defined in the Rakefile along with its description.
=> rake hello_world        # Print hello world
```

Now we can execute the task using the following command
```
$ rake hello_world
=> Hello world from Rubyist
```
We can also use namespace while defining the Rake task add the following code to Rakefile:
```
desc 'Display files from the current directory'
namespace :admin do
  task :display_files do
    system('ls')
  end
end
```
Let's see all tasks once again:
```
$ rake --task
=> rake admin:display_files  # Display files from the current directory
   rake hello_world          # print hello world
```
We can execute this task as follows:
```
$ rake admin:hello_world
(It should display files from your current directory)
```
Namespacing to rake task is always good when the number of tasks is more and also it separates the context of the task.


In the Rails project we can see many rake tasks as following:

* rails db:migrate
* rails routes
* rake tmp:clear
* rake tmp:create

We can find out many more tasks by executing `rake --task` command in the Rails application root directory.

## How to define custom rake tasks in Rails?

We can create file with `.rake` extension in `/lib/tasks/` folder.

```
# lib/tasks/clear_logs.rake

namespace :Logs do
  desc 'clear the log files'
  task clear: :environment do
    Dir["log/*.log"].each do |file|
       File.unlink(file)
    end
  end
end
```
Above task is deleting all files from `log directory`.

Now we can simply execute this task as following:
```
$ rake Logs:clear
```

I hope you loved it.
Please feel free to contact me on [twitter](https://twitter.com/Shekharpatil95).
