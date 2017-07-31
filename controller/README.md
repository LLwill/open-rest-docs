# Controller

因为我们只需要开发api，所以由原来的 MVC 模型，变成了 MC 模型，V 的这一块逐步变成了各种类型的 UI，这些UI绝对多数是在客户端上执行的代码。

<pre>open-rest 中的 controller 一般不去做具体的实现，而是在组装各种 helper，这样 Controller 的方法看起来就像一个程序流程的概述</pre>

我们来看一个例子

```js
const modify = [
  // 1. 根据 req.param.id 从 User 获取 user 实例，挂载到 req.hooks.user 上
  helper.getter(User, 'user', 'param.id'),
  // 2. 判断上一步获取的用户是否存在，不存在直接抛出 404 错误
  helper.assert.exists('hooks.user'),
  // 3. 到这里说明用户是存在的，这里进行权限判断，这里是个数组，是 `或` 的关系
  //    这里设置的是只有自己或者是系统管理员可以执行该请求
  //    open-rest 会依次串行执行这两个 helper，直到有一个通过，如果全部都不通过，则输出第一个错误给用户
  [
    helper.checker.ownSelf('id', 'user'),
    helper.checker.sysAdmin(),
  ],
  // 4. 检查是否需要验证用户密码，比如一般修改email和密码的时候需要提供原密码
  helper.user.checkPass(['emial', 'password']),
  // 5. 调用 open-rest-helper-rest 里的标准 modify 方法对资源进行修改
  helper.rest.modify(User, 'user'),
];
```

> 注意上面代码我在每一行里的注释, 控制器方法是一个数组类型，数组里的每一项是一个函数，或者数组. 最多只有两级，第一级里的每一个函数是串行执行，如果某个失败了，请求就返回错误给用户，停止继续执行下去。第二级的数组里面只允许是函数，同样也是串行执行，区别在于执行错误了会继续往下执行下一个，执行正确了就不会继续执行下去了，全部都执行失败的话那么这个请求就返回错误给用户，返回的错误是第一个执行的错误内容。

一般情况下遇到api错误的事情，先根据 ./app/router.js 找到出问题 api 对应的控制器方法，之后首先看这个方法程序流程是否正确，即对各种 helper 的组装是否正确，包括组装的顺序、组装时传递的参数等等，确定这些都没有问题，那么就是helper实现的问题了，每一个helper的功能尽量保持单一，这样很容易构造 req, res, next 来进行单元测试，从而解决问题。避免后续再次出错。

> 自己开发 helper 尽量保证要有覆盖度很高的单元测试用例，因为 helper 会被大量的重复使用，所以保证每一个小功能的 helper 正确无误，且对此胸有成竹绝对会产生事半功倍的效果。

