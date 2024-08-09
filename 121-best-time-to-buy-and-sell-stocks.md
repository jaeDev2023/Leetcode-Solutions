# 121: Best Time to Buy and Sell Stock

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
