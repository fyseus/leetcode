第二场
第一题（打卡题）
```java
class Solution {
    public int smallestEqual(int[] nums) {
        for (int i = 0; i < nums.length; i++) {
            if (i % 10 == nums[i]) return i;
        }
        return -1;
    }
}
```
第二题：
```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    public int[] nodesBetweenCriticalPoints(ListNode head) {
        int count = 0, begin = 0, last = 0, point = 0;
        int minDistance = Integer.MAX_VALUE, maxDistance = 0;
        int previousVal = head.val, midVal = 0, lastVal = 0;
        head = head.next;
        while (head.next != null) {
            midVal = head.val;
            lastVal = head.next.val;
            if ((midVal < previousVal && midVal < lastVal) || (midVal > previousVal && midVal > lastVal)) {
                count++;
                if (count == 1) {
                    begin = point;
                } else {
                    minDistance = Math.min(minDistance, point - last);
                }
                last = point;
            }
            point++;
            previousVal = midVal;
            head = head.next;
        }
        if (count < 2) {
            return new int[]{-1,-1};
        } else {
            return new int[]{minDistance, last - begin};
        }
    }
}
```
第三题（不太会）：
//用到了一个Deque的LinkedList，其中元素为一个数组！！（和map很像，不过是顺序的且可重复）
还用到了一个HashSet
```java
class Solution {
    public int minimumOperations(int[] nums, int start, int goal) {
        // bfs广度优先遍历
        Deque<int[]> queue = new LinkedList<>();
        Set<Integer> set = new HashSet<>();
        queue.addLast(new int[]{start, 0});
        int n = nums.length;
        while (!queue.isEmpty()) {
            int[] temp = queue.removeFirst();
            if (set.contains(temp[0])) {
                continue;
            }
            set.add(temp[0]);
            if (temp[0] == goal) {
                return temp[1];
            }
            for (int i = 0; i < n; i++) {
                if (temp[0] + nums[i] >= 0 && temp[0] + nums[i] <= 1000) {
                    queue.addLast(new int[]{temp[0] + nums[i], temp[1] + 1});
                } else {
                    if (temp[0] + nums[i] == goal) {
                        return temp[1] + 1;
                    }
                }
                if (temp[0] - nums[i] >= 0 && temp[0] - nums[i] <= 1000) {
                    queue.addLast(new int[]{temp[0] - nums[i], temp[1] + 1});
                } else {
                    if (temp[0] - nums[i] == goal) {
                        return temp[1] + 1;
                    }
                }
                if ((temp[0] ^ nums[i]) >= 0 && (temp[0] ^ nums[i]) <= 1000) {
                    queue.addLast(new int[]{(temp[0] ^ nums[i]), temp[1] + 1});
                } else {
                    if ((temp[0] ^ nums[i]) == goal) {
                        return temp[1] + 1;
                    }
                }
            }
        }
        return -1;
    }
}
```
第四题（更不会）：
//没想到竟然是动态规划，dp[i][j]存一个数组，对于每一个dp[i][j]表示的是i与前j个匹配不冲突，但可能长度有差值，对于长度有差值的，数字继续，字母只前进差值方向
注意边界
```java
class Solution {
    public boolean possiblyEquals(String s1, String s2) {
        int n = s1.length(), m = s2.length();
        Set<Integer>[][] dp = new HashSet[n + 1][m + 1];
        for (int i = 0; i <= n; i++) {
            for (int j = 0; j <= m; j++) {
                dp[i][j] = new HashSet<>();
            }
        }
        dp[0][0].add(0);
        for (int i = 0; i <= n; i++) {
            for (int j = 0; j <= m; j++) {
                for (int delta : dp[i][j]) {
                    int num = 0;
                    for (int k = i; k < Math.min(i + 3, n); k++) {
                        if (isDigit(s1.charAt(k))) {
                            num = num * 10 + s1.charAt(k) - '0';
                            dp[k + 1][j].add(num + delta);
                        } else {
                            break;
                        }
                    }
                    num = 0;
                    for (int k = j; k < Math.min(j + 3, m); k++) {
                        if (isDigit(s2.charAt(k))) {
                            num = num * 10 + s2.charAt(k) - '0';
                            dp[i][k + 1].add(delta - num);
                        } else {
                            break;
                        }
                    }
                    if (i < n && delta < 0 && !isDigit(s1.charAt(i))) {
                        dp[i + 1][j].add(delta + 1);
                    }
                    if (j < m && delta > 0 && !isDigit(s2.charAt(j))) {
                        dp[i][j + 1].add(delta - 1);
                    }
                    if (i < n && j < m && delta == 0 && !isDigit(s2.charAt(j)) && s1.charAt(i) == s2.charAt(j)) {
                        dp[i + 1][j + 1].add(delta);
                    }
                }
            }
        }
        return dp[n][m].contains(0);
    }
    public boolean isDigit(char c) {
        return c >= '0' && c <= '9';
    }
}
```