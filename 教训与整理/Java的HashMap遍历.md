//遍历方法1: 先遍历key , 再取出value
for (String key : map.keySet()) {
    System.out.println("key is "+key);
    System.out.println("value is "+ map.get(key));
}
//遍历方法2: 直接遍历value
for (String value : map.values()) {
    System.out.println("value is "+value);
}
//遍历方法3: 通过遍历entry来取Key和value,推荐的方法!!!
for (Map.Entry<String, String> entry : map.entrySet()) {
    System.out.println("key is "+entry.getKey());
    System.out.println("value is "+ entry.getValue());
}
//遍历方法4: 通过forEach方法直接遍历key和value
map.forEach((key,value)->{
    System.out.println("key is "+ key);
    System.out.println("value is "+ value);
});
要想边遍历边修改，只能通过迭代器来进行
Iterator<Map.Entry<Integer, String>> it = map.entrySet().iterator();
while(it.hasNext()){
    Map.Entry<Integer, String> entry = it.next();
    Integer key = entry.getKey();
    if(key % 2 == 0){}
}