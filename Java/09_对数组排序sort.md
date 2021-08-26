# 对数组排序

1. 导入 java.util.Arrays 包。
2. 使用 Arrays.sort(数组名) 语法对数组进行排序，排序规则是从小到大，即==升序==。

```java
Arrays.sort(nums);
```

3. 降序：

```java
Arrays.sort(nums，Collections.reverseOrder());
```

4. 对二维数组排序

```java
Arrays.sort(intervals, new Comparator<int[]>() {
    public int compare(int[] interval1, int[] interval2) {
        return interval1[0] - interval2[0];  // g
    }
});

```

