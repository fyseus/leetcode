```java
class Solution {
    public int kInversePairs(int n, int k) {
        // dp[i][j]表示有j个逆序数，1到i的数量
        // dp[i][j] = sum{dp[i - 1][k]} (k -> j - i + 1 to j)
        // 求dp[n][k]
        final int MOD = 1000000007;
        int[][] dp = new int[n + 1][k + 1];
        dp[1][0] = 1;
        for (int i = 2; i <= n; i++) {
            dp[i][0] = 1;
            for (int j = 1; j <= k; j++) {
                if (j - i >= 0) {
                    dp[i][j] = dp[i][j - 1] + dp[i - 1][j] - dp[i - 1][j - i];
                } else {
                    dp[i][j] = dp[i][j - 1] + dp[i - 1][j];
                }
                if (dp[i][j] > 1000000007) {
                    dp[i][j] -= 1000000007;
                } else if (dp[i][j] < 0) {
                    dp[i][j] += 1000000007;
                }
            }
        }
        return dp[n][k];
    }
}
```