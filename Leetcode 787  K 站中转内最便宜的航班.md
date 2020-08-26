### Leetcode 787  K 站中转内最便宜的航班

有 n 个城市通过 m 个航班连接。每个航班都从城市 u 开始，以价格 w 抵达 v。

现在给定所有的城市和航班，以及出发城市 src 和目的地 dst，你的任务是找到从 src 到 dst 最多经过 k 站中转的最便宜的价格。 如果没有这样的路线，则输出 -1。

#### 解决思路

**运用Dijkstra算法**

用一个小顶堆来保存当前的最小值，并且通过添加是否等于place来判断是否跳出

用一个HashMap来保存各个点在被第几次到达的情况下的最小值。

并通过来比较HashMap中的这个第几次的最小值来确定是否要把当前的情况加入小顶堆，这种比较可以避免放入无意义的路径，如果放入，同时要更新HashMap中这个最小值。

```java
class Solution {
    public int findCheapestPrice(int n, int[][] flights, int src, int dst, int K) {
        int[][] graph = new int[n][n];
        for(int[] flight : flights){
            graph[flight[0]][flight[1]] = flight[2];
        }
        Map<Integer, Integer> hm = new HashMap<Integer, Integer>();
        PriorityQueue<int[]> heap = new PriorityQueue<int[]>((a, b)->a[0]-b[0]);
        heap.offer(new int[]{0, 0, src});
        
        while(!heap.isEmpty()){
            int[] cur = heap.poll();
            int cost = cur[0];
            int k = cur[1];
            int place = cur[2];
            if(k > K+1 || cost > hm.getOrDefault(k * 1000 + place,Integer.MAX_VALUE)){
                continue;
            }
            if(place == dst){
                return cost;
            }
            for(int i = 0; i < n; i++){
                if(graph[place][i] > 0){
                    int newcost = cost + graph[place][i];
                	if(newcost < hm.getOrDefault((k+1) * 1000 + i,Integer.MAX_VALUE)){
                    	hm.put((k+1) * 1000 + i, newcost);
                    	heap.offer(new int[]{newcost, k+1, i});
                	}
                }
            }
        }
        return -1;
    }
}


```

