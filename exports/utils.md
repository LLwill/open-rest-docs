# utils 公共库函数

> 这里提供一些公共的，通用的函数, 或者变量, 应用自身的 ./app/lib/utils.js 建议也在这个上扩展，这样在使用的时候就不用刻意区分函数是哪里实现的，但是要注意函数名别冲突，冲突可能会导致open-rest的功能不正常

### callback(promise, callback)
> 该函数的目的是把一个 promise 和 callback 回调函数给结合起来

__Arguments__
* `promise` - 异步执行的 promise 实例
* `callback` - 一个回调函数

### intval(value, mode)
> 将一个变量整型化

__Arguments__
* `value` - 要处理的变量
* `mode` - 可选参数，进制, 默认是 10, 即 10 进制

### getModules(path, exts, excludes)
> 根据设置的路径，加载并获取对象

__Arguments__
* `path` - 要加载的路径
* `exts` - 可选，Array|String 类型, 匹配的后缀, 例如 `js` 代表要加载 .js 后缀的模块
* `excludes` - 可选，Array|String 类型，要排除的模块，例如: `index` 代表排除 index.js, index.coffee, index.json 等模块

### remoteIp(req)
> 真实的连接请求端ip，这个ip是建立连接的ip，是不可伪造的

> 但是这个ip往往不是用户的ip

> 比如我们的 API 并未直接让用户访问，会通过本机的 nginx 代理一下，那么这个 ip 是 127.0.0.1

__Arguments__
* `req` - 请求的 request 对象

### clientIp(req)
> 获取客户端真实ip地址, 这个ip最有可能是用户真实的上网ip

> 但是这个ip也是最不可信任的，因为很容易伪造

> 一般请求经过反向代理之类的加速服务用户的ip会放在头信息的 x-forwarded-for/x-real-ip  传递

> 而头信息是可以随意构造的

__Arguments__
* `req` - 请求的 request 对象


### realIp(req, proxyIps)
> 获取可信任的真实ip

> 这个函数先会判断remoteIp 是否是本地nginx代理的ip，如果是的话就获取头信息的 x-real-ip

> 所以如果是这种部署方式的话，要记得nginx代理的时候要传递 x-real-ip 过来, 值是与nginx建立连接的ip

> nginx 里配置如下
<pre>
    proxy_set_header            X-Real-IP $remote_addr;
</pre>

__Arguments__
* `req` - 请求的 request 对象
* `proxyIps` - Array 允许代理的ip地址

> 注: 判断是否是私有客户端就是通过这个 realIp 来判断的，所以这里 proxyIps 一定要谨慎配置

### file2Module(file)
> 文件名称到moduleName的转换, 例如 team-user => teamUser

> 我们的约定是文件名多个单词之间是减号（-）,代码中的变量等是驼峰式

__Arguments__
* `file` - String 文件名称

### ucwords(value)
> 首字符大写, 例如 user => User

__Arguments__
* `value` - String 要转换的字符串

### nt2space(value)
> 将字符串里的换行，制表符替换为普通空格

> 一般用来处理单行文本，比如用户名，email，收货地址等这些用 input 表单收集的字段

> 同时会被左右两侧空白 trim 掉

> 例如: 'Restone\tZhao' => 'Restone Zhao'

__Arguments__
* `value` - String 要处理的字符串

### getToken(req)
> 获取accessToken

> 优先级依次为

* req.headers['x-auth-token']
* req.params.access_token
* req.params.accessToken

__Arguments__
* `req` - 请求的 request 对象

### randStr(len, type)
> 生成随机字符串

__Arguments__
* `len` - Number 生成的随机串的长度
* `type` - String 随机串的强度，可选 `noraml`, `strong`, 默认是 `normal`

> 如果 type 既不是 `noraml` 也不是 `strong` 那么会用 type 直接作为生成随机串的字典

### logger 对象

#### info(...args)
> 调用 console.info 输出信息

#### error(...args)
> 调用 console.error 输出信息

#### warn(...args)
> 调用 console.warn 输出信息


### isTest 常量
> 用来判断当前是否是测试环境 process.env.NODE_ENV 判断是否是 test

### isProd 常量
> 用来判断当前是否是生产环境 process.env.NODE_ENV 判断是否是 production
