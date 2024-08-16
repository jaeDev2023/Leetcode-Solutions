# 33. Search in Rotated Sorted Array

## https://leetcode.com/problems/search-in-rotated-sorted-array/description/

## Description
There is an integer array nums sorted in ascending order (with distinct values).

Prior to being passed to your function, nums is possibly rotated at an unknown pivot index k (1 <= k < nums.length) such that the resulting array is [nums[k], nums[k+1], ..., nums[n-1], nums[0], nums[1], ..., nums[k-1]] (0-indexed). For example, [0,1,2,4,5,6,7] might be rotated at pivot index 3 and become [4,5,6,7,0,1,2].

Given the array nums after the possible rotation and an integer target, return the index of target if it is in nums, or -1 if it is not in nums.

You must write an algorithm with O(log n) runtime complexity.


## Algorithm
`````javascript
/**
 * @param {number[]} nums
 * @param {number} target
 * @return {number}
 */
var search = function(nums, target) {
    // set initial values
    let lo = 0;
    let hi = nums.length - 1;
    // Find the lowest number (find the pivot/rotation point)
    while(lo < hi) {
        let mid = Math.floor((lo + hi) / 2);
        if(nums[mid] > nums[hi]) {
            lo = mid + 1;
        } else {
            hi = mid;
        }
    }

    let rot = lo;
    lo = 0;
    hi = nums.length - 1;

    // Now we binary search for the target, but use modulus to map mid
    while(lo <= hi) {
        let mid = Math.floor((lo + hi) / 2);
        let rotatedMid = (mid + rot) % nums.length;
        if(nums[rotatedMid] === target) {
            return rotatedMid;
        }
        if(nums[rotatedMid] < target) {
            lo = mid + 1;
        } else {
            hi = mid - 1;
        }
    }

    return -1;
};
`````
## Algorithm Explanation
The first block of this code uses binary search to find the lowest number in the array. This effectively
also finds the pivot (rotation) index. With the pivot index, we can use a binary sort in the second chunk of 
the code to find the index of our target value.

The second block is a binary sort, but we use the modulus operator to map the middle index in the 
rotated array to what the mid point of the array would be if nums were sorted. An example of the logic is below:

nums = [4, 5, 6, 7, 0, 1, 2, 3];

The pivot point, at index = 4 is where the lowest point in the array is. If the array where sorted it would look like:
sortedN = [0, 1, 2, 3, 4, 5, 6, 7]

To use binary search, the array needs to be sorted, but we can get arround that using the modulus operator.

Let's say you want to find the position of where 4 is the rotated array and see where it is in the sorted array.
4 is at index = 0 for the rotated array (called nums above). The pivot value is 4. Then the location of 4 in the sorted array given 
its location in the rotated array would be (rotation index + pivot value) = (0 + 4).
sortedN[4] === 4, so we know this logic works initially.

But this process will lead to key error near the end of the nums array.

if we wanted to find the index of 0 in the sorted nums array, then: (0 rotation index + pivot value) = (4 + 4) = 8;
This is too big. We need to circle back around to the beginning, so we can do that with the modulus operator:

(0 rotation index + pivot value) % nums.length =
(4 + 4) % 8 = 0.
sortedN[0] = 0. We Win.




## Space-Time Complexity
### Time Complexity: O(log[n])
### Space Complexity: O(1).
