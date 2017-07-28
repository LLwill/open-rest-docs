# plugin


> rest.plugin 是用来注册 open-rest 插件使用的

> 插件的注册有先后顺序，如果插件 A 依赖插件 B,那么要先注册 B，再注册 A

> 插件在 rest.start 函数被调用以后会执行插件初始化

> 每个注册的插件本质上是一个函数，这个函数在插件初始化的时候被调用执行

> 插件初始化执行的时候函数会得到两个参数, 第一个是 open-rest 库包，第二个是项目 app 的路径


### Example

> 看一个插件实现的例子

```js
module.exports = (rest, path) => {
  rest.helper.log = (msg) => {
    return (req, res, next) => {
      console.log('Message: %s, at: %s', msg, new Date());
      next();
    };
  };
};
```

> 这个简单的例子实现了一个 helper 用来在每次请求过来的时候输出用户指定的一个信息以及时间

> 这个实现挂在了 rest.helper 上，需要在控制器去使用它才会有效果
