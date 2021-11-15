如求Cmn(m为上，n为下)
```java
long ans = 1L;
for (int x = n, y = 1; y <= m; y++, n--) {
    ans = (ans * x)/y;
}
return (int)ans;
```