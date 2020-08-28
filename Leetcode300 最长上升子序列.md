### Leetcode300 最长上升子序列

给定一个无序的整数数组，找到其中最长上升子序列的长度。

#### 解题思路

动态规划最重要的一个思想就是状态转移

创建一个数组dp[]，其中dp[i]指的是以数组中序号为i的数作为结尾的上升子序列的大小。

dp[i]指的是以数组中第i个数结尾的最大上升子序列的长度

```java
class Solution {
    public int lengthOfLIS(int[] nums) {
        if (nums.length == 0) {
            return 0;
        }
		int[] dp = new int[nums.length];
        dp[0] = 1;
        int max0 = 1;
        for(int i = 1; i < nums.length; i++){
            int max1 = 0;
            for(int j = 0; j < i; j++){
                if(nums[j] < nums[i]){
                    max1 = Math.max(max1, dp[j]);
                }
            }
            dp[i] = max1 + 1;
            max0 = Math.max(max0, dp[i]);
        }
        return max0;
    }
}
```

