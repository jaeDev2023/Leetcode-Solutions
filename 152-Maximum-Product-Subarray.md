# 152: Maximum Product Subarray

## https://leetcode.com/problems/maximum-product-subarray/description/

## Description
Given an integer array nums, find a
subarray
that has the largest product, and return the product.

The test cases are generated so that the answer will fit in a 32-bit integer.

Example 1:

Input: nums = [2,3,-2,4]
Output: 6
Explanation: [2,3] has the largest product 6.

Example 2:

Input: nums = [-2,0,-1]
Output: 0
Explanation: The result cannot be 2, because [-2,-1] is not a subarray.

 

Constraints:

    1 <= nums.length <= 2 * 104
    -10 <= nums[i] <= 10
    The product of any prefix or suffix of nums is guaranteed to fit in a 32-bit integer.


## Algorithm
`````
/**
 * @param {number[]} nums
 * @return {number}
 */
var maxProduct = function(nums) {
    let currentMax = 0;
    let max = -Infinity
    for(let i = 0; i < nums.length; i++) {
        let currentNum = nums[i];
        currentMax = Math.max(currentNum, currentMax *= currentNum);
        max = Math.max(max, currentMax);
    }

     return max;
};
`````
## Algorithm Explanation
Kadane's algorithm is used. currentMax will reset the "sliding window" of values used to a new value 
if the current iteration through the array is larger than extending the new value into the array.

## Space-Time Complexity
### Time Complexity: O(n)
We iterate through the entirety of the array.
### Space Complexity: O(1)
Only some variables are created, so the space complexity is a constant.
