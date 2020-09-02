# 踩坑问题解决

## feign依赖下载不下来

在`xc-framework-common`模块中将`feign`改为`openfeign`

```xml
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-openfeign</artifactId>
</dependency>
```

## webpack打包测试add方法报错

?> 声明：我用的webpack版本是`4.43.0`，4以下版本我没用过，不知道会不会是打包方式不同的原因

课件中的`main.js`原代码：

```js
var add = require('./module01.js');
var Vue = require('./vue.min');
var VM = new Vue({
    el:"#app",//表示当前vue对象接管app的div区域
    data:{
        num1:0,
        num2:0,
        result:0,
    },
    methods:{
        add:function(){
            //这里使用了导入的module01.js文件中的add方法
            this.result = add(Number.parseInt(this.num1),Number.parseInt(this.num2))
            alert(this.result)
        }
    }
});
```

!> 重点在第一行和调用module01模块add方法的地方

第一行这里引入module01模块，这里的的add应该是module01中导出的`exports`对象，所以这里的add应该是这样的

```json
{
    add:f(x,y)
}
```

所以直接调用add肯定会报不是function的错误！，修改后的代码：

```js
const Vue = require('./vue.min.js');
const module01 = require('./module01.js');

const VM = new Vue({
    el: '#app',
    data: {
        num1: 0,
        num2: 0,
        result: 0
    },
    methods: {
        add: function function_name() {
            this.result = module01.add(Number.parseInt(this.num1), Number.parseInt(this.num2));
            alert(this.result)
        }
    }
})
```

当然你也可以将add解构出来

```js
const Vue = require('./vue.min.js');
const {add} = require('./module01.js');

const VM = new Vue({
    el: '#app',
    data: {
        num1: 0,
        num2: 0,
        result: 0
    },
    methods: {
        add: function function_name() {
            this.result = add(Number.parseInt(this.num1), Number.parseInt(this.num2));
            alert(this.result)
        }
    }
})
```



## CMS前端项目运行不起来

> 有两种解决方案

1. 修改电脑安装的nodejs版本为 `v9`及以下版本

2. 删除项目本地的npm模块，重新安装`node-sass`

   ```shell
   #卸载npm、cnpm、node-sass
   npm uninstall npm cnpm node-sass
   
   #重新安装node-sass
   npm install node-sass --save
   ```




## 日期选择框太丑

> cmspage添加页面的日期选择框由于充满屏幕，显得非常丑

重新安装`element-ui`模块

```shell
cnpm install element-ui@2.0.10
```

不知道为什么同样的版本号却和项目中安装好的样式表不一样