基于贪心和动态规划求一个图中所有点到所有点最短路径的算法，时间复杂度O(n^3)
# 要点
以每个点为中转站，刷新所有入度和出度的距离
distance[][]：用来存储每个点到其他点的最短距离
path[][]：用来存储每个点到其他点最短距离的路径
遍历每个顶点->遍历点的每一个入度->遍历点的每一个出度
# 初始化
初始化距离distance为图结构graph
# 具体操作
以每个点为入度、出度，重新刷新距离矩阵，并更新最短路径矩阵，基于贪心和动态规划，每次更新的结果可以被下一次遍历使用，得到最终结果即为答案
# 代码
```java
void floyd(int[][] graph) {
    // int[][] distance = graph;
    int[][] path = new int[graph.length][graph.length];
    // 初始化路径
    for (int i = 0; i < graph.length; i++) {
        for (int j = 0; j < graph[i].length; j++) {
            path[i][j] = j;
        }
    }
    // 开始Floyd算法
    // 每个点为中转
    for (int i = 0; i < graph.length; i++) {
        // 所有入度
        for (int j = 0; j < graph.length; j++) {
            // 所有出度
            for(int k = 0; k < graph[j].length; k++) {
                if (graph[j][i] != -1 && graph[i][k] != -1) {
                    int newDistance = graph[j][i] + graph[i][k];
                    if(newDistance < graph[j][k] || graph[j][k] == -1) {
                        graph[j][k] = newDistance;
                        path[j][k] = i;
                    }
                }
            }
        }
    }
```
