第一场周赛，用的是JAVA语言

呜呜┭┮﹏┭┮，一个半小时，才ac了一道题目，得好好总结一下。

第一题，5906.句子中的有效单词数

满足条件的匹配

我的做法：

```java
class Solution {
    public int countValidWords(String sentence) {
        int ans = 0;
        sentence = sentence.trim();
        String[] token = sentence.split(" ");
        for (int i = 0; i < token.length; i++) {
            if (token[i].startsWith("-") || token[i].endsWith("-")) continue;
            int count = 0;
            boolean flag = true;
            for (int j = 0; j < token[i].length(); j++) {
                char c = token[i].charAt(j);
                if (c >= 'a' && c <= 'z') continue;
                else if (c == '-' && token[i].charAt(j-1) >= 'a' && token[i].charAt(j-1) <= 'z' && token[i].charAt(j+1) >= 'a' && token[i].charAt(j+1) <= 'z') count++;
                else if ((c == '.' || c == ',' || c == '!') && j == token[i].length()-1) continue;
                else {
                    flag = false;
                    break;
                }
                if (count >= 2) {
                    flag = false;
                    break;
                }
            }
            if (token[i].length() == 0) flag = false;
            if (flag) ans++;
        }
        return ans;
    }
}
```

看了一位大佬的做法：

```java
class Solution {
    public int countValidWords(String sentence) {
        int count = 0;
        for (String s : sentence.split(" ")) {
            if (!s.isEmpty() && s.matches("[a-z]*([a-z]-[a-z])?[a-z]*[!.,]?")) {
                count++;
            }
        }
        return count;
    }
}
```

差距分析：

我用的是枚举方法。。

而大佬用的是正则表达式匹配的方法。。（好好看好好学。。）

？：0次或1次

*：0次或多次

+：一次或多次

{n}：正好n次

{n,}：至少出现n次

{n,m}：出现n~m次

5907.下一个更大的数值平衡数

```java
class Solution {

    public int nextBeautifulNumber(int n) {
        while (nextBeautifulNumber(("" + ++n).toCharArray())) {
        }
        return n;
    }

    private boolean nextBeautifulNumber(char[] n) {
        int[] count = new int[10];
        for (char c : n) {
            count[c - '0']++;
        }
        for (int i = 0; i < 10; i++) {
            if (count[i] > 0 && count[i] != i) {
                return true;
            }
        }
        return false;
    }
}
```

暴力枚举。。。好吧。。

String的方法.toCharArray()

听说可以枚举打表，🐂

5908.统计最高分的节点数目

```java
class Solution {

    public int countHighestScoreNodes(int[] parents) {
        ArrayList<Integer>[] list = new ArrayList[parents.length];
        for (int i = 0; i < list.length; i++) {
            list[i] = new ArrayList<>();
        }
        for (int i = 1; i < parents.length; i++) {
            list[parents[i]].add(i);
        }
        TreeMap<Long, Integer> map = new TreeMap<>();
        countHighestScoreNodes(0, new int[parents.length], map, list);
        return map.lastEntry().getValue();
    }

    private void countHighestScoreNodes(int index, int[] count, TreeMap<Long, Integer> map, ArrayList<Integer>[] list) {
        long product = count[index] = 1;
        for (int i : list[index]) {
            countHighestScoreNodes(i, count, map, list);
            count[index] += count[i];
            product *= count[i];
        }
        product *= Math.max(1, count.length - count[index]);
        map.put(product, map.getOrDefault(product, 0) + 1);
    }
}
```

