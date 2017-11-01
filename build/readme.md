> 详情请看代码注释

#### build/dev-server.js文件  
1,检查node和npm的版本、引入相关插件和配置  
2,webpack对源码进行编译打包并返回compiler对象    
3 .创建express服务器  
4 .配置开发中间件（webpack-dev-middleware）和热重载中间件（webpack-hot-middleware）  
5 .挂载代理服务和中间件  
6 .配置静态资源  
7 .启动服务器监听特定端口（8080）  
8. 自动打开浏览器并打开特定网址（localhost:8080）  

**说明：** express服务器提供静态文件服务，不过它还使用了http-proxy-middleware，一个http请求代理的中间件。前端开发过程中需要使用到后台的API的话，可以通过配置proxyTable来将相应的后台请求代理到专用的API服务器。  


### build/webpack.base.conf.js

1. 配置webpack编译入口  
2. 配置webpack输出路径和命名规则  
3. 配置模块resolve规则  
4. 配置不同类型模块的处理规则    

**说明：** 这个配置里面只配置了.js、.vue、图片、字体等几类文件的处理规则，如果需要处理其他文件可以在module.rules里面另行配置。

### build/webpack.dev.conf.js

1. 将webpack的热重载客户端代码添加到每个entry对应的应用  
2. 合并基础的webpack配置  
3. 配置样式文件的处理规则，styleLoaders  
4. 配置Source Maps  
5. 配置webpack插件  

### build/utils.js

> utils提供工具函数，包括生成处理各种样式语言的loader，获取资源文件存放路径的工具函数。 
1. 计算资源文件存放路径 
2. 生成cssLoaders用于加载.vue文件中的样式 
3. 生成styleLoaders用于加载不在.vue文件中的单独存在的样式文件


### build/dev-client.js

dev-client.js里面主要写了浏览器端代码，用于实现webpack的热更新。

### build/build.js  

1. loading动画  
2. 删除目标文件夹  
3. 执行webpack构建  
4. 输出信息  
**说明：** webpack编译之后会输出到配置里面指定的目标文件夹；删除目标文件夹之后再创建是为了去除旧的内容，以免产生不可预测的影响。

### build/webpack.prod.conf.js  
 
1. 合并基础的webpack配置  
2. 配置样式文件的处理规则，styleLoaders  
3. 配置webpack的输出  
4. 配置webpack插件  
5. gzip模式下的webpack插件配置  
6. webpack-bundle分析  
**说明：** webpack插件里面多了丑化压缩代码以及抽离css文件等插件。

### build/check-versions.js

最后是build文件夹下的check-version.js，它完成对node和npm的版本检测