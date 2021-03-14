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
```

## 三、VSCode打开项目

打开项目，终端输入

```shell
npm run serve
```

## 四、问题

从GitHub 克隆的代码运行问题：

- 进入文件夹，重新安装依赖：cnpm i
- 如果仍不能运行，更新依赖：cnpm update