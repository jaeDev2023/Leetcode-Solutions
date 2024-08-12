# 121: Best Time to Buy and Sell Stock
https://leetcode.com/problems/best-time-to-buy-and-sell-stock/description/

## Description
You are given an array prices where prices[i] is the price of a given stock on the ith day.

You want to maximize your profit by choosing a single day to buy one stock and choosing a different day in the future to sell that stock.

Return the maximum profit you can achieve from this transaction. If you cannot achieve any profit, return 0.

## Algorithm
`````
/**
 * @param {number[]} prices
 * @return {number}
 */
var maxProfit = function(prices) {
    let buyTime = 0;
    let profit = 0;
    for(let sellTime = 1; sellTime < prices.length; sellTime++) {
        localProfit = prices[sellTime] - prices[buyTime];
        profit = Math.max(localProfit, profit);
        if(prices[sellTime] < prices[buyTime]) {
            buyTime = sellTime;
        }
    }

    return profit;
};

`````
## Space-Time Complexity
### Time complexity: O(n)
### Space Complexity: O(1)
