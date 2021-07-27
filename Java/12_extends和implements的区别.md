# extends和implements的区别

- 在类的声明中，通过关键字extends来创建一个类的子类；extends 是继承某个类, 继承之后可以使用父类的方法, 也**可以重写父类的方法**；
- 一个类通过关键字implements声明自己使用一个或者多个接口；implements 是实现多个接口, **接口的方法一般为空的, 必须重写才能使用**；
- Java中**不支持多重继承**，但是可以用接口 来实现，这样就要用到implements，继承只能继承一个类；但implements可以实现多个接口，用逗号分开就行；

```java
class A extends B implements C,D,E
```

