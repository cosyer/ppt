我们可以看到AngularJS是一个典型的 MVC 架构 （Model - View - Controller ），可以构建响应式网页，双向绑定的web应用，而2以后的版本开始了基于组件的架构。 相比 AngularJS， Angular的体积更小，速度更快。迫于移动端开发的需要，为了更好地支持用于pc和移动端的web开发。采用了ts的语法，全新的命令行构建工具angular/cli。

2.0以后的版本和1完全不同基于js，基于ts。

angularJS的缺点：
双向数据绑定，在项目越大的时候，性能影响很大。

AngularJs采用脏数据检查的方式，跟踪数据的改变，动态改变用户页面的数据。

随着绑定数量的增加，性能就会越来越低。

- 类型
  - 类
  - 注解
  - 泛型
  - 接口

在angular中ts常用的基础用法是声明变量的数据类型
[slide]
- 语法讲解
  - 插值表达式{{}}
    - 单向绑定
    - 双向绑定
  - controller
  - directives(component)
  - service
  - filter
  - module注册入口
  - 父子组件通信
    - Input
    - Output
    - 标签变量引用
  - 内容投影
  - 路由导航
    - 路由传参
  - 生命周期
  - http服务

 ctrl被砍掉了，整个都放在了component之中，新版本在利用注解的时候就已经指明了模块暴露的class是什么类型的angular类了