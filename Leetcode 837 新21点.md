### Leetcode 837 新21点

爱丽丝参与一个大致基于纸牌游戏 “21点” 规则的游戏，描述如下：

爱丽丝以 0 分开始，并在她的得分少于 K 分时抽取数字。 抽取时，她从 [1, W] 的范围中随机获得一个整数作为分数进行累计，其中 W 是整数。 每次抽取都是独立的，其结果具有相同的概率。

当爱丽丝获得不少于 K 分时，她就停止抽取数字。 爱丽丝的分数不超过 N 的概率是多少？



#### 解题思路

对于$0 \le x<k$，dp[x]的值只与d[x+1]，dp[x+2]，dp[x+3]，.....，dp[x+w]的值有关，考虑到从1到w每个值的选取都是随机的所以

$dp[x] = \frac{dp[x+1]+dp[x+2]+dp[x+3]+.....+dp[x+w]}{w}$

```java
class Solution {
    public double new21Game(int N, int K, int W) {
        if (K == 0) {
            return 1.0;
        }
        int min = Math.min(N, K-1+W);
        double[] dp = new double[K+W];
        
        for(int i = K; i <= min; i++){
                dp[i] = 1.0;
        }
        dp[K - 1] = 1.0 * Math.min(N - K + 1, W) / W;
        for(int i = K-2; i >= 0; i--){
            dp[i] = (dp[i+1] * (W+1) - dp[i+W+1]) / W;
        }
        
        return dp[0];
    }
}
```

