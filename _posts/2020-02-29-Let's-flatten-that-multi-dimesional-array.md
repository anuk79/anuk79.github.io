---
title:  "Let’s flatten that multi-dimensional array"
categories: Unit_Tests
tags: ['Javascript', 'Arrays', 'Problem-Solving', 'Interview Questions']
is_post: "True"
is_home_btn_reqd: "True"
subTitle: "Write a function to flatten a multi-dimensional array (depth can go till n-levels) and the result should not contain any null/undefined values."
---

# Let’s flatten that multi-dimensional array

Hi everyone, how are you doing? This is my first article for the year 2020 and let’s get into some problem-solving exercise today.

This is one of the recurring interview questions for JavaScript developers. We will go through both the problem and the solution in this post.

## Problem statement:
Write a function to flatten a multi-dimensional array (depth can go till n-levels) and the result should not contain any null/undefined values.

## Sample input:
var testArray = [1, 2, null, [4, undefined, [11, 10]], 6, [7, null, 0], null, 9];


## Expected output:
`[1, 2, 4, 11, 10, 6, 7, 0, 9]`

## Solution 1: using ‘for’ loop and ‘recursion’

```
// the utility function to flatten input array
function flattenArray(arr) {  
  let result = [];    
  for(let index = 0; index < arr.length; index++) {    
     const currentValue = arr[index]; 
     if(Array.isArray(currentValue)) {
       result = [...result, ...(flattenArray(currentValue))];
       // we can also use concat method to achieve the same result
       // result = result.concat(flattenArray(currentValue));
     } else {      
       if(currentValue != null) {        
          result.push(currentValue);      
       }
    }
  }
  return result;  
} 

// use the code below to execute and test the functionality
const testArray = [1, 2, null, [4, undefined, [11, 10]], 6, [7, null, 0], null, 9]; 
const result = flattenArray(testArray); 
console.log(result);  // [1, 2, 4, 11, 10, 6, 7, 0, 9]
```


**NOTE:** This article was originally posted on [Medium](https://medium.com/@anuradha15/lets-flatten-that-multi-dimensional-array-79787a9b6d13)
