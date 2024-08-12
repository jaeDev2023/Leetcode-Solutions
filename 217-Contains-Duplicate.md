# 217: Contains Duplicate

## https://leetcode.com/problems/contains-duplicate/description/

## Description
Given an integer array nums, return true if any value appears at least twice in the array, and return false if every element is distinct.


## Algorithm
`````
/**
 * @param {number[]} nums
 * @return {boolean}
 */
var containsDuplicate = function(nums) {
    const countMap = new Map();

    for(let i = 0; i < nums.length; i++)
    {
        num = nums[i];
        // If countMap already has the element in the hashmap, return true.
        if(countMap.has(num)) {
            return true;
        } else {
            countMap.set(num, 1);
        }
    }
    return false;
};
`````
## Algorithm Explanation
The algorithm uses a hashmap to see if the value of the array is in the hashmap. If it is in the hashmap already, then
we have a duplicate and the algorithm can return true. Otherwise, add the element to the hashmap.

If we iterate through all values and didn't find a duplicate, then we can return false.

Note: I initially tried to iterate through the numbers in nums using nums.forEach(function(element)) and then returned true if countMap.has(Num) was true. However, forEach won't break out of the iteration when true is
returned, so the function would always sort through the entirety of the array and then always return false.

So, I just iterated using a for-loop.

## Space-Time Complexity
### Time Complexity: O(n)
### Space Complexity: O(n)
