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
