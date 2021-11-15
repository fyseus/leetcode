5926. 买票需要的时间
```java
class Solution {
    public int timeRequiredToBuy(int[] tickets, int k) {
        int ans = 0;
        for (int i = 0; i < k; i++) {
            if (tickets[i] <= tickets[k]) {
                ans += tickets[i];
            } else {
                ans += tickets[k];
            }
        }
        ans += tickets[k];
        for (int i = k + 1; i < tickets.length; i++) {
            if (tickets[i] <= tickets[k] - 1) {
                ans += tickets[i];
            } else {
                ans += tickets[k] - 1;
            }
        }
        return ans;
    }
}
```
5927. 反转偶数长度组的节点
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
    public ListNode reverseEvenLengthGroups(ListNode head) {
        int count = 0;
        ListNode point = head;
        ListNode slow = head.next, fast = head.next;
        while (slow != null) {
            count++;
            fast = slow;
            if (slow == null) {
                return head;
            }
            int num = 0;
            for (int i = 0; i < count; i++) {
                if (fast.next == null) {
                    break;
                }
                num++;
                fast = fast.next;
            }
            ListNode newSlow = fast.next;
            ListNode oldSlow = slow;
            if (num % 2 == 1) {
                point.next = fast;
                reverse(slow, fast);
                oldSlow.next = newSlow;
                point = oldSlow;
            } else {
                point = fast;
            }
            
            slow = newSlow;
        }
        return head;
        
    }
    public void reverse(ListNode slow, ListNode fast) {
        ListNode prev = slow;
        if (slow == fast) {
            return;
        }
        slow = slow.next;
        while (slow != fast) {
            ListNode temp = slow.next;
            slow.next = prev;
            prev = slow;
            slow = temp;
        }
        slow.next = prev;
    }
}
```
5928. 解码斜向换位密码
```java
class Solution {
    public String decodeCiphertext(String encodedText, int rows) {
        StringBuilder builder = new StringBuilder();
        int lenR = encodedText.length() / rows;
        for (int i = 0; i < lenR; i++) {
            for (int j = i; j < encodedText.length(); j += lenR + 1) {
                builder.append(encodedText.charAt(j));
            }
        }
        String ans = builder.toString();
        int end = ans.length();
        for (int i = end - 1; i >= 0; i--) {
            if (ans.charAt(i) != ' ') {
                end = i + 1;
                break;
            }
        }
        return ans.substring(0, end);
    }
}
```
5929. 处理含限制条件的好友请求
```java
class Solution {
    // 并查集
    int[] father;
    public boolean[] friendRequests(int n, int[][] restrictions, int[][] requests) {
        father = new int[n];
        boolean[] ans = new boolean[requests.length];
        for (int i = 0; i < n; i++) {
            father[i] = i;
        }
        
        for (int i = 0; i < requests.length; i++) {
            int fx = find(requests[i][0]);
            int fy = find(requests[i][1]);
            father[fx] = fy;
            if (isVaild(restrictions)) {
                ans[i] = true;
            } else {
                father[fx] = fx;
                ans[i] = false;
            }
        }
        return ans;
    }
    int find(int u) {
        while (father[u] != u) u = father[u];
        return u;
    }
    void union(int x, int y) {
        int fx = find(x);
        int fy = find(y);
        if (fx != fy) {
            father[fx] = fy;
        }
    }
    boolean isVaild(int[][] restrictions) {
        for (int[] rej : restrictions) {
            if(find(rej[0]) == find(rej[1])) {
                return false;
            }
        }
        return true;
    }
}
```