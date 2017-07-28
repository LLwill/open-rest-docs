# helper

> helper 是一类供控制器来组装和调用的组间。

> helper 在实现的时候尽量要功能单一，这样才能被更多的控制器使用，最大限度实现代码重用

> helper 在执行的时候一般返回类似于这样的小函数 (req, res, next) => { /**/ }


### open-rest 自带 helper

#### rest.helper.console

> 用来在控制器中使用

> rest.helper.console 包含 log, error, info, warn, time, timeEnd

> 行为类似于系统自带的 console 对应的方法，只不过他是在请求过来以后触发的

```js

// 这里返回的是 (req, res, next) => { console.log(...args); } 这样的函数
rest.helper.console.log('hello', 'world');

```

#### helper 类型的插件也应该挂在 rest.helper 上面, 方便控制器去组装使用

> 举个例子

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
