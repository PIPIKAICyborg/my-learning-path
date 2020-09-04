## 剑指 Offer 13. 机器人的运动范围

地上有一个m行n列的方格，从坐标 [0,0] 到坐标 [m-1,n-1] 。一个机器人从坐标 [0, 0] 的格子开始移动，它每次可以向左、右、上、下移动一格（不能移动到方格外），也不能进入行坐标和列坐标的数位之和大于k的格子。例如，当k为18时，机器人能够进入方格 [35, 37] ，因为3+5+3+7=18。但它不能进入方格 [35, 38]，因为3+5+3+8=19。请问该机器人能够到达多少个格子？

#### **解体思路**

这道题我们可以通过BFS算法，通过一种扩展的方式来实现。

此处我们需要一个记忆矩阵来帮助我们确定哪些点是我们已经访问过的。

```java
class Solution {
    public int movingCount(int m, int n, int k) {
        boolean[][] visited = new boolean[m][n];
        Queue<int[]> list = new LinkedList<>();
        list.offer(new int[]{0, 0});
        int index = 0;
        while(!list.isEmpty()){
            int[] cur = list.poll();
            int x = cur[0], y = cur[1];
            if(x >= m || y >=n || !expandOrNot(cur, k) || visited[x][y]){
                continue;
            }
            visited[x][y] = true;
            index++;
            list.offer(new int[]{x+1, y});
            list.offer(new int[]{x, y+1});
        }
        return index;
    }
    public boolean expandOrNot(int[] cur, int k){
        int i = cur[0] / 10;
        int j = cur[0] % 10;
        int m = cur[1] / 10;
        int n = cur[1] % 10;
        if(i + j + m + n > k){
            return false;
        }else{
            return true;
        }
    }
}
```

