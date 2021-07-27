# Char数组转字符串

1. 直接在构造String时建立

```java
char data[] = {'s', 'g', 'k'}; 
String str = new String(data);
```

2. `valueOf`方法直接转换

```java
char[] cha = {'s','g','h'}; 
String n = String.valueOf(cha);
```

