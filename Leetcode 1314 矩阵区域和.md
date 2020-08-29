### Leetcode 1314 矩阵区域和

给你一个 m * n 的矩阵 mat 和一个整数 K ，请你返回一个矩阵 answer ，其中每个 answer[i][j] 是所有满足下述条件的元素 mat[r][c] 的和： 

i - K <= r <= i + K, j - K <= c <= j + K 
(r, c) 在矩阵内。

#### 解题思路

对于该题，我们可以把mat矩阵用两个点并且作这两个点的垂线和水平线来划分区域，(K, K)和(m-1-K, n-1-K)

因为在之后的状态转移中，需要固定的在一定范围内所有mat矩阵元素的和，因此需要一个记忆矩阵提前来存储一下某一点左上角的值。

```java
class Solution {
    public int[][] matrixBlockSum(int[][] mat, int K) {
        int row = mat.length;
        int col = mat[0].length;
        
        int[][] mem = new int[row][col];
        mem[0][0] = mat[0][0];
        for(int i = 1; i < row; i++) mem[i][0] = mem[i-1][0] + mat[i][0]; 
        for(int j = 1; j < col; j++) mem[0][j] = mem[0][j-1] + mat[0][j];
        for(int i = 1; i < row; i++){
            for(int j = 1; j < col; j++){
                mem[i][j] = mem[i-1][j] + mem[i][j-1] - mem[i-1][j-1] + mat[i][j];
            }
        }
        
        int[][] answer = new int[row][col];
        for(int i = 0; i < row; i++){
            for(int j = 0; j < col; j++){
                int x1 = Math.max(0, i-K), x2 = Math.min(row-1, i+K);
                int y1 = Math.max(0, j-K), y2 = Math.min(col-1, j+K);
                answer[i][j] = mem[x2][y2]
                    - (x1==0?0:mem[x1-1][y2])
                    - (y1==0?0:mem[x2][y1-1])
                    + (x1==0||y1==0?0:mem[x1-1][y1-1]);
            }
        }
        return answer;
    }
}
```

