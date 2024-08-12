## Two Sum
https://leetcode.com/problems/two-sum/description/

## Description
Given an array of integers nums and an integer target, return indices of the two numbers such that they add up to target.

You may assume that each input would have exactly one solution, and you may not use the same element twice.

You can return the answer in any order.

## Algorithm
`````
/**
 * @param {number[]} nums
 * @param {number} target
 * @return {number[]}
 */
var twoSum = function(nums, target) {
    let copy = nums;
    copy.sort();
    let beg = 0;
    let end = nums.length - 1;
    while(beg < end) {
        let curSum = copy[beg] + copy[end];
        if(curSum === target) { 
            return [nums.indexOf(copy[beg]), nums.indexOf(copy[end])]
            };
        
        if(curSum > target) {
            end--;
        }
        else {
            beg++;
        }
    }


};
`````
