1. 字符串
整数转字符串
String str = String.valueOf(a);
字符串转数组
char[] chars = str.toCharArray();
字符串长度:
int lenght = str.length();
字符串获取某个字符：
char c = str.charAt(i);
字符串替换
str.replace('a','b');
字符串去除空格
str.trim();
字符串拼接
StringBuilder sb = new StringBuilder();
sb.append(a);
sb.length(a);
sb.deleteCharAt(index);
截取字符串
str.substring(start,end) 含前不含后，也可以只有
str.substring(start)
字符串获取某个字符的位置
str.indexOf('a')
字符串分割
str.split("\\s+");按空格分割
list/deque重组成String
String.join("",list);
String.join("",deque);
2. 数组
数组初始化：
char[] array = new char[len];
int[] arr = {1,2,3};
int[] arr = new int[]{1,2,3,4,5,6};
数组长度：
int length = arr.length;
数组拷贝:
T[] target = Arrays.copyOfRange(T[] original,int start,int to)
含前不含后
public static void arraycopy(Object src, int srcPos, Object dest, int destPos, int length)
src:源数组;
srcPos:源数组要复制的起始位置;
dest:目的数组;
destPos:目的数组放置的起始位置;
length:复制的长度.
数组自定义排序：
Arrays.sort(nums,new Comparator<Integer>(){
    public int compare(Integer a,Integer b){
        return b-a;
    }
});
数组转list
(1)ArrayList<String> arrayList = new ArrayList<String>(Arrays.asList(arrays));
(2)List<String> list = Arrays.asList(arrays);
(3)List<String> list2 = new ArrayList<String>(arrays.length);
Collections.addAll(list2,arrays);
Array根据元素查找位置
int positon = Arrays.binarySearch(arrays, "f");  
array中填充元素
 Arrays.fill(array, Integer.MAX_VALUE);
3. list列表相关
基本类型数组转成包装类型List：
int[] nums = {1,2,3};
Arrays.stream(nums).boxed().collect(Collectors.toList());
list转数组(只适用于list成员是包装类型)
String[] strs = list.toArray(new String[list.size()])
list复制
targetList.addAll(sourceList);
list自定义排序
Collections.sort(list,new Comparator<Integer>(){
    @override
    public int compare(Integer o1,Integer o2){
        return o1-o2;
    }
})
list翻转
Collections.reverse(list);
list按位置移除元素
list.remove(index);
list按位置获取元素
list.get(index);
list获取某个元素的位置
list.indexOf(value) 默认返回第一个元素所在的位置
list添加元素
list.add(value)在队尾添加
list.add(place,value);//在指定位置添加
4. 栈
栈初始化
Stack stack = new Stack();
栈插入元素
stack.push();
栈弹出元素
stack.pop();
栈取栈顶元素,不删减元素
stack.peek();
判断栈是不是空
stack.isEmpty()
5. 队列
Queue<String> queue = new LinkedList<String>();
队列插入元素
queue.offer(element);
队列弹出元素
queue.poll();
队列头元素
queue.peek();
6. 双端队列
双端队列初始化
Deque<String> d = new ArrayDeque<String>();
双端队列队首插入元素
d.offerFirst(ele);
双端队列队尾插入元素
d.offer()
d.offerLast()
双端队列队首弹出元素
deque.pollFirst();
deque.poll();
双端队列队尾弹出元素
deque.pollLast()
7. map
groupItemsMap.computeIfAbsent(group[item],key->new ArrayList<Integer>()).add(item);
8. 函数
Math.max(a,b);
Math.min(a,b);
Math.pow(a,digit);
Random random = new Random();
random.nextInt(2);返回0/1
