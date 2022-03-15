##### 针对webpack热加载失效报错问题

![image-20201214141531046](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\image-20201214141531046.png)

webpack.config.js中配置的devServer和HotModuleReplacementPlugin冲突导致的

**webpack-dev-server**是小型的webpack自带的前端服务器，能够提供热加载功能。在packjson里配置hot或者下图的deverServer设置hot:true都可以实现热加载。

**HotModuleReplacementPlugin**简称HMR,也就是模块热替换插件。一般来说前者设置hot就自动添加这个插件,如果再设置HMR,可能就会出现一直热加载现象，一瞬间就会满栈也就是上图的报错。

**解决办法**：将标注的地方任意注释一处

![image-20201214142019799](C:\Users\11026\AppData\Roaming\Typora\typora-user-images\image-20201214142019799.png)