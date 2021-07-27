# NUXT框架

[参考教程](https://www.w3cschool.cn/nuxtjs/nuxtjs-b4kl36fw.html)

一、使用默认启动页安装：（确保安装了npx）(下载经常出错，多试几次就好，阿里云镜像暂时不知道命令)

```shell
$ npx create-nuxt-app OnlineEducationNuxt ----><项目名>
```

二、自己构建新的Nuxt项目：

1. 在新的项目文件夹下创建package.json文件，设定如何运行nuxt

```js
{
  "name": "my-app",
  "scripts": {
    "dev": "nuxt"
  }
}
```

2. 安装nuxt

```shell
$ npm install --save nuxt
```

三、启动项目：

```shell
$ npm run dev
```

