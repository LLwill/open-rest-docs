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

# Example
----------------------
```js

```

