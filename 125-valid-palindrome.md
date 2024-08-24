# 125. Valid Palindrome

## [Link to the leetcode question](https://leetcode.com/problems/valid-palindrome/description/)

## Description
A phrase is a palindrome if, after converting all uppercase letters into lowercase letters and removing all non-alphanumeric characters, it reads the same forward and backward. Alphanumeric characters include letters and numbers.

Given a string s, return true if it is a palindrome, or false otherwise.

Example 1:

Input: s = "A man, a plan, a canal: Panama"
Output: true
Explanation: "amanaplanacanalpanama" is a palindrome.

Example 2:

Input: s = "race a car"
Output: false
Explanation: "raceacar" is not a palindrome.

Example 3:

Input: s = " "
Output: true
Explanation: s is an empty string "" after removing non-alphanumeric characters.
Since an empty string reads the same forward and backward, it is a palindrome.

Constraints:

    1 <= s.length <= 2 * 105
    s consists only of printable ASCII characters.


## Algorithm
```javascript
/**
 * @param {string} s
 * @return {boolean}
 */
var isPalindrome = function(s) {
  // Strip away non-alphanumeric values and convert all letters to lowercase
  s = s.toLowerCase().replace(/[^a-z0-9]/gi,'');
  let beg = 0;
  let end = s.length -1;
  while(beg < end){
      // return false if the values don't match
      if(s[beg] !== s[end]){
          return false;
      }
      beg++;
      end--;
  }
  // Return true if all values, front and back, match.
  return true;
};
```
## Algorithm Explanation
This is a simple two-pointer solution. Our pointers will start at the beginning of the string and the end.

However, we don't want to worry about characters like ",", "^", etc, so we use the regular expression in `s = s.toLowerCase().replace(/[^a-z0-9]/gi,'');` to remove those special characters.

Then its as simple as testing each pointer value in the string and seeing if they match. If they don't match, return false. If we loop all the way through without return false, then we know that
we found a palindrome.

## Space-Time Complexity
### Time Complexity: O(n^100)
### Space Complexity: O(n^100)
