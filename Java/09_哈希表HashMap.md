# HashMap

1. getOrDefault() 方法获取指定 key 对应对 value，如果找不到 key ，则返回设置的默认值。

getOrDefault() 方法的语法为：

```java
hashmap.getOrDefault(Object key, V defaultValue)
```

## 遍历Map对象

1. **在for-each循环中使用entries来遍历**

```java

Map<Integer, Integer> map = new HashMap<Integer, Integer>();

for (Map.Entry<Integer, Integer> entry : map.entrySet()) {
    System.out.println("Key = " + entry.getKey() + ", Value = " + entry.getValue());
}
```

2. **在for-each循环中遍历keys或values**

```java

Map<Integer, Integer> map = new HashMap<Integer, Integer>();

//遍历map中的键
for (Integer key : map.keySet()) {
    System.out.println("Key = " + key);
}
 
//遍历map中的值
for (Integer value : map.values()) {
    System.out.println("Value = " + value);
}
```

3. **使用Iterator遍历**

```java
Map<Integer, Integer> map = new HashMap<Integer, Integer>();
Iterator<Map.Entry<Integer, Integer>> entries = map.entrySet().iterator();
 
while (entries.hasNext()) {
    Map.Entry<Integer, Integer> entry = entries.next();
    System.out.println("Key = " + entry.getKey() + ", Value = " + entry.getValue());
}
```



4. **通过键找值遍历（效率低）**

```java
Map<Integer, Integer> map = new HashMap<Integer, Integer>();
 
for (Integer key : map.keySet()) {
    Integer value = map.get(key);
    System.out.println("Key = " + key + ", Value = " + value);
}
```

