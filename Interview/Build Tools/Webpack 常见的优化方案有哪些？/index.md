---
tags:
  - Webpack
---

1. 升级 webpack 版本，3 升 4，实测是提升了几十秒的打包速度
2. 使用**Tree Shaking和Scope Hoisting**来减少代码体积和模块构建时间，其中Tree Shaking可以去除未使用的代码，而Scope Hoisting可以将模块内的代码尽量合并到一个函数（单一作用域）中，以减少函数声明和闭包的数量。
3. 使用**splitChunksPlugin插件**来将公共代码抽离成单独的chunk，以减少代码重复和提高缓存命中率。
4. 合理配置**resolve.alias和resolve.extensions**选项来减少Webpack查找文件的时间。
5. 针对**生产环境，可以开启代码压缩以及多进程并行处理**等优化方式，以减少构建时间和服务器负载。
6. 使用 **DLLPlugin 和 DllReferencePlugin** 来预先编译一些稳定不变的代码，以减少每次构建的时间。
7. 使用 **HappyPack** 来启用多线程并发处理，以加速代码构建和增强开发体验。
8. 对于图片、字体等资源文件，可以通过**url-loader和file-loader**等loader设置较小的limit值，将文件转换成base64编码的字符串内嵌在js文件中，以减少http请求次数。