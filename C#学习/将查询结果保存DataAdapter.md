# 将查询结果保存

DataAdapter 类用于将数据表中的数据查询出来并添加到 DataSet 中

## 一、SqlDataAdapter常用构造方法与属性

| 构造方法                                       | 说明                                                         |
| ---------------------------------------------- | ------------------------------------------------------------ |
| SqlDataAdapter(SqlCommand cmd)                 | 带参数的构造方法，传递 SqlCommand 类的对象作为参数           |
| SqlDataAdapter(string sql, SqlConnection conn) | 带参数的构造方法，sql 参数是指定对数据表执行的 SQL 语句，conn 是数据库的连接对象 |
| SqlDataAdapter()                               | 不带参数的构造方法                                           |

| 属性或方法           | 说明                                                         |
| -------------------- | ------------------------------------------------------------ |
| SelectCommand        | 属性，设置 SqlDataAdapter 中要执行的查询语句                 |
| InsertCommand        | 属性，设置 SqlDataAdapter 中要执行的添加语句                 |
| UpdateCommand        | 属性，设置 SqlDataAdapter 中要执行的修改语句                 |
| DeleteCommand        | 属性，设置 SqlDataAdapter 中要执行的删除语句                 |
| Fill(DataSet ds)     | 方法，将 SqlDataAdapter 类中查询出的结果填充到 DataSet 对象中 |
| Fill(DataTable dt)   | 方法，将 SqlDataAdapter 类中查询出的结果填充到 DataTable 对象 中，DataTable是数据表对象，在一个DataSet对象中由多个 DataTable对象构成 |
| Update(DataSet ds)   | 方法，更新 DataSet 对象中的数据                              |
| Update(DataTable dt) | 方法，更新 DataTable 对象中的数据                            |

## 二、DataSet常用构造方法与属性

| 构造方法                    | 说明                                                 |
| --------------------------- | ---------------------------------------------------- |
| DataSet()                   | 无参构造方法                                         |
| DataSet(string DataSetName) | 带参数的构造方法，DataSetName 参数用于指定数据集名称 |

| 属性或方法      | 说明                                                         |
| --------------- | ------------------------------------------------------------ |
| Tables          | 属性，获取 DataSet 中所有数据表的集合，Tables[0] 代表集合中的第一个数据表 |
| CaseSensitive   | 属性，获取或设置 DataSet 中的字符串是否区分大小写            |
| Relations       | 属性，获取 DataSet 中包含的关系集合                          |
| Clear()         | 方法，清空 DataSet 中的数据                                  |
| Copy()          | 方法，复制 DataSet 中的数据                                  |
| AcceptChanges() | 方法，更新 DataSet 中的数据                                  |
| HasChanges()    | 方法，获取 DataSet 中是否有数据发生变化                      |
| RejectChanges() | 方法，撤销对 DataSet 中数据的更改                            |

## 三、DataTable常用构造方法与属性

| 构造方法                    | 说明                                                  |
| --------------------------- | ----------------------------------------------------- |
| DataTable()                 | 无参构造方法                                          |
| DataTable(string TableName) | 带参数的构造方法， TableName 参数用于指定数据表的名称 |

| 属性        | 说明                                |
| ----------- | ----------------------------------- |
| TableName   | 属性，获取或设置 DataTable 的名称   |
| Columns     | 属性，获取 DataTable 中列的集合     |
| Rows        | 属性，获取 DataTable 中行的集合     |
| DataSet     | 属性，获取 DataTable 所在的 DataSet |
| Constraints | 属性，获取 DataTable 中的所有约束   |



## 四、SQL server数据表转为DataTable

```c#
using (SqlCommand sqlCommand = new SqlCommand(importTableName, sqlConnection))
    //importTableName:数据库查询语句，select * from @tablename
{
    SqlDataAdapter sqlDataAdapter = new SqlDataAdapter();
    //DataSet dataSet = new DataSet();
    DataTable dataTable = new DataTable();
    sqlDataAdapter.SelectCommand = sqlCommand;
    sqlDataAdapter.Fill(dataTable); //取出选中数据表中所有数据并填入DataTable中
    //sqlDataAdapter.Fill(dataSet);
    dataImport.datatableToCSV(dataTable, NumberofData);  //数据转为CSV导出
}
```

