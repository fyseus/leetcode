一般在HashSet中比较都是先比较hashCode后再比较equals，所以两个都得重写
```java
@Override
public int hashCode() {
    return x + y;
}
@Override
public boolean equals(Object obj) {
    if (!(obj instanceof NewPair) || obj == null) {
        return false;
    }
    if (this == obj) {
        return true;
    }
    NewPair pair = (NewPair)obj;
    return pair.x == x && pair.y == y;
}
```