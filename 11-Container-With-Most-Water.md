# 11: Container With Most Water

## [Leetcode Link](https://leetcode.com/problems/container-with-most-water/description/)

## Description
You are given an integer array height of length n. There are n vertical lines drawn such that the two endpoints of the ith line are (i, 0) and (i, height[i]).

Find two lines that together with the x-axis form a container, such that the container contains the most water.

Return the maximum amount of water a container can store.

Notice that you may not slant the container.

Input: height = [1,8,6,2,5,4,8,3,7]
Output: 49
Explanation: The above vertical lines are represented by array [1,8,6,2,5,4,8,3,7]. In this case, the max area of water (blue section) the container can contain is 49.

Example 2:

Input: height = [1,1]
Output: 1 

Constraints:

    n == height.length
    2 <= n <= 105
    0 <= height[i] <= 104


## Algorithm
```LANGUAGE(javascript)
/**
 * @param {number[]} height
 * @return {number}
 */
var maxArea = function(height) {
    // Create the constants
    let rollingArea = 0;
    let maxArea = 0;
    let beg = 0;
    let end = height.length - 1;

    // Iterate the endpoints until the meet
    while(beg < end){
        rollingArea = (end - beg) * Math.min(height[beg], height[end]);
        maxArea = Math.max(maxArea, rollingArea);

        // Push the pointer with the smaller point to its neighbor.
        if(height[beg] < height[end]){
            beg++;
        } else {
            end--;
        }
    }

    return maxArea;
};
```
## Algorithm Explanation
We use a two pointer approach. One pointer points to the left (beginning of the array) and the other pointer points
towards the right side of the array.

While the left pointer is less than the right pointer, we will test the current heights at each pointer and find a local rolling area.

rollingArea = length * (height of the smallest of the two heights)
the length is the difference between our two pointers, so
`rollingArea = length * Math.min(height[beg] - height[end]`

Then we update maxArea if the rolling area is larger than the current maxArea.
`maxArea = Math.max(maxArea, rollingArea);`

The key part of the algorithm is how we update the pointers. The trick is to push the smaller of the two heights 
towards the center of the array.

So, if the height on the left side is smaller than the height on the right side, increase the left pointer.
`beg++;`

else, decrease the end pointer to its next value
`end--;`

## Space-Time Complexity
### Time Complexity: O(n)
The algorithm will always run through all elements in the array, so the time complexity is O(n)
### Space Complexity: O(1)
Only a few constants are created, so the time complexity is a constant. We will find the current area.
