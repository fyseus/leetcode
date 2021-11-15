//其中Comparator接口代表一个比较器
int[][] arr = new int[100][4];
Arrays.sort(arr, new Comparator<int[]>() {
    @Override
    public int compare(int[] t0, int[] t1) {
        return t0[1] - t1[1];
    }
});