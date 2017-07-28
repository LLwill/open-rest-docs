# errors 错误处理模块

> 这里封装了一些基础的常用的错误，应用如果需要自己封装更多的错误处理函数，建议在这个基础上扩展, 这样使用的时候就不需要刻意区分是open-rest实现的还是应用自己实现的


### notFound(msg, field)
> 当 field 不存在时, 返回资源未找到错误 404, msg 是错误信息

> 当 field 存在时，会返回 422 字段错误

__Arguments__
* msg - String 可选，默认是 `Resource not found.`
* field - String 可选，错误发生的字段名

### notAllowed(msg)
> 没有权限操作错误，403

__Arguments__
* msg - String 可选，默认是 `Not allowed error.`

### notAuth(msg)
> 未授权错误，403

__Arguments__
* msg - String 可选，默认是 `Not authorized error.`

### invalidArgument(msg, values)
> 请求的参数错误，409

__Arguments__
* msg - String 可选，默认是 `Invalid argument error.`
* values - Array|String 可选，错误的参数的值

### missingParameter(msg, missings)
> 缺失必要参数的错误, 409

__Arguments__
* msg - String 可选，默认是 `Invalid argument error.`
* missings - Array|String 可选，缺失的参数

### sequelizeIfError(error, field)
> 判断是否是一个错误，如果不是则返回 null, 如果是则返回一个参数错误

__Arguments__
* error - mixed 要判断的错误
* field - String 可选, 发生错误的字段名称

### ifError(error, field)
* sequelizeIfError 的别名

### normalError(msg, ...values)
> 普通错误, 500

__Arguments__
* msg - String 可选，默认是 'Normal error.'
* values - Array 可选，错误的值

### error(msg, ...values)
> 未知错误, 500

__Arguments__
* msg - String 可选，默认是 'Unknown error.'
* values - Array 可选，错误的值
