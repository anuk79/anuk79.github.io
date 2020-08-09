---
title:  "Proper naming convention pays off in long run"
categories: Programming
tags: ['Code', 'Naming', 'Programming']
is_post: "True"
is_home_btn_reqd: "True"
subTitle: "In the coding universe, names matter a lot."
layout: default
permalink: /programming/2019/08/14/proper-namin-convention-pays-off-in-long-run/
is_project_btn_reqd: "False"
---


Hi everyone, today we will explore how we can use grammar to properly name our variables and functions. I have been using these ever since college and have found it to be extremely helpful for writing readable and clean code.

## Why proper naming convention matters
*In the coding universe, names matter a lot.*

The thumb rule of naming any variable, method, class, etc should be that the name alone should be able to describe:
- **why it exists**
- **what it does**

Let say, we have a code where `var abc = 12;` , what do we infer from this? 
We cannot understand what value does this refer to, what 12 here stands for.

But, instead, if we had `var numberOfMonths = 12;` it is quite clear that 12 stands for the number of months in a year. 
So, the code becomes more readable, and hence, more maintainable, by following good naming conventions.

## Let’s follow some grammar rules
The verbs and nouns play a great role while assigning names in code. I follow the following two rules, and my life has been so much easy. The rules are very simple, and cover almost all scenarios:

**If we are naming a variable, the name should be a NOUN, and if we are naming a function, it should be a VERB.**

Let’s understand through some examples:

1. While creating a variable used to store a value, we can use **nouns**, like:
  ```
    var personName = 'some name';
    var personAge = 25;

    // using plural names for arrays, etc.
    var candidates = [];
  ```

  For variables which store **boolean** values, often **is/has/did/should**, etc are pre-pended. So when we read that name,   it is quite clear that the value will be either true or false, like:
  ```
    // boolean values
    var hasError = false;
    var isSelected = true;
    var didValueChange = true;
    var shouldHide = false;
  ```
  
2. While creating any function, we can use **verbs** (so that they denote some kind of action), like:
  
  ```
    // getters
    function getName () { /** code goes here */ }
    
    // setter
    function setName () { /** code goes here */ }
    
    // performing some action
    function displayAvailableOptions { /** code goes here */ }
    
    function validateNumber()  { /** code goes here */ }
    
    function updateCandidateInformation()  { /** code goes here */ }
    
    function handleValueChange() { /** code goes here */ }
    
    function onButtonClick()  { /** code goes here */ }
  ```
  
  For functions which will return a **boolean** value, we can pre-pend **is/has/did/should**, etc to the name, similar to naming variables holding boolean values, like:
  ```
    function isDataLoaded() { /** code goes here */ }
    function hasValueChanged() { /** code goes here */ }
    function didStudentPass() { /** code goes here */ }
    function shouldUpgrade()  { /** code goes here */ }
  ```
  
### That’s all.

These are the TWO simple rules which cover almost all kinds of scenarios which we can stumble upon while coding.

They have proven to be very useful to me, and I hope you also find it useful and helpful for creating a cleaner and more readable codebase.

Do let me know, what do you follow while naming your variables, functions, etc.
Happy learning, have a great day… 😊



**NOTE:** This article was originally posted on [Medium](https://medium.com/@anuradha15/proper-naming-convention-pays-off-in-long-run-962798527848)
