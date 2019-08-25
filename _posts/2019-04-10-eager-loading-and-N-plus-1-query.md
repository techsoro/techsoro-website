---
layout: post
title: Eager loading and N+1 query in rails.
subtitle: Difference between Eager loading and N+1 query in rails.
tags: [Rails, Ruby]
author: Shekhar Patil
comments: true
---


Sometimes, the implementation of an algorithm can make performance worst. Then it does not matter whether it has used the faster programming language like C or slower like Ruby. So we should implement the algorithms properly. Same while dealing with the database we should use proper queries so that the performance should not affect.

### Let's observe an example.

```ruby
class College < ApplicationRecord
  has_many :students
end
```
```ruby
class Student < ApplicationRecord
  belongs_to :college
end
```
Now create some colleges and respective students.

## N+1 query in Rails

If we wanted to list the first ten students and their colleges, We could write the following code.

```sql
students = Student.limit(10)

students.each do |student|
  puts "#{student.college.name} build number #{student.name}"
end
```
The above code works, but it makes far too many independent database queries:

```sql
Student Load (0.3ms) SELECT "students".* FROM "students" LIMIT ? [["LIMIT", 10]]
College Load (0.2ms) SELECT "colleges".* FROM "colleges" WHERE "colleges"."id" = ? LIMIT ? [["id", 1], ["LIMIT", 1]]
College Load (0.2ms) SELECT "colleges".* FROM "colleges" WHERE "colleges"."id" = ? LIMIT ? [["id", 1], ["LIMIT", 1]]
College Load (0.2ms) SELECT "colleges".* FROM "colleges" WHERE "colleges"."id" = ? LIMIT ? [["id", 1], ["LIMIT", 1]]
College Load (0.2ms) SELECT "colleges".* FROM "colleges" WHERE "colleges"."id" = ? LIMIT ? [["id", 1], ["LIMIT", 1]]
College Load (0.2ms) SELECT "colleges".* FROM "colleges" WHERE "colleges"."id" = ? LIMIT ? [["id", 1], ["LIMIT", 1]]
College Load (0.2ms) SELECT "colleges".* FROM "colleges" WHERE "colleges"."id" = ? LIMIT ? [["id", 1], ["LIMIT", 1]]
College Load (0.2ms) SELECT "colleges".* FROM "colleges" WHERE "colleges"."id" = ? LIMIT ? [["id", 2], ["LIMIT", 1]]
College Load (0.1ms) SELECT "colleges".* FROM "colleges" WHERE "colleges"."id" = ? LIMIT ? [["id", 2], ["LIMIT", 1]]
College Load (0.2ms) SELECT "colleges".* FROM "colleges" WHERE "colleges"."id" = ? LIMIT ? [["id", 2], ["LIMIT", 1]]
College Load (0.1ms) SELECT "colleges".* FROM "colleges" WHERE "colleges"."id" = ? LIMIT ? [["id", 2], ["LIMIT", 1]]
```

Currently, There are 11 independent queries to fetch 10 students. One query to fetch students and other N queries to fetch college in each iteration. hence the total number of queries is N+1. Now are fetching just 10 records but in the real-time scenario, the number of required records can be large. Suppose we want to fetch 10000 records then we'll need to connect database 10001 times and it will degrade the performance of the application heavily.

## Eager loading in Rails

To avoid the performance degradation of the previous example we need to reduce the number of independent queries to the database. In rails, this is done by eager loading associated relations. In the eager loading, we collect the required data with only one query.

```sql
students = Student.includes(:college).limit(10)

students.each do |student|
  puts "#{student.college.name} build number #{student.name}"
end
```
This time we'll use one query to fetch the students and another for fetching the associated colleges.
```sql
Student Load (0.4ms) SELECT "students".* FROM "students"
College Load (0.4ms) SELECT "colleges".* FROM "colleges" WHERE "colleges"."id" IN (?, ?, ?, ?) [["id", 1], ["id", 2], ["id", 3], ["id", 4]]
```
Now, we'll required only two queries. Even though we wanted 10000 records only two queries are required to fetch the records from the database and it will improve the performance of our application.

For comparison, the time necessary to load and display 10 builds in my system is 2.1 milliseconds without eager loading and only 0.8 milliseconds with eager loading. This is s huge difference. Currently, In the case of a large number of record fetching, this time difference can be even far more.

I would love to hear some of your tips on dealing with N+1 queries on [twitter](https://twitter.com/Shekharpatil95).

Cheers!
