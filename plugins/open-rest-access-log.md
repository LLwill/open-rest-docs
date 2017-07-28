# open-rest-access-log

这是一个 open-rest 的中间件插件用来记录访问的日志，带有自动按天切分日志的功能，可以自定义log 格式

[![Build status](https://api.travis-ci.org/open-node/open-rest-access-log.svg?branch=master)](https://travis-ci.org/open-node/open-rest-access-log)
[![codecov](https://codecov.io/gh/open-node/open-rest-access-log/branch/master/graph/badge.svg)](https://codecov.io/gh/open-node/open-rest-access-log)
[![NPM version](https://img.shields.io/npm/v/open-rest-access-log.svg?style=flat-square)](https://www.npmjs.com/package/open-rest-access-log)

## Node version
<pre> >= 6 </pre>

# Usage

<pre>Write access log for http-server</pre>

<pre>npm install open-rest-access-log --save</pre>

<pre>
const logger = require('open-rest-access-log');
// /var/log/app/access-20160630.log
// /var/log/app/access-20160701.log
// /var/log/app/access-20160702.log

// 返回的这个函数形似 (req, res, next) => { /**/ } 放在 ./app/middle-wares/index.js 里即可
logger('/var/log/app/access', 'YYYY-MM-DD HH:mm:ss', logFormat)
</pre>
