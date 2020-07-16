title: vue安装与创建
author: 大白腿
tags:
  - vue
categories:
  - vue
date: 2020-05-24 14:49:00
---
安装vue cli3
```
npm install -g @vue/cli
```
```
vue create 名字    --创建文件 
```
第二个之后选 1.babel  4.router  5.vuex  6.css
      save this 选no
      
      
1、vue create 搭建新项目


vue create <Project Name> //文件名 不支持驼峰（含大写字母）
具体操作如下：

首先，会提示你选择一个preset（预设）：

① 除最后两个，其他选项都是你此前保存的预设配置

如果没有配置保存过，则只有以下两个选项：

② default（babel，eslint）：

默认设置（直接enter）非常适合快速创建一个新项目的原型，没有带任何辅助功能的 npm包

③ Manually select features：

手动配置（按方向键 ↓）是我们所需要的面向生产的项目，提供可选功能的 npm 包


手动配置，根据你需要用方向键选择（按 “空格键”选择/取消选择，A键全选/取消全选）对应功能


简介：
```
? Check the features needed for your project: (Press <space> to select, <a> to toggle all, <i> to invert selection)
>( ) Babel                           //转码器，可以将ES6代码转为ES5代码，从而在现有环境执行。                      
 ( ) TypeScript// TypeScript是一个JavaScript（后缀.js）的超集（后缀.ts）包含并扩展了 JavaScript 的语法，需要被编译输出为 JavaScript在浏览器运行，目前较少人再用
 ( ) Progressive Web App (PWA) Support// 渐进式Web应用程序
 ( ) Router                           // vue-router（vue路由）
 ( ) Vuex                             // vuex（vue的状态管理模式）
 ( ) CSS Pre-processors               // CSS 预处理器（如：less、sass）
 ( ) Linter / Formatter               // 代码风格检查和格式化（如：ESlint）
 ( ) Unit Testing                     // 单元测试（unit tests）
 ( ) E2E Testing                      // e2e（end to end） 测试
 ```
选择完后直接enter，然后会提示你选择对应功能的具体工具包，选择自己擅长或者使用广泛的（方便遇到问题时百度），简介如下：

①是否使用history router：


![upload successful](/images/pasted-26.png)
Vue-Router 利用了浏览器自身的hash 模式和 history 模式的特性来实现前端路由（通过调用浏览器提供的接口）

hash： 浏览器url址栏 中的 # 符号（如这个 URL：http://www.abc.com/#/hello，hash 的值为“ #/hello”），hash 不被包括在 HTTP 请求中（对后端完全没有影响），因此改变 hash 不会重新加载页面

history：利用了 HTML5 History Interface 中新增的 pushState( ) 和 replaceState( ) 方法（需要特定浏览器支持）。单页客户端应用，history mode 需要后台配置支持（详细参见：https://router.vuejs.org/zh/guide/essentials/history-mode.html）

② css预处理器

主要为css解决浏览器兼容、简化CSS代码 等问题（*<u style="box-sizing: inherit;"> Sass诞生于2007年，最早也是最成熟的一款CSS预处理器语言。</u>）
```
? Please pick a preset: Manually select features
? Check the features needed for your project: Router, Vuex, CSS Pre-processors, Linter, Unit
? Pick a CSS pre-processor (PostCSS, Autoprefixer and CSS Modules are supported by default):
> SCSS/SASS  //Sass安装需要Ruby环境，是在服务端处理的，SCSS 是 Sass3新语法（完全兼容 CSS3且继承Sass功能）
  LESS       //Less最终会通过编译处理输出css到浏览器，Less 既可以在客户端上运行，也可在服务端运行 (借助 Node.js)
  Stylus     //Stylus主要用来给Node项目进行CSS预处理支持，Stylus功能上更为强壮，和js联系更加紧密，可创建健壮的、动态的的CSS。
③ ESLint：
```
提供一个插件化的javascript代码检测工具
```
? Pick a linter / formatter config: (Use arrow keys)
> ESLint with error prevention only
  ESLint + Airbnb config
  ESLint + Standard config
  ESLint + Prettier         //使用较多
  ```
④ 何时检测：
```
? Pick additional lint features: (Press <space> to select, <a> to toggle all, <i> to invert selection)
>( ) Lint on save                    // 保存就检测
 ( ) Lint and fix on commit          // fix和commit时候检查
 ```
⑤ 单元测试 ：
```
? Pick a unit testing solution: (Use arrow keys)
> Mocha + Chai  //mocha灵活,只提供简单的测试结构，如果需要其他功能需要添加其他库/插件完成。必须在全局环境中安装
  Jest          //安装配置简单，容易上手。内置Istanbul，可以查看到测试覆盖率，相较于Mocha:配置简洁、测试代码简洁、易于和babel集成、内置丰富的expect
  ```
⑥ 如何存放配置 ：
```
? Where do you prefer placing config for Babel, PostCSS, ESLint, etc.? (Use arrow keys)
> In dedicated config files // 独立文件放置
  In package.json // 放package.json里
  ```
⑦ 是否保存本次配置（之后可以直接使用）：
```
? Save this as a preset for future projects? (Y/n) // y:记录本次配置，然后需要你起个名; n：不记录本次配置
```
链接：https://www.jianshu.com/p/72c3da7b013c