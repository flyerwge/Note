# Vue学习

## 一、安装

1. 安装node(官网下载)；验证：node -v;npm -v

2. 安装cnpm淘宝镜像：npm install -g cnpm -- registry=https://registry.npm.taobao.org ；验证：cnpm -v

3. vue环境：cnpm i -g vue @vue/cli ;验证：vue -V

   重新安装依赖：cnpm i;

## 二、创建项目

```shell
cmd进入项目文件夹
vue create name   //name为项目名称

//或者可视化创建
vue ui
```

## 三、VSCode打开项目

打开项目，终端输入

```shell
npm run serve
```

## 四、问题

从GitHub 克隆的代码运行问题：

- 进入文件夹，重新安装依赖：`cnpm i`
- 如果仍不能运行，更新依赖：`cnpm update`

## 五、路由跳转

1、通过router-link配合router-view进行声明式导航

2、编程式导航，通过：this.$router.push(地址);可以通过代码实现切换

==路由传参==

在地址的后面写上？分隔

通过`key = value1&key = value2`的方式添加参数

组件中通过`this.$route.query`访问对应的key即可获取数据

## 六、接口使用

### 1、轮播图

安装并导入`axios`

- ​	进入项目根目录，`npm install axios`

在`created`生命周期函数中调用轮播图接口

获取到数据并渲染到页面上