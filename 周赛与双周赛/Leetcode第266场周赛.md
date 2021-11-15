第一题（5918）：
```java
class Solution {
    public int countVowelSubstrings(String word) {
        int ans = 0;
        Set<Character> set = new HashSet<>();
        set.add('a');
        set.add('e');
        set.add('i');
        set.add('o');
        set.add('u');
        for (int i = 0; i < word.length(); i++) {
            for (int j = i + 5; j <= word.length(); j++) {
                char[] arrs = word.substring(i, j).toCharArray();
                Set<Character> newSet = new HashSet<>();
                for (int k = 0; k < arrs.length; k++) {
                    newSet.add(arrs[k]);
                }
                if (set.equals(newSet)){
                    ans++;
                }
            }
        }
        return ans;
    }
}
```
第二题（5919）：
```java
class Solution {
    public long countVowels(String word) {
        long ans = 0;
        Set<Character> set = new HashSet<>();
        set.add('a');
        set.add('e');
        set.add('i');
        set.add('o');
        set.add('u');
        for (int i = 0; i < word.length(); i++) {
            long temp = set.contains(word.charAt(i)) ? 1L : 0L;
            ans += temp * (i + 1) * (word.length() - i);
        }
        return ans;
    }
}
```
第三题（5920）：
```java
class Solution {
    public int minimizedMaximum(int n, int[] quantities) {
        int m = quantities.length;
        PriorityQueue<int[]> queue = new PriorityQueue<>(new Comparator<int[]>() {
            @Override
            public int compare(int[] t1, int[] t0) {
                return (t0[0] % t0[1] == 0 ? t0[0] / t0[1] : t0[0] / t0[1] + 1) - (t1[0] % t1[1] == 0 ? t1[0] / t1[1] : t1[0] / t1[1] + 1);
            }
        });
        for (int i = 0; i < quantities.length; i++) {
            queue.offer(new int[]{quantities[i], 1});
        }
        n -= m;
        while (n != 0) {
            int[] cur = queue.poll();
            queue.offer(new int[]{cur[0], cur[1] + 1});
            n--;
        }
        int[] res = queue.poll();
        return (res[0] % res[1] == 0 ? res[0] / res[1] : res[0] / res[1] + 1);
    }
}
```
第四题（5921）：
```java
class Solution {
    int ans = 0;
    int[] visited;
    int val;
    public int maximalPathQuality(int[] values, int[][] edges, int maxTime) {
        List<List<int[]>> newEdges = new ArrayList<>();
        for (int i = 0; i < values.length; i++) {
            newEdges.add(new ArrayList<int[]>());
        }
        for (int[] edge : edges) {
            newEdges.get(edge[0]).add(new int[]{edge[1], edge[2]});
            newEdges.get(edge[1]).add(new int[]{edge[0], edge[2]});
        }
        visited = new int[values.length];
        visited[0] = 1;
        val = values[0];
        dfs(values, newEdges, 0, maxTime, 0);
        return ans;
    }
    public void dfs(int[] values, List<List<int[]>> edges, int cost, int maxTime, int beginPoint) {
        if (cost > maxTime) {
            return;
        }
        if (beginPoint == 0) {
            ans = Math.max(ans, val);
        }
        for (int[] cur : edges.get(beginPoint)) {
            if (visited[cur[0]] == 0){
                val += values[cur[0]];
            }
            visited[cur[0]]++;
            dfs(values, edges, cost + cur[1], maxTime, cur[0]);
            visited[cur[0]]--;
            if (visited[cur[0]] == 0){
                val -= values[cur[0]];
            }
        }
    }
    
}
```