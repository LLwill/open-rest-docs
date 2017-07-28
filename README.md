# open-rest 手册

> 基于 [restify](https://github.com/restify/node-restify) 快速实现的标准 restful api

[![Build status](https://api.travis-ci.org/open-node/open-rest.svg?branch=master)](https://travis-ci.org/open-node/open-rest)
[![codecov](https://codecov.io/gh/open-node/open-rest/branch/master/graph/badge.svg)](https://codecov.io/gh/open-node/open-rest)
[![NPM version](https://img.shields.io/npm/v/open-rest.svg?style=flat-square)](https://www.npmjs.com/package/open-rest)


## 环境要求
------------------------------
Node.js version 6 以上，最好直接使用 Node.js 8 这样可以放心的使用 async/await 而不用考虑 babel 转换的事情


## 快速开始
------------------------------
建议使用样本工程直接开始，这样能酱烧很多工作量

```bash
// 克隆样本功能
git clone git@github.com:open-node/open-rest-es6-boilerplate.git myApp
cd myApp

// 安装依赖库包
npm install

// 安装部署
npm run setup

```


## 编码规范
- 按照 eslint-airbnb 风格执行,
- 仅修改了少数几个规则，具体参考样本工程项目下的 .eslintrc

## 目录结构约定
------------------------------
<pre>
├── app
│   ├── configs // 存放配置信息，里面会根据 NODE_ENV 环境变量自动选择要加载的配置信息
│   ├── controllers // 控制器
│   │   └── helper // 提供控制器组装的 helper 功能模块
│   ├── data // 放一些静态的数据, 比如全国城市的数据
│   ├── lib // 公共功能模块, 比如转码的，压缩的，加密的等等和业务关系不大的，通用性的函数
│   ├── locale // 存放 i18n 语言项
│   ├── middle-wares // 公共中间件，每一个请求都会经过
│   ├── models // 数据模型
│   └── routes.js // 路由定义
├── index.js // api 启动入口
├── LICENSE
├── package.json
└── README.md
</pre>

注: 项目下新增的目录一定要在目录里放置一个 README.md 用来说明该目录的作用


## MIT license
-------------------------------

* Copyright (c) 2017 open-node
* Author Redstone Zhao
* Email: 13740080@qq.com
