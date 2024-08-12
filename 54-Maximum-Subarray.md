# 53: Maximum Subarray

## https://leetcode.com/problems/maximum-subarray/description/

## Description
Given an integer array nums, find the
subarray
with the largest sum, and return its sum.


## Algorithm
`````
/**
 * @param {number[]} nums
 * @return {number}
 */
var maxSubArray = function(nums) {
    let curMax = 0;
    let max = -Infinity;

    nums.forEach(function(currentNumber) {
        curMax = Math.max(currentNumber, curMax + currentNumber);
        max = Math.max(max, curMax);
    });

    return max;

    // Time complexity: O(n)
    // Space Complexity: O(1);

};
`````

## Space-Time Complexity
### Time Complexity: O(n)
### Space Complexity: O(1)
