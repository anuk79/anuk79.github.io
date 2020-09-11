---
title:  "Why should I unit test my code?"
categories: Unit_Tests
tags: ['Unit Testing', 'TDD', 'Javascript']
is_post: "True"
is_home_btn_reqd: "True"
subTitle: "A very popular debate in dev community"
layout: default
permalink: /unit_tests/2019/05/05/why-should-i-unit-test-my-code
nextBlogLink: /unit_tests/2019/05/18/how-should-i-unit-test-my-code-part-1/
is_project_btn_reqd: "False"
---




Hi everyone, today we are going to explore the **WHY question** on unit testing the code.

A very popular debate which I have observed in the developers’ world is *whether or not to write unit test cases for code and how writing those test cases could(no, it shouldn’t) be an overhead for the developers.*

In my experience of more than 5 years of coding(mostly web development), I have met very few people who willingly unit test almost everything they code. So I feel that it’s the need of the hour to talk more about it and focus more on [TDD](https://en.wikipedia.org/wiki/Test-driven_development) (Test Driven Development).

**As quoted by one of the articles [here](https://smartbear.com/blog/test-and-monitor/a-short-lecture-on-the-value-and-practice-of-unit/), unit tests are so important that they should be a first class language construct.**

**Me: Yes please.. it’s about time now!!**

## What is unit testing?

So, before you shall ask me, why should I unit test my code, 🤔, let’s start by understanding what exactly is unit testing…

There are many good explanations and introductory articles present on web which cover this topic. As [wikipedia](https://en.wikipedia.org/wiki/Unit_testing) says:

**Unit testing** is a [software testing](https://en.wikipedia.org/wiki/Software_testing) method by which individual units of [source code](https://en.wikipedia.org/wiki/Source_code), sets of one or more computer program modules together with associated control data, usage procedures, and operating procedures, are tested to determine whether they are fit for use.

Here, **unit** can be the smallest part of the application/module that can be tested in isolation. It can be a class in object oriented programming, a function in procedural programming, a component in React, Angular, Vue, and so on.
The main purpose is to verify if that unit of code is working fine for all the scenarios which might occur. If yes, then whichever module consumes it, we are sure that this code will not break.

The main purpose is to verify if that unit of code is working fine for all the scenarios which might occur. If yes, then whichever module consumes it, we are sure that this code will not break.

Unit testing makes the process more [agile](https://en.wikipedia.org/wiki/Agile_software_development). Ask me how?

This is because as the application evolves we need to add more and more features, and some times it involves revisiting earlier designs and code. Unit tests can detect breaking changes in design contracts, and issues can be found very early and resolved.

They also help in safe refactoring of the code. If we are refactoring a code, the end purpose of that code should remain same, and if we have proper unit tests in place, any defect in refactored code can be easily detected by the test cases. So we know where to debug if any of test cases fail. This also makes the [debugging](https://en.wikipedia.org/wiki/Debugging) process easier.

We have plenty of reasons to unit test the code, but now enough of talks, let’s try to explore the importance by coding it out.

**Point to Note:** All my examples below are written in [JavaScript](https://developer.mozilla.org/en-US/docs/Web/JavaScript) and unit test framework used is [Jest](https://jestjs.io/).

## Example 1:
We want to write a method which adds two numbers as below:
```
function addNumbers(num1, num2) {
   return num1 + num2;
}
```
PFB test case for above addNumbers method:
```
expect(addNumbers(5, 6)).toBe(11);
expect(addNumbers(-1, 9)).toBe(8);
```

Now, imagine a situation where the consuming module forgot to pass parameters to **addNumbers**. What should happen then? Let’s say I want it to return 0 when any unexpected(undefined, null, string, etc.) value comes in. So, I go ahead and add corner case tests to handle this scenario.

```
// fails as with current implementation, result will be NaN
expect(addNumbers()).toBe(0);
// fails as with current implementation, result will be 'abcxyz' expect(addNumbers('abc', 'xyz')).toBe(0);
```

Now these two test cases will break, because the actual result is different than what I had expected from this method. So, I go ahead and update the implementation, as below:

```
function addNumbers(num1, num2) {
   return parseFloat(num1 + num2) || 0;
}
```

Now, all our test cases should pass, and if I had delivered this code today to production, I can sleep peacefully because I know that this method will not break any module from which it is getting consumed. What a relief, isn’t it 😎

## Example 2:
Let’s consider we had a method which takes in userDetails as its argument and returns a new object, as below:

```
function getUserDetailsToDisplay(userDetails) {
   return {
     name: getFullName(userDetails.firstName, userDetails.lastName),
     dateOfBirth: userDetails.dob || '-'
   };
}
function getFullName(firstName = '', lastName = '') {
   return (firstName + ' ' + lastName).trim() || '-'; 
}
```

And the UT goes as below:

```
const resultWithValidDetails = getUserDetailsToDisplay({
   firstName: 'testFirstName',
   lastName: 'testLastName', 
   dob: 'test date'
});
expect(resultWithValidDetails.name).toBe('testFirstName testLastName');
expect(resultWithValidDetails.dateOfBirth).toBe('test date');
const resultWithNoDetails = getUserDetailsToDisplay({});
expect(resultWithNoDetails.name).toBe('-');
expect(resultWithNoDetails.dateOfBirth).toBe('-');
```

Now, the new requirement comes in, wherein, we need to show the ‘middleName’ of the user as well. So we go and change the functionality of **getUserDetailsToDisplay** as below:

```
function getUserDetailsToDisplay(userDetails) {
   return {
     name: getFullName(userDetails.firstName,     
           userDetails.middleName, userDetails.lastName),
     dateOfBirth: userDetails.dob || '-'
   };
}
```

At this point, let say that we forgot to update the getFullName method, and we also ignored any warning that we got. So If we had the test cases in place, they would start breaking, and this will alert us to examine the code in **getFullName**.

PFB the exact error we will get while running the tests:

So we know there is some issue with our code, and we know exactly what is breaking. So, we should now go and see the logic of computing name, and fix it.

There can be a second scenario, where, if we are following TDD, we would have already updated the test cases to test the new changes as below:

```
const resultWithValidDetails = getUserDetailsToDisplay({
   firstName: 'testFirstName',
   middleName: 'testMiddleName'
   lastName: 'testLastName', 
   dob: 'test date'
});
expect(resultWithValidDetails.name).toBe('testFirstName testMiddleName testLastName');
expect(resultWithValidDetails.dateOfBirth).toBe('test date');
```

But, the test cases would still fail, because the getFullName expects three parameters now, but we are only passing 2 of them in actual code. This is an example of easier debugging, we know where and what code block to debug based on the unit test case failed. PFB error in this case:

<img>

So, here, we found our mistake and could easily fix the code as below:

```
function getFullName(firstName = '', middleName = '', lastName = '') {
   return (firstName + ' ' + middleName + ' ' + lastName).trim() || 
          '-';
}
```

Now, all test cases should pass, and we should be good to go. So far, by writing unit tests, we have prevented two bugs in production, thereby reducing the cost of delivery (by avoiding the extra iteration of finding bug, fixing it, verifying it and delivering it again to production). The quality of the code gets better when it is tested properly, and hence quite less prone to breaking our application/product.

By now, at least you have some idea about how unit testing might help. Now, I know these were not one of the greatest examples out there, but I purposefully kept it so simple, so that we are comfortable with the very idea of **unit testing.**

## Conclusion

If you ask of my take on it, unit tests should not be seen as an overhead or burden, instead *we should embrace them as a daily practice and a healthy coding habit.*

There have been many times where I have thanked my past self for writing that piece of test case which saved me from making a huge mistake and preventing an otherwise almost certain production bug.

Unit tests help us write a better code and handle the multiple real-time scenarios quite well.

I always stress on the point to *write logical test cases, and not to write it just for the sake of achieving that coverage goal*, so that if anyone makes any design change in the component/function, the unit test should fail and that’s how any developer, new to that codebase, can understand what was the original purpose of that code.

This covers one more purpose of unit test, which is documentation of the code. *Good unit test cases serve as a documentation for future* and it’s easy to maintain a code base that is well documented and properly unit tested.
PFB one quote i once read on web (I do not remember the author name, but he/she must be a legend)

**Any code that is not unit tested is legacy code.**

So, if you want to ask me when should be right time to start unit testing my code, the answer would be *NOW!*

Stay tuned and catch you in the next article !! Any feedback is highly appreciable.

As I would be covering the **How?** part in my next article, do let me know if you would like me to talk about how to test any specific scenario/code (I would be covering examples for unit testing React with Jest and Enzyme).

Thanks for reading, have a great day!!




**NOTE:** This article was originally posted on [Medium](https://medium.com/@anuradha15/why-should-i-unit-test-my-code-989c378e8ebc)

<blockquote class="embedly-card"><h4><a href="https://medium.com/@anuradha15/why-should-i-unit-test-my-code-989c378e8ebc">Why should I unit test my code?</a></h4><p>So, before you shall ask me, why should I unit test my code, 🤔 let's start by understanding what exactly is unit testing... There are many good explanations and introductory articles present on web which cover this topic.</p></blockquote>
<script async src="//cdn.embedly.com/widgets/platform.js" charset="UTF-8"></script>
