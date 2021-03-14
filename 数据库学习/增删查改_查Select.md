# 查询select

## 一、查看数据表具体信息：

- 查询所有字段

  ```c#
  select * from 表名;
  select * from students;
  select id,name from classes;
  ```

- 查询指定字段

  ```c#
  select 列1,列2,… from 表名;
  select age,name from students;
  ```

- 使用as给字段起别名

  ```c#
  select name as 姓名, age as 年龄 from students;
  select age as 年龄, name as 姓名 from students;
  ```

- select 表名.字段 … from 表名;

  ```c#
  select students.name, students.age from students;
  select s.name,s.age from students as s;
  select students.name, students.age from students as s;(失败)
  ```

  ## 二、条件查询：

  1、比较运算

    

  ```c#
  select … from 表名 where …
  //查询大于18岁的信息
  select * from students where age>18;
  select id,name,gender from students where age>18;
  //查询等于18岁的信息
  select * from stundents where age=18;
  ```

  2、逻辑运算符

  - and

  ```c#
  //18到28之间的所以学生信息
  select * from students where age>18 and age<28;
  失败select * from students where age>18 and <28;
  //18岁以上的女性
  select * from students where age>18 and gender=“女”;
  select * from students where age>18 and gender=2;
  ```

  