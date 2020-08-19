---
title:  "Let’s flatten that multi-dimensional array"
categories: Programming
tags: ['Javascript', 'Arrays', 'Problem-Solving', 'Interview Questions']
is_post: "True"
is_home_btn_reqd: "True"
subTitle: "Write a function to flatten a multi-dimensional array (depth can go till n-levels) and the result should not contain any null/undefined values."
layout: default
permalink: /programming/2020/02/29/let's-flatten-that-multi-dimesional-array/
prevBlogLink: /accessibility/2019/11/25/awareness-for-accessibility/
nextBlogLink: /unit_tests/2020/04/04/test-styled-components-in-react-effeciently-using-display-names/
is_project_btn_reqd: "False"
---


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

Let’s breakdown the implementation to understand the approach:

1. We create the utility function **flattenArray** which will take the multidimensional array as input, and return the flattened array with no null/undefined items as output.

2. Create an array called **result** to which will contain the final array to be returned.

3. Loop over the input array to iterate over each item. I have used **for** loop here for simplicity. We can also use **forEach** loop or [reduce](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/reduce) ( a higher-order function present on Array prototype) to achieve the same result.

4. For each item of the current array, we need to check first if that element is an Array? In the above example, [Array.isArray](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/isArray) function is used to check the same.

5. If the current element is not an Array, we can go ahead and push that element onto the **result** array after **null** check. Remember, we need to eliminate any null/undefined values from the Array. If you notice, in the code, I have used loose equality check for null values (currentValue != null). This was done intentionally so that both null and undefined values get eliminated from the result.

6. But what if the current element is an array? We will have to perform step 3 till 5 again to push the individual items of this new array to existing results array. This can be achieved by using a concept called [recursion](https://javascript.info/recursion) (where a function calls itself until a condition is met).

7. As the recursive function will also return an array of items, we will now [concat](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/concat) the result of recursive function with the already existing results array. This will ensure that the two different arrays get merged. This logic will continue till *n-level* (here, n is the depth of the input array). I have used the [ES6 spread operator](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax) to achieve the same result.

8. Finally, when items at all levels of the input array are concatenated into a single-dimensional array, that result is returned from the function. This will be our most-awaited, most precious result that we were coding for.
:dancer:	:dancer:	:dancer:	

Now, if you felt that the code is too much, well JavaScript has a simpler solution for you. Presenting a second solution below.

## Solution 2: using [Array.prototype.flat()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/flat)

We have a **flat** method on the Array prototype which flattens the Array, and we can provide an optional parameter to decide the depth of array till which it should be flattened.

Although we will still need to write the logic to remove null/undefined items from the result, it does take away all the loop and recursion code just to flatten the Array.

By default, it flattens the Array for first level depth. Please find below an example.

```
const testArray = [1, 2, null, [4, undefined, [11, 10]], 6, [7, null, 0], null, 9];
console.log(testArray.flat()) 
// results as below
// [1, 2, null, 4, undefined, [11, 10], 6, 7, null, 0, null, 9]
```

If we do not know the depth of Array and want it flattened till the n-th level, then we can pass **Infinity** as the depth parameter. See example below:

```
const testArray = [1, 2, null, [4, undefined, [11, 10]], 6, [7, null, 0], null, 9];
console.log(testArray.flat(Infinity))
// results as below
// [1, 2, null, 4, undefined, 11, 10, 6, 7, null, 0, null, 9]
```

We can then use [filter](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/filter) to eliminate all null/undefined items from the result. PFB final code:

```
const testArray = [1, 2, null, [4, undefined, [11, 10]], 6, [7, null, 0], null, 9];
const result = testArray.flat(Infinity).filter(val => val != null);
console.log(result);
// [1, 2, 4, 11, 10, 6, 7, 0, 9]
```

**Note:** You might want to check the browser support for this before starting to use it in production code. Check the below link for more details — [https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/flat](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/flat)




## Github link

FWIW, I have also added the above code examples at [github gist](https://gist.github.com/anuk79/58da1549aa0827ea6a74cd78c10868cd)

----------------------------

## Conclusion

There can be multiple solutions to this problem statement. While I have explained two of them, I would like to know about what approach will you follow to solve the same. Do let me know your solutions/thoughts in the comments.

Till then, happy learning and have a wonderful leap year.

________________________________



**NOTE:** This article was originally posted on [Medium](https://medium.com/@anuradha15/lets-flatten-that-multi-dimensional-array-79787a9b6d13)
