# Router
-----------------------

指向 [open-router](https://github.com/open-node/open-router) 库包

open-router 是 open-rest 使用的一个依赖，他的作用是给 restify 提供一个高效、简介的路由功能

应用开发人员一般不用直接使用他，只需要在约定的 ./app/routers.js 里使用 Router 的实例即可

Router 的初始化是 open-rest 完成的

[![Build status](https://api.travis-ci.org/open-node/open-router.svg?branch=master)](https://travis-ci.org/open-node/open-router)
[![codecov](https://codecov.io/gh/open-node/open-router/branch/master/graph/badge.svg)](https://codecov.io/gh/open-node/open-router)
[![NPM version](https://img.shields.io/npm/v/open-router.svg?style=flat-square)](https://www.npmjs.com/package/open-router)


# Router 实例的用法，即 ./app/routers.js 的定义
-----------------------
./app/routers.js 按照我们对目录的约定，这里会定义所有的路由规则以及对应的控制器方法，
换言之他是把 verb path 和 controller method 链接起来的桥梁

./app/routers.js 需要通过 module.exports 释放一个函数，这个函数会有一个参数，这个参数就是 open-router 的实例


# Example
----------------------
```js
module.exports = (r) => {
  /** 首页默认路由 */
  r.get('/', 'home#index');

  /** 用户登陆接口 */
  r.post('/session', 'user#login');

  /** 用户退出接口 */
  r.del('/session', 'user#logout');

  /** 用户查看自身信息接口 */
  r.get('/session', 'user#session');

  /** 用户接口 */
  r.resource('user');
  /** 用户client授权接口 */
  r.collection('client', null, 'user');
  r.model('client');
  r.get('/clients', 'client#list');
}
```

这个函数的执行是 open-rest 来控制的，你可以不用关注他的执行。这里的参数 `r` 就是 open-router 的实例


# Methods
----------------------------

### router.get(routePath, actionPath)

用于获取资源详情或者列表, 成功状态码  200

HTTP.verb `GET`

__Arguments__
* `routePath` - 路由路径 ，例如 `/users/:id` or `/users/:userId/books`
* `actionPath` - 控制器方法路径. 例如: `user#detail` 会对应 ./app/controllers/user.js 释放的 detail 方法组

__Example__
```js
router.get('/users', 'user#list'); // 当通过 GET 方法请求 `/users`, ./app/controllers/user.js 的 list 对应的方法组被调用
router.get('/users/:id', 'user#detail'); // 当通过 GET 方法请求 `/users/:id`, ./app/controllers/user.js 的 detail 对应的方法组被调用

```

### router.put(routePath, actionPath)

HTTP.verb `PUT`

用于修改某个资源描述, 成功状态码 200

__Arguments__
* `routePath` - 路由路径 ，例如 `/users/:id` or `/users/:userId/books`
* `actionPath` - 控制器方法路径. 例如: `user#modify` 会对应 ./app/controllers/user.js 释放的 modify 方法组

__Example__
```js
router.put('/users/:id', 'user#modify'); // 当通过 PUT 方法请求 `/users/:id`, ./app/controllers/user.js 的 modify 对应的方法组被调用
```

### router.patch(routePath, actionPath) 同上 put


### router.post(routePath, actionPath)

HTTP.verb `POST`

一般用于资源的创建, 成功状态码 201

__Arguments__
* `routePath` - 路由路径 ，例如 `/users/:id` or `/users/:userId/books`
* `actionPath` - 控制器方法路径. 例如: `user#add` 会对应 ./app/controllers/user.js 释放的 add 方法组

__Example__
```js
router.post('/users', 'user#add'); // 当通过 POST 方法请求 `/users`, ./app/controllers/user.js 的 add 对应的方法组被调用
```

### router.del(routePath, actionPath)
一般用于删除某个资源，成功状态码 204

HTTP.verb `DELETE`

__Arguments__
* `routePath` - 路由路径 ，例如 `/users/:id` or `/users/:userId/books`
* `actionPath` - 控制器方法路径. 例如: `user#remove` 会对应 ./app/controllers/user.js 释放的 remove 方法组

__Example__
```js
router.del('/users', 'user#add'); // 当通过 DELETE 方法请求 `/users`, ./app/controllers/user.js 的 remove 对应的方法组被调用
```


### router.resource(name, [routePath])

HTTP.verb `DELETE` or `GET` or `PATCH` or `PUT`

一般用于全局资源，比如系统用户，会自动添加资源的增、删、改、查(列表和详情) 全部的接口

__Arguments__

* `name` - 必选参数，资源名称 例如 `user`, `book`, `order` 等
* `routePath` - 可选参数，默认是第一个参数计算得来 例如 `name` = user, 那么 `routePath` 为 /users，也可以自己指定


__Example__

```js
router.resource('user')

// 等价于
// router.get('/users', 'user#list');
// router.get('/users/:id', 'user#detail');
// router.put('/users/:id', 'user#modify');
// router.patch('/users/:id', 'user#modify');
// router.delete('/users/:id', 'user#remove');
// router.post('/users', 'user#add');


router.resource('weiboUser', '/weibo/users');
// 等价于一下六个
// 注意这里对应的控制器模块路径是 ./app/controllers/weibo-user.js
// 注意这里文件名，使用了中划线连接不同的单词, open-rest 在加载控制器的时候会自动处理
// router.get('/weibo/users', 'weiboUser#list');
// router.get('/weibo/users/:id', 'weiboUser#detail');
// router.put('/weibo/users/:id', 'weiboUser#modify');
// router.patch('/weibo/users/:id', 'weiboUser#modify');
// router.delete('/weibo/users/:id', 'weiboUser#remove');
// router.post('/weibo/users', 'weiboUser#add');
```

### router.model(name, routePath)

HTTP.verb `DELETE` or `GET` or `PATCH` or `PUT`

一般用于对用于相同路由路径的单个资源的 `查`, `删`, `改` 操作

__Arguments__

* `name` - 必选参数，资源名称 例如 `user`, `book`, `order` 等
* `routePath` - 可选参数，默认是第一个参数计算得来 例如 `name` = user, 那么 `routePath` 为 /users/:id，也可以自己指定

__Example__

```js
router.model('user')

// 等价于
// router.get('/users/:id', 'user#detail');
// router.put('/users/:id', 'user#modify');
// router.patch('/users/:id', 'user#modify');
// router.delete('/users/:id', 'user#remove');

router.model('user', '/systems/users')

// 等价于
// router.get('/systems/users/:id', 'user#detail');
// router.put('/systems/users/:id', 'user#modify');
// router.patch('/systems/users/:id', 'user#modify');
// router.delete('/systems/users/:id', 'user#remove');
```

### router.collection(name, routePath)

HTTP.verb `POST` or `GET`

一般用于对用于相同路由路径的资源集合的 `查`, `增` 操作

__Arguments__

* `name` - Response's name. eg: `user`, `book`, `order`
* `routePath` - optional, uri
* `parent` - optional, The resource's parent resource name

* `name` - 必选参数，资源名称 例如 `user`, `book`, `order` 等
* `routePath` - 可选参数，默认是第一个和第三个参数计算得来, 具体参考我下面的实例代码
* `parent` - 可选参数, 资源的父级所属资源名称, 例如 `user`, `team` 等

__Example__

```js
router.collection('book', null, 'user')

// 等价于
// router.get('/users/:userId/books', 'user#books');
// router.post('/users/:userId/books', 'user#addBook');


router.collection('book', '/users/:creatorId/books', 'user')

// 等价于
// router.get('/users/:creatorId/books', 'user#books');
// router.post('/users/:creatorId/books', 'user#addBook');
```
