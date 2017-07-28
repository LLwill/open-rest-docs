# 对外变量

> open-rest 会在将自身使用一些重要库包以及一些重要的变量，附着在自身之上。

> 这样外部在使用的时候就可以直接获取到, open-rest 的某些插件也会通过这样的方式来供外部使用。

> 最常见的就是 helper 类型的插件，通过附着在 helper 上，外部可以轻易的使用这些。

### 基本属性如下
```js
const rest = require('open-rest');

// rest.Router open-router 库包
// rest.helper 基础的一些控制器 helper
// rest.utils open-rest 提供的库函数
// rest.errors open-rest 封装的错误对象
// rest.restify restify 库包
// rest.plugin open-rest 插件注册函数
// rest.start 用于启动 api 服务的函数
```

> 除了这些基础的变量之外，插件也会有其他的变量注册到 rest 上，要参考具体的插件的文档
