### Leetcode 1139 最大正方形

给一个由若干0和1组成的二维网格grid，请你找出边界全部由1组成的最大正方形子网格，并返回该子网格种的元素数量，如果不存在，则返回0



#### 解题思路：

以某一个点为右下角所能组成正方形的大小，重要标准是从该点起左侧和上方1的个数。

#### 构建状态：

$f[i][j][0]$指代在第i行，第j列的点开始向左连续1的数量

$f[i][j][1]$指代在第i行，第j列的点开始向上连续1的数量

#### 状态迭代：

$if \quad grid[i-1][j-1] ==1 \quad  f[i][j][0] = f[i][j-1][0] + 1$

$if \quad grid[i-1][j-1] ==1 \quad f[i][j][1] = f[i-1][j][1] + 1$

$if \quad grid[i-1][j-1] ==0 \quad  f[i][j][0] = 0$

$if \quad grid[i-1][j-1] ==0 \quad  f[i][j][1] = 0$



通过比较左侧和上方的1的个数，取最小值为目前所能构建的最大正方形的边长

得到边长后，从右下角得到正方形的左下角和右上角

判断左下角上方连续1的数量和右上角左侧连续1的数量是否大于等于目前的边长

是， 输出结果

否，边长减一，继续判断

```java
class Solution:
	public int largest1BorderedSquare(int[][] grid) {
		int m = grid.length;
        int n = grid[0].length;
        int res = 0;
        
        int[][][] map = new int[m+1][n+1][2];
        for(int i = 1; i <= m; i++){
            for(int j = 1; j <= n; j++){
                if(grid[i-1][j-1]==1){
                    map[i][j][0] = map[i][j-1][0] + 1;
                    map[i][j][1] = map[i-1][j][1] + 1;
                    int size = Math.min(map[i][j][0], map[i][j][1]);
                    while(map[i][j-size+1][1] < size || map[i-size+1][j][0] < size){
                        size--;
                    }
					res = Math.max(res, size);
                }
            }
        }
        return res * res;
    }
}
```

