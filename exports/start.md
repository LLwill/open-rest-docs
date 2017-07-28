# start

启动 open-rest api服务的函数

### rest.start(path, callback);
> 启动 web service, path 为 app 的代码绝对路径

> callback service启动完成后的回到函数
* Arguments
  * error 是否启动时发生错误
  * server 启动后的 server 实例

__Arguments__
* path - String 应用app代码路径，按照约定是项目根目录下的 ./app, 即 `${__dirname}/app`
* 启动后的回调函数
