



# 一、如何使用终端操作数据库

## 1.查询数据库服务器中所有的数据库

```mysql
->show databases;
```

[![img](https://flyergw.top/studyofMySql/1.png)](https://flyergw.top/studyofMySql/1.png)

## 2.在数据库服务器中创建数据库

```mysql
->create database sqlname;
```

[![img](https://flyergw.top/studyofMySql/2.png)](https://flyergw.top/studyofMySql/2.png)

## 3.选中一个数据库进行操作

1.先选中：

```mysql
->use sqlname;
```

2.检索信息：

```mysql
->SELECT *what_to_select*
->FROM *which_table*
->WHERE *conditions_to_satisfy;*
```

**注：**what_to_select指出你想要看到的内容，可以是列的一个表，或”*“表示“所有的列”。which_table指出你想要从其检索数据的表。WHERE子句是可选项，如果选择该项，conditions_to_satisfy指定行必须满足的检索条件。
查询语句：select * from tablename;
**MySQL提供了几个函数，可以用来计算日期，例如，计算年龄或提取日期部分。**

3.查看数据表：

```mysql
->show tables;
```

4.创建一个数据表：

数据表命名格式：

（1）采用26个英文字母(区分大小写)和0-9的自然数(经常不需要)加上下划线'_'组成，命名简洁明确，多个单词用下划线'_'分隔

（2）全部小写命名，禁止出现大写

（3）禁止使用数据库关键字，如：name，time ，datetime，password等

```mysql
->CREATE TABLE people();表中分割用“,”;
```

[![img](https://flyergw.top/studyofMySql/3.png)](https://flyergw.top/studyofMySql/3.png)

[![  ](https://flyergw.top/studyofMySql/4.png)](https://flyergw.top/studyofMySql/4.png)

5.查看数据表

查看数据表的具体结构：

```mysql
->DESCRIBE tablename;
```

[![img](https://flyergw.top/studyofMySql/5.png)](https://flyergw.top/studyofMySql/5.png)

查看数据表具体信息：

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

其中默认的列值分隔符和行尾标记是定位符（tab）和换行符(\r\n)。

6.删除数据表：

```mysql
drop table tablename;
```

6.往数据表中添加记录：

基本语法格式：   

```mysql
INSERT INTO 表名(字段1,字段2,...,字段m) VALUES(值1,值2,...,值m);
```

- 为表的所有字段添加数据
- 为表的指定字段添加数据
- 同时添加多条记录

```mysql
->INSERT INTO tablename
 -> VALUES('王一','男','2005.01.01');
```

[![img](https://flyergw.top/studyofMySql/6.png)](https://flyergw.top/studyofMySql/6.png)

[![img](https://flyergw.top/studyofMySql/7.png)](https://flyergw.top/studyofMySql/7.png)
**==注：==**这里字符串和日期值均为引号扩起来的字符串。
*将文本文件装载到表中：*
eg:将路径下的pet.txt文本文件装载到表pet中：

```mysql
->LOAD DATA LOCAL INFILE '/path/pet.txt' INTO TABLE pet;
```

其中默认的列值分隔符和行尾标记是定位符（tab）和换行符(\r\n)。
**注：**想要一次增加一个新记录，可以使用INSERT语句。

7.常用数据类型 
数值：TINYINT,SMALLINT,MEDIUMINT,INT,BIGINT,FLOAT,DOUBLE,DECIMAL…
日期/时间：DATE,TIME,YEAR,DATETIME,TIMESTAMP…
字符串（字符）：CHAR,VARCHAR,TINYBLOB,TINYTEXT,BLOB,TEXT,MEDIUMBLOB,MEDIUMTEXT,LONGBLOB,LONGTEXT…
日期选择按照格式，数值、字符（串）选择按照大小。

8.删除数据：

```mysql
->DELETE FROM tablename WHERE name='王一';
```

[![img](https://flyergw.top/studyofMySql/8.png)](https://flyergw.top/studyofMySql/8.png)

9.修改数据：UPDATE,UPDATE只更改有问题的记录，不需要重新装载数据库表。

```
->UPDATE pet SET birth = '1989-08-31' WHERE name = 'Bowser';
```

10.模式匹配：SQL模式匹配允许你使用“_”匹配任何单个字符，而“%”匹配任意数目字符(包括零字符)。 SQL的模式默认是忽略大小写的,注意使用SQL模式时，不能使用=或!=；而应使用LIKE或NOT LIKE比较操作符。

```
->mysql> SELECT * FROM pet WHERE name LIKE 'b%';(找出以“b”开头的名字)
->SELECT * FROM pet WHERE name LIKE '%fy';(找出以“fy”结尾的名字)
->SELECT * FROM pet WHERE name LIKE '%w%';(找出包含“w”的名字)
->SELECT * FROM pet WHERE name LIKE '_____';(找出正好包含5个字符的名字，使用“\_”模式字符)
```

**扩展：**

- ‘.’匹配任何单个的字符。
- 字符类“[…]”匹配在方括号内的任何字符。例如，“[abc]”匹配“a”、“b”或“c”。为了命名字符的范围，使用一个“-”。“[a-z]”匹配任何字母，而“[0-9]”匹配任何数字。
- “*”匹配零个或多个在它前面的字符。例如，“x*”匹配任何数量的“x”字符，“[0-9]*”匹配任何数量的数字，而“.*”匹配任何数量的任何字符。

## 4.退出数据库服务器

```
->exit;
```

## 5.建表约束

1. 主键约束（primary key）：唯一确定一张表中的一条记录，即通过给某个字段添加约束，就可以使得该字段不重复且不为空。
   联合主键约束：只要联合起来的主键加起来不重复即可。
2. 自增约束（auto_increment）:可以自动增加序列，eg:1,2,3…
3. 唯一约束（unique）：约束修饰的字段的值不可重复。
4. 非空约束（not null）：修饰的字段不能为空。
5. 默认约束（default）：当插入字段值的时候，如果没有传值，就会使用默认值，传了值则不会使用默认值。
6. 外键约束（foreign key）：涉及到两个表，父表、子表;子表收到父表内容的约束；父表的记录被子表引用，则不可以被删除。

## 数据库的三大设计范式

1. 第一范式：数据表中的所有字段都是不可分割的原子值，字段值还可以继续拆分的则不满足第一范式。
2. 第二范式：满足第一范式的前提下，第二范式要求，除主键外的每一列都必须完全依赖于主键；如果要出现不完全依赖，只可能发生在联合主键的
   情况下。
3. 第三范式：必须先满足第二范式，除开主键列的其他列不能有传递依赖关系。

# 二、如何使用可视化工具操作数据库

# 三、如何在编程语言中操作数据库

# 四、MySql的两个基础对象

## 1.MySqlConnection对象：用于和数据库建立连接，它接收一个连接用的字符串，返回一个MySqlConnection对象。

```
string connStr = "server = localhost; user = root; database = test; port = 3306; password = ***"
MySqlConnection conn = new MySqlConnection(connStr) ;
try{conn.Open();}
catch(Exception ex){Console.WriteLine(ex.ToString());}
```

## 2. MySqlCommand对象：用于把SQL语句传送到数据服务器执行,MySqlCommand对象实例化时接收两个参数：SQL语句（命令）以及和数据库的连接，即MySqlConnection连接对象。

MySqlCommand 对象常用的三个执行方法:

1. ExecuteReader:调用ExecuteReader方法来查询数据库,返回一个包含着查询结果的MySqlDataReader对象。

   ```c#
   MysqlCommand cmd = new MySqlCommand(sql, conn) ;
   MySqlDataReader rdr = cmd.ExecuteReader();
   while(rdr.Read())
   {
       Console.WriteLine(rdr[0] + " -- " + rdr[1]) ;
   }
   rdr.Close() ;
   ```

2. ExecuteNonQuery:调用ExecuteNonQuery来插入和删除数据。

   ```c#
   string sql = "INSERT INTO writer value(...)" ;
   MySqlCommand cmd = new MySqlCommand(sql, conn);
   cmd.ExecuteNonQuery();
   ```

3. ExecuteScalar:仅返回单个值。

   ```c#
   sql = "SELECT COUNT(*) FROM writer;"  ;
   MySqlCommand cmd = new MySqlCommand(sql, conn) ;
   object result = cmd.ExecuteScalar();
   if(result != null)
   {
       int r = Convert.ToInt32(result) ;
       ...
   }
   ```

**总结：**使用MySQL的基本步骤：

1. 使用账号密码等连接数据库创建MySqlConnection对象
2. 将命令以及连接对象传给命令构造器MySqlCommand
3. 调用命令构造器的执行方法如,executeReader

# 五、处理解耦数据

希望仅在需要连接数据库时才连接。

1. 数据集：DataSet类，一个DataSet对象被实例化后，可以用来处理多个表的数据。

   ```
   DataSet dsCountry;
   ...
   dsCountry = new DataSet() ;
   ```

2. 数据适配器：数据适配器是连接数据集以及数据库之间的一个接口。数据适配器负责打开、关闭以及管理数据库的连接。 可以通过实例化MySqlDataAdapter对象来创建一个数据适配器。 数据适配器有两个主要的方法：
   Fill 方法：将数据库中的数据取出，装入数据集
   Update：方法将数据集中的数据定入数据库中

   ```
   MySqlDataAdapter adapter ;
   ...
   string sql = "SELECT Code, Name, HeadOfState FROM Country WHERE Continent = 'North America'" ;
   adapter = new MySqlDataAdapter(sql, conn) ;
   ```

3. 命令建造器：可以通过实例化MySqlCommandBuilder来创建一个命令建造器，命令建造器是一个支持对象，命令建造器需要跟数据适配器一起协作。当一个MySqlDataAdapter被创建的时候，通常会给他一个初始的 SELECT 语句。根据这个 SELECT 语句，命令建造器可以判断出相应的 INSERT, UPDATE 和 DELETE 语句的格式。 这样，当你执行Update方法时，数据适配器就能够自动地把更改的数据更新到你的SQL数据库中去。
   一个命令建造器被创建之后，我们需要生成一些附加的语句提供给它，以用来插入、更新和删除数据。我们在这里只用最简单的一种方法：把适配器传给命令建造器。

   ```
   MySqlCommandBuilder cb = new MySqlCommandBuilder(adapter) ;
   ```

4. 把数据装入数据集:我们使用适配器的 Fill 方法来获取数据库中的数据然后装载入数据集中。 适配器会自动与数据库连接并获取数据。 第二个参数”Country”指明要装载、修改的表。

   ```
   DataSet dsCountry ;
   ...
   dsCountry = new DataSet() ;
   ...
   daCountry.Fill(dsCountry, "Country") ;
   ```

5. 更新数据集的数据到数据库:我们使用适配器的 Update 方法将数据集中被改变的数据写回到数据库中。

   ```
   adapter.Update(dsCountry, "Country") ;
   ```

**总结：**整个过程

- 创建连接实例

  ```
  string connStr = "server=localhost;user=root;database=world;port=3306;password=***";
  MySqlConnection conn = new MySqlConnection(connStr) ;
  ```

- 使用连接实例以及SELECT语句初始化适配器

  ```
  string sql = "SELECT Code, Name, HeadOfState FROM Country WHERE Continent = 'North America'" ;
  adapter = new MySqlDataAdapter (sql, conn) ;
  ```

- 使用适配器初始化命令建造器

  ```
  MySqlCommandBuilder cb = new MySqlCommandBuilder(adapter) ;
  ```

- 创建数据集

  ```
  DataSetCountry = new DataSet();
  ```

- 把数据库中的 Country 表加载进数据集

  ```
  adapter.Fill(DataSetCountry, "Country") ;
  ```

- 设置控件dataGridView的数据来源

  ```
  dataGridView1.DataSource = DataSetCountry ;
  dataGridView1.DataMember = "Country" ;
  adapter.Update(DataSetCountry, "Country") ;
  ```

# 六、数据库理论知识

## 访问方式：

1. 直接数据访问：不需要在内存中保存信息副本，当数据库打开连接时，可以在一段较短时间内维持与数据库的交互，然后数据库连接就会迅速断开。
2. 不连接数据访问：在内存中的DateSet对象保存数据的副本，在数据库连接断开后仍然能够操作这些数据。不连接方式最大的好处即是可以占据尽可能少的数据库连接资源。

## 数据库连接：

需要把数据库操作的代码写在try-catch结构中以对可能发生的错误进行处理，并在代码中确保关闭数据库连接。

