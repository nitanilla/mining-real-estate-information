个人简历
======================
唐志荣的个人简历

## 个人信息

**姓名**：唐志荣

**性别**：男

**学校专业**：**北京邮电大学**网络技术研究院

**github**：https://github.com/tangzhirong

**blog**：https://www.cnblogs.com/tangzhirong

## 技术能力

专注Web前端，致力于全栈开发，熟练掌握JavaScript、HTMl、CSS以及JavaScript框架来搭建web应用。

* 前端基础：掌握HTML5、CSS3、JavaScript；熟悉原生JavaScript，理解作用域、闭包、this和原型对象、继承、异步等原理
* 前端框架：熟悉各主流前端框架的实现原理，掌握jQuery、Vuejs，对Angular.js、React.js也有一些了解
* JavaScript模块化：熟悉AMD、CMD、CommonJs规范，掌握RequireJS、NodeJs模块化开发
* 掌握CSS预编译器：Sass
* 掌握项目构建工具：Grunt、Webpack、Fis（由百度FEX团队开发）
* 掌握项目管理和协同工具的使用：Git
* 掌握基本后端开发：NodeJS、Python
* 掌握web相关技术：HTTP2.0、Websocket、SEO、Express、MongoDB、Django、Celery、Redis等

##个人经历

* 2011年进入北京邮电大学计算机科学与技术专业学习
* 大二开始接触Web，开始学习Web技术，独立完成了几个课程大作业的网站开发
* 大四进入”东信北邮“战略研发部实习，设计了新浪微博用户大数据分析的原型和算法，完成了分析结果的Web大数据可视化工作
* 2015年进入北京邮电大学网络技术研究院学习
* 研一正式开始做前端，开始系统地学习前端技术
* 研一加入了“艺伴”创业团队，主要负责后台管理系统整站开发、基于微信的投票网站和移动端APP的NodeJs后台开发等
* 研一加入了实验室泛搜索项目组，主要负责Django网站开发、使用Python编写iOS客户端后台API等
* 研二加入了实验室房地产大数据分析平台前端组，并担任组长，主要负责技术选型、核心代码编写以及管理团队协作开发等

## 个人作品

### [链区网]
项目地址： https://github.com/tangzhirong/real_estate
- 简介
  + 链区网是一个针对小区的房地产大数据分析可视化平台，通过数据报表、地图组件、图表组件等为用户提供了人性化的全国小区数据展示服务。
- 项目收获
  + 熟悉了HTML5、CSS3、Ajax、Express、NodeJs、Mysql、RestfulApi等技术
  + 熟悉了基于Highcharts、Highmaps、百度地图API等第三方库的jQuery组件开发
  + 熟悉了前端性能优化的常用方法，比如：减少HTTP请求、DOM元素异步加载等
  + 熟悉了如何使用git来进行团队开发协作
  + 对于前端模块化有了更加深层次的理解，理解了组件化开发对于前端团队开发的重要性
- 项目总结
  + 这个项目我作为前端组组长，主要负责技术选型、核心代码编写以及管理团队协作开发等。
  + 关于技术选型，考虑到页面可以拆分成多个组件，多个组件间存在一定的数据逻辑关联，实现前端组件化是必要的。并且，双向数据绑定也能够让前端逻辑大大简化，所以在前端框架上我倾向于更轻量级的Vuejs。但是，由于团队其他成员对Vuejs很陌生，最后决定使用jQuery，虽然通过编写jQuery组件的形式实现了组件化，但前端逻辑较为复杂。由于NodeJs很好地实现了commonJs规范，团队成员也可以用自己熟悉的JS来编写服务器端代码，我们选用了NodeJS+Express的方案来搭建网站，前端通过Ajax，以RestfulApi的形式与后台交互（MySQL操作和部分SparkSql操作）。
  + 关于前端性能优化，由于这是一个大数据分析网站，对前端性能要求较高。我们使用了前端构建工具fis进行了资源的压缩合并、图片和地图资源缓存等策略减少了Http请求数，使用Nodejs在服务器端渲染大量的数据、书写innerHTML等方法减少了DOM操作，使用列表懒加载、scroll触发请求等方法提升了页面性能，还有一些代码规范的要求，比如：避免css表达式、避免eval语句等等。
  + 在技术实现上，后续会考虑将项目框架迁移到Vuejs，使用Webpack、RequireJs等前端工具进行项目重构；在网站设计与完善上，后续会考虑更具吸引力的前端可视化算法和方案。
  
### [泛搜索]
项目地址： https://github.com/tangzhirong/easyFind
- 简介
  + 泛搜索是一个基于ibeacon低功耗蓝牙设备定位的帮助寻找走失老人、小孩的参与式感知平台，目前提供Web端网站、IOS移动端APP这两个平台的应用。该平台涉及到的核心算法包括：高覆盖率的参与者选择算法、稀疏感知数据恢复算法、三点定位算法以及激励分发算法等。
- 项目收获
  + 熟悉了Bootstrap、jQuery、Python、Django、Celery、Redis、Websocket等技术
  + 熟悉了前后台的交互和协作方式
  + 根据项目执行异步和周期性任务后进行消息推送的需求，改写了django-websocket-redis源码，提高了自己理解源码和造轮子的能力
  + 加强了自己的算法功底
- 项目总结
  + 这个项目是我研究生期间在实验室参与的核心项目，主要负责Django网站开发、使用Python编写iOS客户端后台API、算法研究与实现等工作。
  + 项目锻炼了我独立解决问题的能力，比如实现适合项目的技术方案：数据存储（Mongodb）、服务器端异步响应和周期任务（Celery）、消息推送（Websocket）、数据缓存（Redis）、图片压缩存储、静态资源优化（Nginx）等。
  + 项目锻炼了我的团队协作能力，”文档驱动+及时交流“的git分支协作方式让我和学长学姐们配合融洽。
  
### [个人博客]
项目地址： https://github.com/tangzhirong/personal-blog
- 简介
  + 这是我使用Express框架搭建的个人博客，能够实现个人技术分类管理、支持markdown的博文发表、博文浏览、点赞、转发、评论等功能。
- 项目收获
  + 熟悉了NodeJs、jQuery、Express、Mongoose等技术
  + 熟悉了CSS布局、解决常见浏览器兼容问题的方法等
- 项目总结
  + 纯属练手，个人博客在”博客园“，本科写的博文较多，现在人变懒了～～
 
 
### [艺宝]
MUI项目地址： https://github.com/tangzhirong/Yibao

React项目地址： https://github.com/tangzhirong/Yibao_dcloud
- 简介
  + 艺宝是一个帮助美术生艺考的应用，这是我在创业团队做的一个项目，主要包括一个后台管理系统和移动端APP。后台管理系统的前端使用”AngularJs+Bootstrap“进行开发，移动端APP的前端框架由于性能瓶颈，经历了一个很长的变迁：”AngularJs->MUI->ReactJs",整个项目的后台均采用NodeJs进行开发。
- 项目收获
  + 熟悉了AngularJs、ReactJs、NodeJs、Mongoose、jsonp等技术，对前端框架的原理和优缺点有了一定的理解
  + 编写过API请求的Cookie身份检验、防JS注入等NodeJs中间件，对网站的安全性有了一定的认识和理解
  + 加深了对JavaScript闭包、异步等特性的理解
  + 熟悉了q、underScore等npm第三方库的使用
  + 团队每周召开会议讨论技术问题，对代码质量有了更加严格的要求
  + 积累了一些移动端开发的经验
- 项目总结
  + 这个项目我主要负责后台管理系统的整站开发、基于微信的投票网站和移动端APP的NodeJs后台开发，参与了项目的前后端的开发，对NodeJs全栈开发有了极大的兴趣。
  + 在项目leader的领导下，经历了一个产品从无到上线的全过程，学到了很多干货。更重要的是，我学到了”从自己思考、到团队讨论，再到合作解决问题“的方法。
  + 不是什么框架火就是什么框架好，契合业务需求的框架才是最好的框架！


### [组件开发]
轮播图组件：https://github.com/tangzhirong/sass-slider

日历组件：https://github.com/tangzhirong/jquery-calendar

浮出层组件：https://github.com/tangzhirong/popUpper

表单组件：https://github.com/tangzhirong/form-constructor
- 简介
  + 平时练手开发过一些组件，当然也有一些是项目需求，包括原生组件和框架组件（jQuery、Vue）

  
  
## 自我简介

从大二开始了解web技术，大二开始正式投入学习web各种技术。对于web有着极高的兴趣和热情，每天坚持学习web。

目前为止对于前端技术比较了解，关注最新的前端技术，认为优秀的前端项目需要做的事情其实很多，前端工程师不比算法和后台工程师Low，目标是成为一名优秀的web全栈工程师。

拥有较强的学习能力和沟通能力，能够比较良好的和团队成员协同完成开发。
