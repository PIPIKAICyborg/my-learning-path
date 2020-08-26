### Leetcode 474 一和零

在计算机界中，我们总是追求用有限的资源获取最大的收益。

现在，假设你分别支配着 m 个 0 和 n 个 1。另外，还有一个仅包含 0 和 1 字符串的数组。

你的任务是使用给定的 m 个 0 和 n 个 1 ，找到能拼出存在于数组中的字符串的最大数量。每个 0 和 1 至多被使用一次。

这种问题是一个二维的背包问题，一维的背包问题通过画线型图来进行理解，

对于字符串数组中的每一个字符串，我们进行遍历。

假设对于第k个字符串时，假设在此之前我们用m个0，n个1可以表达m个字符串，那我们如何判断是否需要继续表达这个字符串。假设这个第k个字符串需要a个0，b个1，那么我们就考虑一下如果我们的m个0，n个1没有这a个0，b个1的情况下可以表示多少字符串，再加1，如果得到的值大于我们现在可以表达的数量，就取这个值，否则不变。

```java
public class Solution{
    public int findMaxForm(String[] strs, int m, int n){
        int[][] map = new int[m+1][n+1];
        for(String s : strs){
            int[] count = countZeroesOnes(s);
            for(int i = m; i >= count[0]; i--){
                for(int j = n; j >= count[1]; j--){
                    map[i][j] = Math.max(1+map[i-count[0]][j-count[1]], map[i][j]);
                }
            }
        }
   		return map[m][n];
    }
    public int[] countZeroesOnes(String s){
        int[] result = new int[2];
        for(int i = 0; i < s.length(); i++){
 			result[s.charAt(i) - '0']++;           
        }
        return result;
    }
}
```

