# 点击事件button

先定义button按钮并绑定事件：

```c#
public void test()
{
    Button btn = new Button();
    btn.Click += Btn_Click;
}

private void Btn_Click(object sender, RoutedEventArgs e)
{
     Console.WriteLine("点击了按钮！");
}
```

