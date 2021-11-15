创建：
Set<int[]> treeset = new TreeSet<>(new Comparator<int[]>() {
    @Override
    public int compare(int[] t0, int[] t1) {
        return t0[2] - t1[2];
    }
});//从小到大排序
增加：
add()
清空：
clear()
删除：
remove(key)
比较器：
implements Comparable<Student>
@Override
public int compareTo(Student o) {
    int i = this.name.compareTo(o.getName());
   return i==0?0:-i;
}
遍历：
for(int[][] event : treeset)