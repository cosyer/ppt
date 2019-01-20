title: angular7 讲解
transition: rollIn

[slide]
# angular7 讲解
## CKP3-陈宇

[slide]
# 讲解纲要
- 与AngularJS的架构区别
- TypeScript简介
- Angular开发环境
- Angular语法特性

[slide]
AngularJS 是一个典型的 MVC 架构 （Model - View - Controller)

![AngularJS](/images/framework2.png)
[slide]
而 Angular 则是基于组件(Component)的架构
![Angular](/images/framework1.jpeg)
[slide]
- 浏览器支持情况：

  ![浏览器支持情况](/images/brower-support.jpeg)

不像angular1支持IE8，新版本的angular放弃了它

[slide]
- TypeScript简介

  ![typescript](/images/typescript.png)

  简单说来es6是typescript的超集，在支持ES6的基础之上加入了一些新的特性。

[slide]
- 在angular中使用ts
  ```Typescript
    @Component({
      selector: 'app-user-item',
      templateUrl: './user-item.component.html',
      styleUrls: ['./user-item.component.css']
    })
    export class UserItemComponent {
      // 声明变量数据类型
      // 基本类型
      name: string = 'zhang san';
      age: number = 666;
      isMale: boolean = true;
      // 不做限制
      something: any = 'as string';
      something = 1;
      // 引用类型
      names: Array<string> = ['react', 'vue', 'angular', 'flutter', 'pwa']; // 在声明数据类型的同时可以声明内容的数据类型
      names: string[] = ['react', 'vue', 'angular', 'flutter', 'pwa'];// 简写
      constructor() {//和ES6类的写法很像
        this.names=['react', 'vue', 'angular', 'flutter', 'pwa'];
      }
      // 有返回值
      function greet():string {
         return this.name;
      }
      // 不期望返回值 isMale?: boolean声明为可传参数
      function setName(name: string, isMale?: boolean): void {
        this.name = name;
      }
    }
  ```

[slide]
- 开发环境简介
- 工具安装 angular-cli
  - ```
      npm i -g @angular/cli
    ```
- 常用命令解释
  - ```
      ng new my-app // 构建项目脚手架
    ```
    选择是否加入路由模块以及哪种css预处理器。

    - 可ctrl+c取消自动安装node_modules，手动进入项目npm install
    
    - node-sass安装不上可切换淘宝镜像库或者用cnpm安装

    - npm config set registry https://registry.npm.taobao.org 再 npm install

    - npm install -g cnpm cnpm install 

[slide]

- 构建后的项目结构：
    ```
    |-- app/
    |   |-- app.component.css
    |   |-- app.component.html
    |   |-- app.component.spec.ts
    |   |-- app.component.ts
    |   |-- app.module.ts
    |   `-- app-routing.module.ts //路由配置
    |-- assets/        //放置静态资源
    |-- environments/  //环境配置
    |   |-- environment.prod.ts
    |   `-- environment.ts
    |-- favicon.ico
    |-- index.html     //根html文件
    |-- main.ts        //指明整个应用主入口的配置文件，ng serve跑服务的依据
    |-- polyfills.ts   //语法兼容polyfill
    |-- styles.css     //全局样式文件
    |-- test.ts        //单元测试用的
    `-- tsconfig.app.json  //类似于webpack.config.js
    ```
    ```
      $ ng serve --open //启动本地开发环境 自动打开浏览器http://localhost:4200/ --port 指定端口
    ```
    ```
      $ ng g c article //生成组件 如果不想要或者自定义前缀可在angular.json里修改prefix属性
    ```
    ```
      $ ng g s ./serveices/eventBus //生成服务 可指定目录
    ```

[slide]
- 语法讲解

- 插值表达式{{}}

  将业务逻辑中的数据通过插值表达式显示在模板文件，即html页面上，或者将html页面上的事件传输到业务逻辑。
  ```javascript
  <p>标题是{{title}}</p>
  ```
  插值运算 加减乘除/字符串拼接/三元/函数调用
  ```
  <div>{{5+3}},{{5-3}},{{5*3}},{{5/3}},{{ "a" + "b" }},{{true ? 1 : 0}}</div>
  ```
[slide]
- 单向绑定

  1. 属性绑定
  ``` html
  <app-show-user [name]="name"></app-show-user>
  ```
  2. 事件绑定
  ``` html
  <button (click)="postForm()">点击提交</button>
  ```

- 双向绑定
  ``` html
  您的姓名：<input type="text" [(ngModel)]="userName">
  ```
  为了ngModel能够解析需要单独引入FormsModule模块
  ```javascript
  import {FormsModule} from "@angular/forms";
  ```

[slide]
- controller
  - 旧版写法

  ```JavaScript
  angular
    .module("app.controllers")
    .controller('authCtrl', authCtrl);

  function authCtrl($scope){
    //...
  }
  ```

  - 新版写法

  ```TypeScript
    @Component({
      selector: 'auth',
      templateUrl: './auth.component.html',
      styleUrls: [ './auth..component.css' ],
    })

    export class authComponent {
      //...

      constructor(){
        //...
      }
    }
  ```

[slide]
- directives

  1. 说明

    在新版本中指令特指在view中声明的各种angular语法譬如\*ngIf,\*ngFor等

  2. 新旧语法对比

  ```html
  <button ng-click="method()">click</button>
  <button (click)="method()">click</button>

  <input type="text" ng-model="name">
  <input type="text" [(ngModel)]="name">
  <!--判断指令-->
  <div ng-if="names.length">
    if
  </div>
  <div *ngIf="names.length">
    if
  </div>

  <h3 ng-show="isShow">
    show
  </h3>
  <h3 [hidden]="!isShow">
    Your favorite hero is: {{favoriteHero}}
  </h3>
  ```

[slide]

``` html

<ul>
  <li ng-for="name in names">{{ name }}</li>
</ul>
<ul>
  <li *ngFor="let name of names">{{ name }}</li>
</ul>

<a ng-href="companyUrl">to company</a>
<a [href]="companyUrl">to company</a>
<!--样式指令-->
<div ng-class="{active: isActive}">

</div>
<div [ngClass]="{active: isActive}">

</div>

<div ng-style="{color: colorPreference}">
<!--多style-->
<div [ngStyle]="{color: colorPreference}">
<!--单个style绑定-->
<div [style.color]="colorPreference">

<!--过滤器-->
<p>{{title | uppercase}}</p>
<p>{{currentTime | date: "yyyy-MM-dd HH:mm:ss" }}</p>
```

[slide]
- service

- 注册service

  ```TypeScript
  import { Injectable, Type } from '@angular/core';
  
  @Injectable()
  export class TestService{
    splitStrToArr (str:string){
      return str.split('')
    }
  }
  ```
- 使用service
  ```TypeScript
  import { TestService } from '../service/test.service';
  export class BrotherComponent implements OnInit {

    constructor(private testService: TestService) { }

    splitStrToArr(str: string) : Array<string> {
      return this.testService.splitStrToArr(str);
    }
  }
  ```

[slide]
- 服务总线 组件间分享数据
  1. 注册服务
  ```javascript
  ng g s ./services/eventBus
  import { Injectable } from "@angular/core";
  import { Observable, Subject } from "rxjs";
  @Injectable({
    providedIn: "root"
  })
  export class EventBusService {
    public eventBus: Subject<string> = new Subject();
    constructor() {}
  }
  ```

  2. 组件内发射数据
  ```javascript
  this.eventBusService.eventBus.next("child组件发送的数据");
  ```

  3. 组件接收数据
  ```javascript
  this.eventBusService.eventBus.subscribe(arg => {
      console.log(`接收到事件${arg}`);
  });
  ```

[slide]
- module注册入口

  ``` TypeScript
  import { BrowserModule } from '@angular/platform-browser';
  import { NgModule } from '@angular/core';

  import { AppRoutingModule } from './app-routing.module';
  import { AppComponent } from './app.component';

  @NgModule({
    declarations: [
      AppComponent
    ],
    imports: [
      BrowserModule,
      AppRoutingModule
    ],
    providers: [],
    bootstrap: [AppComponent]
  })
  export class AppModule { }
  // import部分是模块以及装饰器的引入。
  // declarations部分是声明模块的内部成员。
  // imports部分是导入其它模块。
  // providers指定应用程序根级别需要使用的service。
  // bootstrap是app启动的根组件。
  // export控制将那些内部成员暴露给外部使用。
  ```

[slide]
- 父子组件通信
```javascript
// 输入
<child title="我的子组件"></child>
@Input()
public title:string =""
// 输出
<child title="我的子组件" #child (follow)="getFollow($event)"></child>
@Output()
public follow = new EventEmitter();
this.follow.emit("子组件传来的数据");
```
 - @Output的实现必须使用EventEmitter来实现。

 - @Output() mySignal = new EventEmitter<boolean>();// 声明传递的数据类型

 - 标签变量引用
  ```javascript
  <child title="我的子组件" #child (follow)="getFollow($event)"></child>
  <button (click)="child.sayHello()">子组件说话</button>
  ```
[slide]
- 内容投影

  ng-content标签将父组件模版上的任意片段投影到子组件上。

  1. 子组件中使用<ng-content>指令来标记投影点
  ```
  <ng-content></ng-content>
  <ng-content selecter=".header"></ng-content>
  <ng-content selecter=".footer"></ng-content> 
  ```

  2. 父组件把要投影到子组件的投影点的html片段写到子组件的标签中
  ```
  <child>
    <div>父组件投影到子组件</div>
    <div class="header">header</div>
    <div class="footer">footer</div>
  </child>
  ```

  3. 属性绑定插入html片段

    ```
    <div [innerHTML]="divContent"></div>

    public divContent:string = "<div>属性绑定绑innerHTML</div>";
    ```

[slide]
- 路由导航

  ```Typescript
  import { NgModule } from '@angular/core';
  import { Routes, RouterModule } from '@angular/router';
  import { ChildComponent } from "./child/child.component";
  import { BrotherComponent } from "./brother/brother.component";
  const routes: Routes = [{
    path: '',
    component: ChildComponent
  },
  {
    path: 'brother',
    component: BrotherComponent
  }];
  @NgModule({
    imports: [RouterModule.forRoot(routes)],
    exports: [RouterModule]
  })
  export class AppRoutingModule { }
  ``` 

  ```html
  <a [routerLink]="['/']">child</a><br/>
  <a [routerLink]="['/brother']">brother</a>
  <!--router-outlet 相当于一个占位符,在Angular中根据路由状态动态插入视图。-->
  <router-outlet></router-outlet>
  ```
  - 也可以注入Router进行跳转
  ```
  import { Router } from '@angular/router';
  ...
  constructor(private router: Router){}
  jumpHandle(): void {
  this.router.navigate(['brother'], {
      queryParams: {
          title: 'moon'
      }
  });
  ```
[slide]
- 路由传参
  ```
  // html
  <a [routerLink]="['/brother',1]" [queryParams]="{title:'sun'}">brother</a>
  // 路由配置
  {
    path: 'brother/:id',
    component: BrotherComponent,
    data:[{Data:'路由配置静态数据'}]
  }
  // ts 取数据
  import { ActivatedRoute } from '@angular/router';
  ···
  constructor(private activatedRoute: ActivatedRoute) { }
  this.activatedRoute.queryParams.subscribe(queryParams => {
      let title = queryParams.title;
      console.log(`传递的title参数${title}`)
  });
  console.log(`第二种方式${this.activatedRoute.snapshot.queryParams['title']}`);
  // 配置路由/:id
  console.log(`第三种方式${this.activatedRoute.snapshot.params['id']}`);
  // 路由配置的data
  console.log(`路由配置的data${this.activatedRoute.snapshot.data[0].Data}`);
  ```

[slide]
- 生命周期
  - ngOnChanges	当被绑定的输入属性的值发生变化时调用，首次调用一定会发生在 ngOnInit之前。
  - ngOnInit	在第一轮 ngOnChanges 完成之后调用。 ( 译注：也就是说当每个输入属性的值都被触发了一次 ngOnChanges 之后才会调用 ngOnInit ，此时所有输入属性都已经有了正确的初始绑定值 )	
  - ngDoCheck	在每个 Angular 变更检测周期中调用。
  - ngAfterContentInit	当把内容投影进组件之后调用。
  - ngAfterContentChecked	每次完成被投影组件内容的变更检测之后调用。
  - ngAfterViewInit	初始化完组件视图及其子视图之后调用。
  - ngAfterViewChecked	每次做完组件视图和子视图的变更检测之后调用。
  - ngOnDestroy	当 Angular 每次销毁指令 / 组件之前调用。

  一般在ngOnInit()函数中获取初始数据是比较好的。

[slide]
-  http服务
  ```javascript
  // app.module.ts
  import { HttpModule } from '@angular/http';
  import { HttpClientModule } from '@angular/common/http';
  // services
  import { HttpClient, HttpResponse } from '@angular/common/http';

  this.httpClient.request(UserService.METHOD_POST, url, options).subscribe((data)=>{});
  ``` 

[slide]
# Thanks！