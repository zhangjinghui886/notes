 ### 新一代打包工具

为什么使用这个工具？

- 加快本地项目启动
  - 1-vite使用esbuild预构建依赖，这个功能是使用go编写的，速度很快
  - 2-使用在当前浏览器中使用的到的js代码才会被转换
- 加速开发时代码变动更新速度
  - Vite只找到已编辑的模块，对他进行更新，并不是更新整个文件
  - vite利用http请求头，加速这个页面的重新加载，依赖通过cache-control: max-age 进行强缓存，

### Vite

> 包含两部分

- 一个开发服务器 利用原生es模块提供了丰富的内建功能
- 一套构建指令，使用rollup打包代码，预配置输出高度优化的静态资源用于生产

### 功能

+ 依赖构预建
+ 静态资源处理
+ 构建生产版本
+ 环境变量与模式
+ 服务端渲染
+ 后端集成

### 配置

共享配置

本地开发配置

打包构建生产包配置

```js
1-target: 
构建的目标 主要是兼容浏览器

2-outDir
打包到哪个目录下

3-assetsDir
指定生成静态资源存放的目录

4-assetsInlineLimit
阈值 default: 4096b 小于这个值 将资源内联为base64编码，减少http请求

5-cssCodeSplit
是否进行css代码拆分，如果不拆分，就是讲所有的css提取到一个css文件中 default: true 【拆分】

6-sourcemap
构建后是否生成sourcemap文件 default: false[不生成]

7-rollupOptions
自定义底层的rollup打包配置，
```



依赖优化配置

服务端渲染配置





## rollup打包工具

> Rollup 是一个 JavaScript 模块打包器，可以将小块代码编译成大块复杂的代码，例如 library 或应用程序。Rollup 对代码模块使用新的标准化格式，这些标准都包含在 JavaScript 的 ES6 版本中，而不是以前的特殊解决方案，如 CommonJS 和 AMD。ES6 模块可以使你自由、无缝地使用你最喜爱的 library 中那些最有用独立函数，而你的项目不必携带其他未使用的代码。ES6 模块最终还是要由浏览器原生实现，但当前 Rollup 可以使你提前体验。

## webpack打包工具

> 

