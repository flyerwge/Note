# 替换Replace

```c#
string tableJudge = "SELECT table_name FROM information_schema.TABLES WHERE table_name ='@Data'";

string tbJudge = tableJudge.Replace("@Data", tableTime);
```

**==注：==**用于替换字符串中某一段字符。

​	