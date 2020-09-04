## 图遍历算法-DFS和BFS

在学习图的时候，我们接触到了两种算法DFS和BFS，对于这两种算法，他们在思想上有较大差异并且使用也非常的不同。

### 1.DFS和BFS不同之处

DFS用通俗的话来说就是宣扬一种不撞南墙不回头的精神。从初始点出发，沿着一条方向，一直到该方向走通或者走不通，然后回到初始点，从初始点的另一个方向继续出发，如此往复，直到走完所有的方向。

<img src="https://s1.ax1x.com/2020/09/03/wCnNhd.gif" alt="wCnNhd.gif" style="zoom:50%;" />

​											  ~（图片源自https://cuijiahua.com/blog/2018/01/alogrithm_10.html）~

BFS则是一种“海王”精神，从初始点出发，判断初始点周围的所有方向是否都可以满足条件，从中选出满足条件的点，并且以这些点作为新的初始点并且寻找在这些点附近满足条件的点,如下图所示。

<img src="https://s1.ax1x.com/2020/09/03/wCZKpt.gif" alt="wCZKpt.gif" style="zoom:50%;" />

​                                             ~（图片源自https://cuijiahua.com/blog/2018/01/alogrithm_10.html）~

### 2.DFS和BFS优缺点

DFS的实现方法是通过采用**栈**和**递归**来实现的，这种一条路走到黑的风格也比较容易被人脑所理解，适用的问题对象往往是要求得到**所有的解**或者判断**连通性**的问题。由于采用了递归的方式避免了空间上的占用，因此递归的轮数不能过大，否则效率会大大降低，可以归类为一种**时间换空间**的做法。

BFS的实现方法是通过**队列**进行入队和出队的操作来实现的。由于它例举出了每个层次下所有的可能性，因此这种问题比较适合**最优解**的问题，由于采用了队列的数据结构避免了递归，因此它可以处理一些规模较大的数据，属于一种**空间换时间**的做法。

### 3.例题，解法

剑指 Offer 13. 机器人的运动范围 https://leetcode-cn.com/problems/ji-qi-ren-de-yun-dong-fan-wei-lcof/

这道题既可以通过BFS也可以通过DFS来解决，这两种解法在大多数情况下都是同时出现的。

#### BFS

```java
class Solution {
    public int movingCount(int m, int n, int k) {
    	boolean[][] visited = new boolean[m][n];
        Queue<int[]> queue = new LinkedList<>();
        queue.offer(new int[]{0, 0});
        int index = 0;
        while(!queue.isEmpty()){
            int[] cur = queue.poll();
            int x = cur[0], y = cur[1];
            if(x >= m || y >= n || !expandOrNot(cur, k) || visited[x][y]){
                continue;
            }
            visited[x][y] = true;
            index++;
            queue.offer(new int[]{x+1, y});
            queue.offer(new int[]{x, y+1});
        }
        return index;
    }
    public boolean expandOrNot(int[] cur, int k){
        int x0 = cur[0] / 10;
        int y0 = cur[0] % 10;
        int x1 = cur[1] / 10;
        int y1 = cur[1] % 10;
        return (x0+y0+x1+y1)>k?false:true;
    }
}
```

#### DFS

```java
class Solution {
    int m;
    int n;
    boolean[][] visited;
    int k;
    public int movingCount(int m, int n, int k) {
        this.m = m;
        this.n = n;
        this.k = k;
        this.visited = new boolean[m][n];
        return dfs(0, 0);
    }
    public int dfs(int x, int y){
        if(x >= m || y >= n || !expandOrNot(new int[]{x, y}, k) || visited[x][y]){
            return 0;
        }
        visited[x][y] = true;
        return 1 + dfs(x+1, y) + dfs(x, y+1);
    }
    public boolean expandOrNot(int[] cur, int k){
        int x0 = cur[0] / 10;
        int y0 = cur[0] % 10;
        int x1 = cur[1] / 10;
        int y1 = cur[1] % 10;
        return (x0+y0+x1+y1)>k?false:true;
    }
}
```

