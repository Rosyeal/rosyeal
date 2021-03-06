# 1. entry
# 2. output中的publicPath
# 3. hash, chunkhash
# 4. hash
# 5. hashmap
# 6. compiler和compilation
Compiler 代表了整个 Webpack 从启动到关闭的生命周期，而 Compilation 只是代表了一次新的编译
# 7. Manifest和Runtime
runtime包含：在模块交互时，连接模块所需的加载和解析逻辑。包括浏览器中的已加载模块的连接，以及懒加载模块的执行逻辑。

Manifest：通过manifest，webpack及其插件”知道“应该哪些文件生成，webpack能够对‘你的模块映射到输出bundle的过程’保持追踪。

# 8. Manifest缓存， WebpackManifestPlugin
# 9. style-loader和HMR
# 10. SourceMap用来跟踪错误, 不同的选项体现在devtool的配置上
# 11. HtmlWebpackPlugin
# 12. CleanWebpackPlugin
# 13. express webpack-dev-middleware搭建本地开发服务器
# 14. Tree Shaking移除JavaScript上下文中的未引用代码(没有被import)。UglifyJS
# 15. webpack-merge
# 16. 代码分离：入口起点， 防止重复（使用CommonsChunkPlugin去重和分离chunk），动态导入（通过模块的内联函数调用来分离代码）
# 17. 代码分离：webpack.optimize.CommonsChunkPlugin，ExtractTextPlugin，bundle-loader，promise-loader。
webpack.optimize.CommonsChunkPlugin和entry中的vendor，CommonsChunkPlugin插件在webpack4中已经被替换。

取而代之的是如下配置方案:

# 18. hash和chunkhash，hash在output.filename中包含一个构建相关的hash，chunkhash是在output.filename中包含一个chunk相关的hash。
每次运行构建，输出的dist文件中的文件名都可能不同，因为webpack在入口chunk中，包含了某些样板(boilerplate)，特别是runtime和manifest。
通过以下步骤可以解决这个问题：

**提取模板(Extracting Boilerpalte)**,通过CommonsChunkPlugin
```javascript
new webpack.optimize.CommonsChunkPlugin({
  name: 'manifest'
})
```

将第三方库提取出来，通过客户端的长效缓存机制，通过命中缓存来消除请求，同时还能保证客户端代码和服务端代码版本一致。

CommonsChunkPlugin的‘vendor’实例，必须在‘manifest’实例之前引入。

**模块标识符[module Identifiers]**,由于每个module.id会基于默认的解析顺序(resolveorder)进行增量。也就是说，当解析顺序发生变化，ID也会随之变化。

通过HashedMoudleIdsPlugin解决这个问题
# 19. 创建Library，externals，library&&libraryTarget和entry中的vendor

# 20. Shimming（垫片）,处理老旧模块
**全局变量**，new webpack.ProvidePlugin({
	_: 'lodash'
})
**细粒度shimming**，imports-loader
```javascript
module: {
  rules: [
    {
      test: requrire.resolve('index.js'),
      use: 'imports-loader?this=>window'
    }
  ]
}
```
**全局exports**
```javascript
{
  test: require.resolve('global.js'),
  use: 'exports-loader?file,parse = helpers.parse'
}
```
**polyfills**

# 21. 渐进式网络应用程序(Progressive Web Application)(了解)WorkboxWebpackPlugin
PWA可以用来做很多事，其中最为重要的是，在离线（offline）时应用程序能够继续运行功能，这是通过**Service Workers**的网络技术来实现的。

# 22. 管理依赖

# 23. publicPath

# 24. 集成，webpack（打包工具）和gulp（任务流模式）

# 25. 构建性能

# 26. module
noParse
rules 规则数组，每个规则可以分为三部分 —— 条件（condition)， 结果（results)和嵌套规则(nested rule)。

### Rule条件

两种输入值：
1. resource
2. issuer

### Rule结果

两种输入值：
1. 应用的loader
2. Parser选项

### 嵌套规则

使用属性值rules和oneOf指定嵌套规则

# 27. postcss

# 28. 辅助插件
chalk

# 29. node常用api
process.argv

# 31. fork-ts-checker-webpack-plugin
# 32. resolve解析
# 33. svgo-loader svg精简压缩工具

# 34. bail属性，表示在错误发生时立即抛出错误


