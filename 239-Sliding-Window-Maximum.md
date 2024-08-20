# 239: Sliding Window Maximum

## [Link to the leetcode question](https://leetcode.com/problems/sliding-window-maximum/)

## Description
You are given an array of integers nums, there is a sliding window of size k which is moving from the very left of the array to the very right. You can only see the k numbers in the window. Each time the sliding window moves right by one position.

Return the max sliding window. 

Example 1:

Input: nums = [1,3,-1,-3,5,3,6,7], k = 3
Output: [3,3,5,5,6,7]
Explanation: 
Window position                Max
---------------               -----
[1  3  -1] -3  5  3  6  7       3
 1 [3  -1  -3] 5  3  6  7       3
 1  3 [-1  -3  5] 3  6  7       5
 1  3  -1 [-3  5  3] 6  7       5
 1  3  -1  -3 [5  3  6] 7       6
 1  3  -1  -3  5 [3  6  7]      7

Example 2:

Input: nums = [1], k = 1
Output: [1]

Constraints:

    1 <= nums.length <= 105
    -104 <= nums[i] <= 104
    1 <= k <= nums.length

## Algorithm
```LANGUAGEjavascript 
/**
 * @param {number[]} nums
 * @param {number} k
 * @return {number[]}
 */
var maxSlidingWindow = function(nums, k) {
    const q = [];
    const sol = [];

    for(let i = 0; i < nums.length; i++){
        // Pop of indices in q if the value at the end of q is smaller than the current value in the nums array: num[i]
        while(q && nums[q[q.length - 1]] < nums[i]){
            q.pop();
        }
        // Add current index
        q.push(i);
        // Remove the oldest index in the q array if it outside of the sliding window
        if(q[0] === i - k){
            q.shift();
        }
        // Add the largest value in the sliding window if the sliding window has reach the given size, k.
        if(i >= k - 1){
            sol.push(nums[q[0]]);
        }
    }
    return sol;
};
```
## Algorithm Explanation
The process of the algorithm uses a deque to keep track of the local large values.

q is an array that holds onto the indices of the elements in nums.

While iterating through all of the values in the array, will add values to our q, but also pop off values in the q that are smaller than the current iteration at nums[i]

`while(q && nums[q[q.length - 1]] < nums[i])` is explained below
`q.length - 1` is the index of the final value in the q array.
`q[q.length - 1]` is the value at the end of our q array. This final value in the q array points to a value in the nums array. So, this line gets us the value of the last item in our q.

Thus, `while(q && nums[q[q.length - 1]] < nums[i])` removes the values in q if `nums[i]` is larger than the last element associated with q. This ensures that the values in q are linked to the nums values in descending order, so we are constantly removing any numbers smaller than nums[i].

`q.push(i)` Just adds the current index for the nums iteration.

`q[0] === i - k` tests the first value in our index array. This will test to see if it lies outside of the range of our sliding window. If it is outside of the range, then remove it with `q.shift();`

`if(i >= k - 1)`: If our sliding window has reached the given size of `k`, then we can push `q[0]`, which is the highest value in our sliding window.


## Space-Time Complexity
### Time Complexity: O(n)
### Space Complexity: O(n) per the result array, which only happens if the sliding window size is equal to 1.
