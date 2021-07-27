# 组件传值

## 父组件向子组件传值

父组件：

```vue
<template>
<div>
    父组件:
    <input type="text" v-model="name">
    <br>
    <br>
    <!-- 引入子组件 -->
    <child :inputName="name"></child>
    </div>
</template>
<script>
    import child from './child'
    export default {
        components: {
            child
        },
        data () {
            return {
                name: ''	//向子组件传入的值
            }
        }
    }
</script>
```

子组件：

```vue
<template>
<div>
    子组件:
    <span>{{inputName}}</span>
    </div>
</template>
<script>
    export default {
        // 接受父组件的值
        props: {
            inputName: String,
            required: true
        }
    }
</script>
```

## 子组件向父组件传值

子组件：

```vue
<template>
<div>
    子组件:
    <span>{{childValue}}</span>
    <!-- 定义一个子组件传值的方法 -->
    <input type="button" value="点击触发" @click="childClick">
    </div>
</template>
<script>
    export default {
        data () {
            return {
                childValue: '我是子组件的数据'
            }
        },
        methods: {
            childClick () {
                // childByValue是在父组件on监听的方法
                // 第二个参数this.childValue是需要传的值
                this.$emit('childByValue', this.childValue)
            }
        }
    }
</script>  
```

父组件：

```vue
<template>
<div>
    父组件:
    <span>{{name}}</span>
    <br>
    <br>
    <!-- 引入子组件 定义一个on的方法监听子组件的状态-->
    <child v-on:childByValue="childByValue"></child>
    </div>
</template>
<script>
    import child from './child'
    export default {
        components: {
            child
        },
        data () {
            return {
                name: ''
            }
        },
        methods: {
            childByValue: function (childValue) {
                // childValue就是子组件传过来的值
                this.name = childValue	//父组件中name就等于子组件传过来的值
            }
        }
    }
</script>
```

## 非父子组件之间的传值

（非父子组件之间传值，需要定义个公共的公共实例文件bus.js，作为中间仓库来传值，不然路由组件之间达不到传值的效果。）

公共bus.js

```js
//bus.js
import Vue from 'vue'
export default new Vue()
```

组件A：

```vue
<template>
<div>
    A组件:
    <span>{{elementValue}}</span>
    <input type="button" value="点击触发" @click="elementByValue">
    </div>
</template>
<script>
    // 引入公共的bus，来做为中间传达的工具
    import Bus from './bus.js'
    export default {
        data () {
            return {
                elementValue: 4
            }
        },
        methods: {
            elementByValue: function () {
                Bus.$emit('val', this.elementValue)  //将elementValue传递给bus on的val
            }
        }
    }
</script>
```

组件B：

```vue
<template>
<div>
    B组件:
    <input type="button" value="点击触发" @click="getData">
    <span>{{name}}</span>
    </div>
</template>
<script>
    import Bus from './bus.js'
    export default {
        data () {
            return {
                name: 0
            }
        },
        mounted（） {
            // 用$on事件来接收参数
            Bus.$on('val', (data) => {
                console.log(data)
                this.name = data  //data即为传递过来的参数
            })
        },
        methods: {
            getData: function () {
                this.name++
            }
        }
    }
</script>
```

