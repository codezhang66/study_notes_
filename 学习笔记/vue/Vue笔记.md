## Vue笔记

### 1、第一个vue程序

**vue程序必不可少的开头！**

```java
xmlns:v-bind="http://www.w3.org/1999/xhtml"
```

**引入vue**

```java
<!--导入vue.js-->
<script src="https://cdn.jsdelivr.net/npm/vue@2.5.21/dist/vue.min.js"></script>
```



#### 1.1、**test1**:  鼠标悬浮在span标签上会出现绑定文字`v-bind:title`所绑定的提示信息。

```java
<!DOCTYPE html>
<html lang="en" xmlns:v-bind="http://www.w3.org/1999/xhtml">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<div id="app">
    <span v-bind:title="message">
        鼠标悬停几秒钟可以查看动态绑定的提示信息！
    </span>
</div>

<!--导入vue.js-->
<script src="https://cdn.jsdelivr.net/npm/vue@2.5.21/dist/vue.min.js"></script>

<script>
    var vm = new Vue({
        el: "#app",
        data: {
            message: "hello,Vue!"
        }
    });
</script>

</body>
</html>
```



#### 1.2、**test2**: 练习判断`v-if 和v-else-if`

```java
<div id="app">
    <h1 v-if="ok==='A'">A</h1>
    <h1 v-else-if="ok==='B'">b</h1>
    <h1 v-else>c</h1>
</div>
        
<script>
    var vm = new Vue({
        el: "#app",
        data: {
            ok: 'B'
        }
    });
</script>
```



#### 1.3、**test3**: 练习循环遍历`v-for`

```java
<!--view 层  模板-->
<div id="app">
    <li v-for="(item,index) in items">
        {{item.message}}----{{index}}
    </li>
</div>

<script>
    var vm = new Vue({
        el: "#app",
        /*注意[]：表示数组  {}：表示对象*/
        data: {
            items: [
                {message: '小张...'},
                {message: '小于...'}
            ]
        }

    });
</script>
```



#### 1.4、**test4**: 练习单击事件`v-on:click` 点击之后弹出来窗口显示message内容。

```java
<!--view 层  模板-->
<div id="app">
    <button v-on:click="sayHi">点击我！</button>
</div>
        
<script>
    var vm = new Vue({
        el: "#app",
        data: {
            message: '小张，你好呀！'
        },
        methods: {//方法必须定义在methods的对象中
            sayHi: function () {
                alert(this.message)                
            }
        }
    });
</script>
```

#### 1.5、**test5**： 练习`component`组件

这里组件需要用`props`来接受view层传来的参数`zhang`。其实组件就相当于标签，可以自定义标签。

```java
<!--view 层  模板-->
<div id="app">
    <!--绑定的参数用来接收遍历的参数-->
    <xiaozhang v-for="item in items" v-bind:zhang="item"></xiaozhang>
</div>
        
<script>
    /*定义一个Vue 组件component*/
    Vue.component("xiaozhang",{
        props: ['zhang'],
        template: '<li>{{zhang}}</li>'
    });

    var vm = new Vue({
        el: "#app",
        data: {
            items: ["三国演义","水浒传","西游记"]
        }
    });
</script>
```

- Vue.component():注册组件
- my-component-li: 自定义组件的名字
- template:组件的模板

### 2、`Axios`异步通信

#### **特性：**

- 从浏览器中创建 [XMLHttpRequests](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest)
- 从 node.js 创建 [http](http://nodejs.org/api/http.html) 请求
- 支持 [Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) API
- 拦截请求和响应
- 转换请求数据和响应数据
- 取消请求
- 自动转换 JSON 数据
- 客户端支持防御 [XSRF](http://en.wikipedia.org/wiki/Cross-site_request_forgery)

**中文文档：**`http://www.axios-js.com/zh-cn/docs/`

**JavaScript必须是ECMAScript6版本**

**在线cdn:**`<script src="https://unpkg.com/axios/dist/axios.min.js"></script>`

```java
<!DOCTYPE html>
<html lang="en" xmlns:v-bind="http://www.w3.org/1999/xhtml">
<head>
    <meta charset="UTF-8">
    <title>axios</title>

    <!--v-clock:解决闪烁问题-->
    <style>
        [v-clock]{
            display: none;
        }
    </style>
</head>
<body>

<div id="vue" v-clock>
    <div>{{info.name}}</div>
    <div>{{info.url}}</div>

    <a v-bind:href="info.url">点我</a>
</div>

<!--导入vue.js-->
<script src="https://cdn.jsdelivr.net/npm/vue@2.5.21/dist/vue.min.js"></script>
<script src="https://unpkg.com/axios/dist/axios.min.js"></script>
<script>
    var  vm = new Vue({
        el: '#vue',
        data:{
            info: null
        },
        mounted(){//钩子函数  链式编程 es6的新特性
            axios.get('../data.json').then(response => {
                this.info = response.data;
            });
        }
    });
</script>

</body>
</html>
```

​			下图展示了实例的生命周期。

![Vue 实例生命周期](https://cn.vuejs.org/images/lifecycle.png)

### 3、计算属性(vue特色，类似于缓存)

​	计算出来的结果保存在属性中~,（内存中运行：虚拟Dom）

```java
<!DOCTYPE html>
<html lang="en" xmlns:v-bind="http://www.w3.org/1999/xhtml">
<head>
    <meta charset="UTF-8">
    <title>计算属性</title>

</head>
<body>
<div id="app">
    <p>currentTime1:{{currentTime1()}}</p>
    <p>currentTime2:{{currentTime2}}</p>
</div>


<!--导入vue.js-->
<script src="https://cdn.jsdelivr.net/npm/vue@2.5.21/dist/vue.min.js"></script>

<script>
    var vm = new Vue({
        el: "#app",
        data: {
            message: "小张，你好.."
        },
        methods: {
            currentTime1: function () {
                return Date.now();      //返回当前时间戳
            }
        },
        computed: {     //计算属性： methods，computed 方法不能重名，重名之后会优先使用methods的
            currentTime2: function () {
                return Date.now();      //返回当前时间戳
            }
        }
    });
</script>

</body>
</html>
```

