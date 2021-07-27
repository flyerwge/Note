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

## 七、Vue生命周期

```javascript
//===创建时的四个事件 
beforeCreate() { 
    // 第一个被执行的钩子方法：实例被创建出来之前执行 
    console.log(this.message) //undefined 
    this.show() //TypeError: this.show is not a function 
    // beforeCreate执行时，data 和 methods 中的 数据都还没有没初始化
},
    
created() { 
    // 第二个被执行的钩子方法 
    console.log(this.message) //床前明月光 
    this.show() //执行show方法 
    // created执行时，data 和 methods 都已经被初始化好了！ /
    / 如果要调用 methods 中的方法，或者操作 data 中的数据，最早，只能在 created 中操作
},
    
beforeMount() { 
    // 第三个被执行的钩子方法 
    console.log(document.getElementById('h3').innerText) //{{ message }} 
    // beforeMount执行时，模板已经在内存中编辑完成了，尚未被渲染到页面中
},
    
mounted() { 
    // 第四个被执行的钩子方法 
    console.log(document.getElementById('h3').innerText) //床前明月光 
    // 内存中的模板已经渲染到页面，用户已经可以看见内容
},
    
//===运行中的两个事件 
beforeUpdate() { 
    // 数据更新的前一刻 
    console.log('界面显示的内容：' + document.getElementById('h3').innerText) console.log('data 中的 message 数据是：' + this.message) // beforeUpdate执行时，内存中的数据已更新，但是页面尚未被渲染
},
    
updated() { 
    console.log('界面显示的内容：' + document.getElementById('h3').innerText)
	console.log('data 中的 message 数据是：' + this.message) // updated执行时，内存中的数据已更新，并且页面已经被渲染
}
```

