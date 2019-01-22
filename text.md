我们可以看到AngularJS是一个典型的 MVC 架构 （Model - View - Controller ），可以构建响应式网页，双向绑定的web应用，而2以后的版本开始了基于组件的架构。 
相比 AngularJS， Angular的体积更小，速度更快。迫于移动端开发的需要，为了更好地支持用于pc和移动端的web开发。采用了ts的语法，全新的命令行构建工具angular/cli。

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

Angular 的http.get返回一个 RxJS 的Observable对象。 Observable是一个管理异步数据流的强力方式。
从6版本开始新的httpclients 

大家好，今天和大家简单讲下ng7的入门和快速上手。首先我们先来看下ng7和现在我们用的ng1的版本有哪些不同以及架构的区别。
AngularJS 是一个典型的 MVC 架构 
M - Model  数据：数据实体,用来保存页面要展示的数据.
V - View      视图：负责显示数据的,一般其实就是指的html页面.
C - Controller 控制器： 控制整个业务逻辑,负责处理数据,比如数据的获取,以及数据的过滤，进而影响数据在视图上的展示.

AngularJS是早期比较完善的前端框架 包含了模板，数据双向绑定，路由，模块化，服务，过滤器，依赖注入等功能，虽然在开发响应式页面双向绑定的web应用上比较成熟，但同时也有它的缺点。
- 它采用的脏数据检查的方式，会跟踪数据的改变，动态改变用户页面的数据。随着绑定数量的增加，检查的效率就不断降低，页面加载速度也会变慢。
- 落后于当前web发展理念(如组件式的开发)
- 对手机端的支持不是太友好

- 两者的对比分析
  - Angular不是从AngularJS升级过来的，Angular是用Typescript重写的，所以从设定之初就是不一样的；
  - AngularJS诞生在09年，在设计之初主要是针对pc端的，对移动端支持较少，而Angular是设计包含移动端的；
  - AngularJS的核心概念是$scope，但是Angular中没有$scope；
  - AngularJS中的controller也在Angular中不再使用，被Component组件所替代。

* 相比AngularJS，移除了 controller +$scope 作用域的设计，改用组件式开发，使得其更容易被理解和上手性能更好（渲染更快，变化检测效率更高）优先为移动应用设计（Angular Mobile Toolkit ）更加贴合未来的标准（如es6/7、WebComponent）

而Angular则是基于组件的
M - Model 数据：它是与应用程序的业务逻辑相关的数据的封装载体
V - View 视图：它专注于界面的显示和渲染
VM - ViewModel 视图-数据：它是View和Model的粘合体，负责View和Model的交互和协作
MVC的界面和逻辑关联紧密，数据直接从数据库读取。MVVM的界面与viewmodel是松耦合，界面数据从viewmodel中获取。所以angular更倾向于mvvm

angular的浏览器支持情况，我们可以看到不像angularjs支持ie8，新版本的angular放弃了它

ts是js的超集，在js的基础上加入了一系列的新特性，

强类型的语言添加了基于类的面向对象编程。扩展了语法，
在angular的开发过程中比较常用的用法为类 接口 继承（泛型） 类型的注解 编译时的类型检查。不同于es6的class语法糖，typescript支持es6规范的类写法和es6的类的写法很像，同时ts是支持用static关键字来声明静态属性的,
和用private等关键字来实现类属性的私有化。等一些java语言的特性
使用ts好处在于在编译时就能检查出很多语法问题，使得代码变得便于维护、优雅。更加适合大型项目的管理开发。

在angular中简单使用ts，我们看到一个angular的组件首先用component装饰器声明类的类型 类型的注解
还有枚举类型等不常用的语法 这里就不一一展开叙述了
还有Enum,Void(和any相反),Null,Undefined,Never,Object

接下来是开发环境的介绍，angularjs的使用通常是页面里直接引入angularjs。
而angular有自己一套的命令行工具cli进行项目脚手架的构建，单元测试，打包。
安装好node环境 npm 全局安装cli模块 这样全局下就可以使用ng指令 ng new项目名 接着可以回车一路操作选择是否加入路由模块以及哪种css预处理器
通常这里会遇到各种问题 这里会自动安装node_modules 可以手动取消进入新建的项目中进行安装 node-sass模块安装不上可以设置成淘宝的经想哭或者全局安装cnpm然后进行安装

构建出来的项目结构如下。接着启动项目 ng server --open --port来指定端口
标签是默认带有app-前缀的

接下来是语法介绍，用过angularjs的很熟悉插值表达式，通过差值表达式我们可以将声明的数据显示在模板html上

- 1. 类型检测 2.private修饰 不能在实例中和子类中访问； protected能在子类中访问。

- 当声明一个void类型变量时，只能赋值为undefined 和 null
let unusable: void = undefined;

//声明数值类型的变量age，但不予赋值
var age:number
console.log(age) // undefined
- x1: undefined = undefined
- x2: null = null

- 类型断言(类似类型的强制转换)
- 其一是“尖括号”语法：

let someValue: any = "this is a string";

let strLength: number = (<string>someValue).length;
另一个为as语法：

let someValue: any = "this is a string";

let strLength: number = (someValue as string).length;
动态编译和运行的

// enum(枚举类型)
enum REN{ nan , nv ,zhongxing}
console.log(REN.zhongxing)  //返回了2，这是索引index，跟数组很像。

enum REN{nan='男人',nv='女人',zhongxing='人妖'}
console.log(REN.zhongxing)  // 人妖

Undefined :
Number:数值类型;
string : 字符串类型;
Boolean: 布尔类型；
enum：枚举类型；
any : 任意类型，一个牛X的类型；
void：空类型；
Array : 数组类型;
Tuple : 元祖类型；
Null ：空类型。

<!--过滤器-->
<p>{{title | uppercase}}</p>
<p>{{currentTime | date: "yyyy-MM-dd HH:mm:ss" }}</p>

- 运行时按需加载
- 延迟加载 通过将代码拆分成多个包并以按需加载的方式，来加速应用程序初始加载过程。
主模块 module 将业务拆分成不同的子模块 ngmodule