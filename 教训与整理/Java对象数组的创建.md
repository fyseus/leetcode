//先创建数组，再对每一个进行初始化
Set<Integer>[][] dp = new HashSet[n][m];
for (int i = 0; i < n; i++) {
    for (int j = 0; j < m; j++) {
        dp[i][j] = new HashSet<>();
    }
}