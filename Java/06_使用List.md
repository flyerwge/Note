# 使用List

```java
A:添加功能
boolean add(E e):向集合中添加一个元素
void add(int index, E element):在指定位置添加元素
boolean addAll(Collection<? extends E> c)：向集合中添加一个集合的元素。
    
B:删除功能
void clear()：删除集合中的所有元素
E remove(int index)：根据指定索引删除元素，并把删除的元素返回
boolean remove(Object o)：从集合中删除指定的元素
boolean removeAll(Collection<?> c):从集合中删除一个指定的集合元素。

C:修改功能
E set(int index, E element):把指定索引位置的元素修改为指定的值，返回修改前的值。

D:获取功能
E get(int index)：获取指定位置的元素
Iterator iterator():就是用来获取集合中每一个元素。

E:判断功能
boolean isEmpty()：判断集合是否为空。
boolean contains(Object o)：判断集合中是否存在指定的元素。
boolean containsAll(Collection<?> c)：判断集合中是否存在指定的一个集合中的元素。

F:长度功能
int size():获取集合中的元素个数

G:把集合转换成数组
Object[] toArray():把集合变成数组。

```

## 遍历List的三种方法

```java
方法一：
超级for循环遍历
for(String attribute : list) {
  System.out.println(attribute);
}
方法二：
对于ArrayList来说速度比较快, 用for循环, 以size为条件遍历:
for(int i = 0 ; i < list.size() ; i++) {
  system.out.println(list.get(i));
}
方法三：
集合类的通用遍历方式, 从很早的版本就有, 用迭代器迭代
Iterator it = list.iterator();
while(it.hasNext()) {
  System.ou.println(it.next);
}
```

