# Stopwatch检测某段代码的运行时间

```c#
  System.Diagnostics.Stopwatch stopwatch = new System.Diagnostics.Stopwatch();
  stopwatch.Start(); //  开始监视代码运行时间
  /*
  要检测时间的代码段
  */
  stopwatch.Stop(); //  停止监视
  TimeSpan timespan = stopwatch.Elapsed; //  获取当前实例测量得出的总时间
  double hours = timespan.TotalHours; // 总小时
  double minutes = timespan.TotalMinutes;  // 总分钟
  double seconds = timespan.TotalSeconds;  //  总秒数
  double milliseconds = timespan.TotalMilliseconds;  //  总毫秒数
  log.InfoFormat("递归用时：{0}", milliseconds);
```

