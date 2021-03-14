# 插入Insert

```c#
string result = System.Text.RegularExpressions.Regex.Replace(tim, @"[^0-9]+", "");  //找出输入字符的所有数字
result = result.Insert(4, "_").Insert(7, "_");  //将输入数字变为对应时间格式
```

