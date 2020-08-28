### Leetcode 714 买卖股票的最佳时机

给定一个整数数组 prices，其中第 i 个元素代表了第 i 天的股票价格 ；非负整数 fee 代表了交易股票的手续费用。

你可以无限次地完成交易，但是你每笔交易都需要付手续费。如果你已经购买了一个股票，在卖出它之前你就不能再继续购买股票了。

返回获得利润的最大值。

注意：这里的一笔交易指买入持有并卖出股票的整个过程，每笔交易你只需要为支付一次手续费。

#### 解题思路

对于每天的初始状态有两种

1.有股票

2.没股票

每天的末尾状态有两种

1.有股票

2.没股票

![image-20200827203731342](C:\Users\Kyle-Sung-Gu\AppData\Roaming\Typora\typora-user-images\image-20200827203731342.png)

```java
class Solution {
    public int maxProfit(int[] prices, int fee) {
        int cash = 0;
        int hold = -prices[0];
        for(int i = 1; i < prices.length; i++){
            cash = Math.max(cash, hold + prices[i] - fee);
            hold = Math.max(hold, cash - prices[i]);
        }
        return cash;
    }
}
```

