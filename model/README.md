# Model

Model 是数据模型层，在 open-rest 的约定中负责数据层的存储读取，以及业务领域代码的功能性封装，open-rest 提倡 Model 层要做成充血模型，controller/helper 尽量不要过多封装业务，而仅仅是对 Model 层各种封装的调用。这么做的好处是 因为 Model 层的代码方便在各种环境和模式下调用，比如命令行下，socket请求等，而 controller/helper 的代码仅适合在 http 请求中被调用。Model 层的具体约定取决于您选择的 open-rest 插件。


### Model 层对于业务领域功能的封装一般有类方法是实例方法两类，原则如下

1. 实例方法: 功能和特定的某个实例有直接关系, 比如禁用某个用户 user.disable(); 就应该是一个实例方法
2. 类方法: 功能和特定的某个实例没有关系，比如获取全部已禁用的用户 User.getDisabled(); 就应该是一个类方法
