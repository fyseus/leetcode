5910. 检查两个字符串是否几乎相等
```java
class Solution {
    public boolean checkAlmostEquivalent(String word1, String word2) {
        Map<Character, Integer> map = new HashMap<>();
        for (int i = 0; i < word1.length(); i++) {
            map.put(word1.charAt(i), map.getOrDefault(word1.charAt(i), 0) + 1);
        }
        for (int i = 0; i < word2.length(); i++) {
            map.put(word2.charAt(i), map.getOrDefault(word2.charAt(i), 0) - 1);
        }
        for (Map.Entry<Character, Integer> entry : map.entrySet()) {
            if (Math.abs(entry.getValue()) > 3) return false;
        }
        return true;
    }
}
```
5911. 模拟行走机器人 II
```java
class Robot {

    String[] dirs;
    int currentDir;
    int width, height;
    int pointW, pointH;
    public Robot(int width, int height) {
        this.height = height - 1;
        this.width = width - 1;
        pointW = 0;
        pointH = 0;
        dirs = new String[4];
        dirs[0] = new String("East");
        dirs[1] = new String("North");
        dirs[2] = new String("West");
        dirs[3] = new String("South");
        currentDir = 0;
    }
    
    public void move(int num) {
        if (num >= (height + width) * 2) {
            num %= (height + width) * 2;
            if (pointH == 0 && pointW == 0) {
                currentDir = 3;
            }
            if (pointH == 0 && pointW == width) {
                currentDir = 0;
            }
            if (pointH == height && pointW == width) {
                currentDir = 1;
            }
            if (pointH == height && pointW == 0) {
                currentDir = 2;
            }
        }
        while (num != 0) {
            switch(currentDir) {
                case 0 :
                    if (num > width - pointW) {
                        num -= width - pointW;
                        currentDir = 1;
                        pointW = width;
                    } else {
                        pointW = pointW + num;
                        num = 0;
                    }
                    break;
                case 1 :
                    if (num > height - pointH) {
                        num -= height - pointH;
                        currentDir = 2;
                        pointH = height;
                    } else {
                        pointH = pointH + num;
                        num = 0;
                    }
                    break;
                case 2 :
                    if (num > pointW) {
                        num -= pointW;
                        currentDir = 3;
                        pointW = 0;
                    } else {
                        pointW = pointW - num;
                        num = 0;
                    }
                    break;
                case 3 :
                    if (num > pointH) {
                        num -= pointH;
                        currentDir = 0;
                        pointH = 0;
                    } else {
                        pointH = pointH - num;
                        num = 0;
                    }
                    break;
                default:
            }
        }
        
    }
    
    public int[] getPos() {
        return new int[]{pointW, pointH};
    }
    
    public String getDir() {
        return dirs[currentDir];
    }
}

/**
 * Your Robot object will be instantiated and called as such:
 * Robot obj = new Robot(width, height);
 * obj.move(num);
 * int[] param_2 = obj.getPos();
 * String param_3 = obj.getDir();
 */* 
```
5912. 每一个查询的最大美丽值
```java
class Solution {
    public int[] maximumBeauty(int[][] items, int[] queries) {
        Arrays.sort(items, new Comparator<int[]>() {
            @Override
            public int compare(int[] t0, int[] t1) {
                return t0[0] - t1[0];
            }
        });
        int n = queries.length;
        int[] ans = new int[n];
        for (int i = 1; i < items.length; i++) {
            items[i][1] = Math.max(items[i - 1][1], items[i][1]);
        }
        for (int i = 0; i < n; i++) {
            int begin = 0, end = items.length - 1;
            while (begin <= end) {
                int mid = (begin + end) / 2;
                if (items[mid][0] > queries[i]) {
                    end = mid - 1;
                } else {
                    begin = mid + 1;
                }
            }
            if(end != -1)ans[i] = items[end][1];
            else ans[i] = 0;
        }
        return ans;
    }
}
```
5913. 你可以安排的最多任务数目
```java
// TreeMap nlog^2(n)
class Solution {
    public int maxTaskAssign(int[] tasks, int[] workers, int pills, int strength) {
        Arrays.sort(tasks);
        TreeMap<Integer, Integer> map = new TreeMap<>();
        for (int worker : workers) {
            map.put(worker, map.getOrDefault(worker, 0) + 1);
        }
        int end = Math.min(tasks.length, workers.length), begin = 0;
        while (begin <= end) {
            int mid = (begin + end) / 2;
            if (isVaild(tasks, new TreeMap<>(map), mid, pills, strength)) {
                begin = mid + 1;
            } else {
                end = mid - 1;
            }
        }
        return end;
    }
    public boolean isVaild(int[] tasks, TreeMap<Integer, Integer> map, int k, int pills, int strength) {
        for (int i = k - 1; i >= 0; i--) {
            if (map.ceilingKey(tasks[i]) != null) {
                map.put(map.ceilingKey(tasks[i]), map.ceilingEntry(tasks[i]).getValue() - 1);
                if (map.get(map.ceilingKey(tasks[i])) == 0) {
                    map.remove(map.ceilingKey(tasks[i]));
                }
            } else if (map.ceilingKey(tasks[i] - strength) != null && pills-- > 0) {
                map.put(map.ceilingKey(tasks[i] - strength), map.ceilingEntry(tasks[i] - strength).getValue() - 1);
                if (map.get(map.ceilingKey(tasks[i] - strength)) == 0) {
                    map.remove(map.ceilingKey(tasks[i] - strength));
                }
            } else {
                return false;
            }
        }
        return true;
    }
}
// 双端队列 nlogn
class Solution {
    public int maxTaskAssign(int[] tasks, int[] workers, int pills, int strength) {
        Arrays.sort(tasks);
        Arrays.sort(workers);
        int end = Math.min(tasks.length, workers.length), begin = 0;
        while (begin <= end) {
            int mid = (begin + end) / 2;
            if (isVaild(tasks, workers, mid, pills, strength)) {
                begin = mid + 1;
            } else {
                end = mid - 1;
            }
        }
        return end;
    }
    public boolean isVaild(int[] tasks, int[] workers, int k, int pills, int strength) {
        Deque<Integer> deque = new ArrayDeque<>();
        int ptr = -1;
        for (int i = workers.length - k; i < workers.length; i++) {
            while (ptr + 1 < k && tasks[ptr + 1] <= workers[i] + strength) {
                deque.addLast(tasks[++ptr]);
            }
            if (deque.isEmpty()) {
                return false;
            }
            if (deque.peekFirst() <= workers[i]) {
                deque.pollFirst();
            } else if (pills > 0) {
                pills--;
                deque.pollLast();
            } else {
                return false;
            }
        }
        return true;
    }
}
```