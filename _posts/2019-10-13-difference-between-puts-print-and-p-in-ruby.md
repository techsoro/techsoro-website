---
layout: post
title: Compare puts, p, print in ruby.
subtitle: Difference between puts, p, and print in ruby.
tags: [Ruby]
author: Shekhar Patil
comments: true
---

Ruby is developer friendly language and it provides many ways to perform same task. For example for printing the output on the console we can use puts, prints and p. But multiple ways to do same task means more confusion for selecting correct way for our use case. In this blog we will discuss about difference between puts, print and p so that we can select correct method as per our use case.

#### Let's start with `hello world` using all of this.

#### 1. Using `puts`.

```ruby
> puts 'hello world'
hello world
 => nil
```
#### 2. Using `p`.

```ruby
> p 'hello world'
"hello world"
 => "hello world"
```
#### 3. Using `print`

```ruby
print 'hello world'
hello world => nil
```

You must have observed there is some difference in every output.

#### Few observations:

1. puts and print has return `nil` while p has return the input we have passed to it.
2. p has shown output in string format.
3. return value of puts and p has printed on next line and for print return value is on same line.

### Let's take one more example for better understanding:

Now we create one file with extension .rb and paste below given code in that file.

1.Example of puts:

```ruby
A = 'I'
B = 'Love'
C = 'Ruby'

puts A
puts B
puts C
```
Now we can run this file using `ruby filename.rb` in the terminal and before running this command confirm that you are in the same directory where you have created ruby file.

output of above code will be as following

Output of puts:

```ruby
I
Love
Ruby
```

Now we will execute same code for print and p.

2.Using print

```ruby
A = 'I'
B = 'Love'
C = 'Ruby'

print A
print B
print C
```
Output of print:
```
ILoveRuby
```

3.Using p.

```ruby
A = 'I'
B = 'Love'
C = 'Ruby'

p A
p B
p C
```
Output of p:
```
"I"
"Love"
"Ruby"
```

Now you must have more clarity about all of this methods.

Let's conclude the blog:

1. puts: puts add newline character at the end of the output. that is why we got return value `nil` on the next line.

2. print: print does not add newline character at the end of output because of that the return value of print that is `nil` is printed on the same line where output is printed.

3. p: p does not change data type of the input provided to it. if we are passing string type of input it also prints the string type of output. Most importantly, unlike to puts and print p does not return nil value. It returns the same value which has passed to it.


Please feel free to contact me on [twitter](https://twitter.com/Shekharpatil95).
