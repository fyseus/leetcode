第一题（5898.）：
```java
class Solution {
    public String kthDistinct(String[] arr, int k) {
        Map<String, Integer> map = new HashMap<String, Integer>();
        int count = 0;
        for (int i = 0; i < arr.length; i++) {
            if (map.containsKey(arr[i])) {
                map.put(arr[i], map.get(arr[i]) + 1);
            } else {
                map.put(arr[i], 1);
            }
        }
        for (int i = 0; i< arr.length; i++) {
            if (map.get(arr[i]) == 1) {
                count++;
                if (count == k) {
                    return arr[i];
                }
            }
        }
        return "";
    }
}
```
第二题（超时）：
```java
class Solution {
    public int maxTwoEvents(int[][] events) {
        int n = events.length;
        int ans = 0;
        Arrays.sort(events, new Comparator<int[]>() {
            @Override
            public int compare(int[] t0, int[] t1) {
                return t0[0] - t1[0];
            }
        });
        Set<int[]> treeset = new TreeSet<>(new Comparator<int[]>() {
            @Override
            public int compare(int[] t0, int[] t1) {
                return t1[2] - t0[2];
            }
        });
        for (int i = 0; i < n; i++) {
            int start = events[i][0], end = events[i][1], val = events[i][2];
            int valLast = 0;
            for (int[] event : treeset) {
                if (event[1] < start) {
                    valLast = event[2];
                    break;
                }
            }
            ans = Math.max(ans, val + valLast);
            treeset.add(events[i]);
        }
        return ans;
    }
}
```
第三题（5900.）：
```java
class Solution {
    public int[] platesBetweenCandles(String s, int[][] queries) {
        int[] ans = new int[queries.length];
        int[] nums = new int[s.length()];
        int[] point1 = new int[s.length()];
        int[] point2 = new int[s.length()];
        if(s.charAt(0) == '|'){
            nums[0] = 1;
        } else {
            point1[0] = -1;
        }
        if(s.charAt(s.length() - 1) != '|'){
            point2[s.length() - 1] = -1;
        }
        for (int i = 1; i < s.length(); i++) {
            if (s.charAt(i) == '|'){
                nums[i] = nums[i - 1] + 1;
                point1[i] = i;
            } else{
                nums[i] = nums[i - 1];
                point1[i] = point1[i - 1];
            }
        }
        for (int i = s.length() - 2; i >= 0; i--) {
            if (s.charAt(i) == '|'){
                point2[i] = i;
            } else {
                point2[i] = point2[i + 1];
            }
        }
        for (int i = 0; i < queries.length; i++) {
            int begin = queries[i][0], end = queries[i][1];
            int firstPosition = point2[begin], secondPosition = point1[end];
            if (firstPosition >= secondPosition) continue;
            int de = nums[secondPosition] - nums[firstPosition];
            ans[i] = secondPosition - firstPosition -de;
            
        }
        return ans;
    }
}
```
第四题（不会5901.）：
```java

```