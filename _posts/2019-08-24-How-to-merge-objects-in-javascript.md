---
layout: post
title: How to merge objects in Javascript.
subtitle: Extend, Merge methods in the Javascript.
tags: [Javascript]
author: Shekhar Patil
comments: true
---

Yesterday, I was working on an issue in which database value for particular object attribute was correct but on UI it was showing the wrong value. I dig into the front-end Javascript code and I found that bug occurred while merging the two objects in Javascript. first, we will discuss how to merge two objects then I will explain what we should care about while merging two objects.

## How to merge objects?

### 1. Merge two objects having distinct attributes names.

declare two objects as the following:
```javascript
var student = { 
  student_name: "Rahul", 
  age: 22, 
  standard: "6th" 
};

var school = { 
  school_name: "SBK high school", 
  location: "Pune" 
};


```

Now, we will use `extend` method to merge these two objects.

```javascript
$.extend(student, school);

> {student_name: "Rahul", age: 22, standard: "6th", school_name: "SBK high school", location: "Pune"}
```

We can also use the `merge` method to merge these objects

```javascript
$.merge(student, school);

> { student_name: "Rahul", age: 22, standard: "6th", length: undefined}
```

### 2. Merge two objects having some common attributes names.

We don't have to care where there are distinct attributes in the objects. But when there are some common attribute names then those attributes value gets an override.


declare two objects having the same attribute names like the following:
```javascript
var student = { 
  name: "Rahul", 
  age: 22, 
  standard: "6th" 
};

var school = { 
  name: "SBK high school", 
  location: "Pune" 
};


```

Now, we will use `extend` method to merge these two objects.

```javascript
$.extend(student, school);

> {name: "SBK high school", age: 22, standard: "6th", location: "Pune"}
```

We can also use the `merge` method to merge these objects

```javascript
$.merge(student, school);

> {name: "Rahul", age: 22, standard: "6th", length: undefined}
```

Now we have understood how to merge two objects in Javascript and the difference between merge and extend method in Javascript. We should be careful while merging two objects having a common attribute name. Common attribute names can cause unexpected result in the output.

Please feel free to contact me on [twitter](https://twitter.com/Shekharpatil95).  
