# 获取时间

## DateTime类：获取当前的时间

```c#
//获取日期+时间
DateTime.Now.ToString();      // 2008-9-4 20:02:10
DateTime.Now.ToLocalTime().ToString();    // 2008-9-4 20:12:12

//获取日期
DateTime.Now.ToLongDateString().ToString();  // 2008年9月4日
DateTime.Now.ToShortDateString().ToString();  // 2008-9-4
DateTime.Now.ToString("yyyy-MM-dd");    // 2008-09-04
DateTime.Now.Date.ToString();      // 2008-9-4 0:00:00

//获取时间
DateTime.Now.ToLongTimeString().ToString();  // 20:16:16
DateTime.Now.ToShortTimeString().ToString();  // 20:16
DateTime.Now.ToString("hh:mm:ss");    // 08:05:57
DateTime.Now.TimeOfDay.ToString();    // 20:33:50.7187500

//其他
DateTime.ToFileTime().ToString();    // 128650040212500000
DateTime.Now.ToFileTimeUtc().ToString();  // 128650040772968750
DateTime.Now.ToOADate().ToString();    // 39695.8461709606
DateTime.Now.ToUniversalTime().ToString();  // 2008-9-4 12:19:14

DateTime.Now.Year.ToString();     获取年份 // 2008
DateTime.Now.Month.ToString();   获取月份  // 9
DateTime.Now.DayOfWeek.ToString(); 获取星期  // Thursday
DateTime.Now.DayOfYear.ToString(); 获取第几天  // 248
DateTime.Now.Hour.ToString();     获取小时  // 20
DateTime.Now.Minute.ToString();   获取分钟  // 31
DateTime.Now.Second.ToString();   获取秒数  // 45

//n为一个数,可以数整数,也可以事小数
dt.AddYears(n).ToString();  //时间加n年
dt.AddDays(n).ToString();  //加n天
dt.AddHours(n).ToString();  //加n小时
dt.AddMonths(n).ToString();  //加n个月
dt.AddSeconds(n).ToString();  //加n秒
dt.AddMinutes(n).ToString();  //加n分
```



### **SQL语句使用时间和日期的函数**

### getdate():获取系统当前时间
```mysql
dateadd(datepart,number,date):计算在一个时间的基础上增加一个时间后的新时间值,比如：dateadd(yy,30,getdate())
datediff(datepart,startdate,enddate):计算两个时间的差值,比如：datediff(yy,getdate(),'2008-08-08')
dataname(datepart,date):获取时间不同部分的值，返回值为字符串
datepart(datepart,date):和datename相似，只是返回值为整型
day(date):获取指定时间的天数
month(date):获取指定时间的月份
year(date):获取指定时间的年份
select year(getdate()) ：当前年份
```

