# 238. Product of Array Except Self
https://leetcode.com/problems/product-of-array-except-self/description/

## Description
Given an integer array nums, return an array answer such that answer[i] is equal to the product of all the elements of nums except nums[i].

The product of any prefix or suffix of nums is guaranteed to fit in a 32-bit integer.

You must write an algorithm that runs in O(n) time and without using the division operation.

## Algorithm
`````javascript
/**
 * @param {number[]} nums
 * @return {number[]}
 */
var productExceptSelf = function(nums) {
    // build prefix
    let leftProduct = 1;
    const prefix = [];
    prefix.push(leftProduct);
    for(let i = 1; i < nums.length; i ++)
    {
        leftProduct *= nums[i - 1];
        prefix.push(leftProduct);
    }

    let revProduct = 1;
    const suffix  = [];
    suffix.push(revProduct);

    for(let i = nums.length - 2; i >= 0; i--) {
        revProduct *= nums[i + 1];
        suffix.unshift(revProduct)
    }

    const solution = [];
    for(let i = 0; i < nums.length; i++) {
        solution[i] = prefix[i] * suffix[i];
    }

    return solution
    
};
`````
