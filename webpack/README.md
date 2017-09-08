# webpack
webpack是模块化打包工具。

## 使用步骤
  + 1.全局安装webpack
  ```
    npm install -g webpack
  ```
  + 2.npm配置pakeage.json  
  ```
     npm init
  ```
  + 3.项目中安装webpack
  ```
   npm install webpack --save-dev
  ```

## webpack.config.js
```
var path=require("path");
moudle.exports={
    entry:"./src/main.js",  //需打包的文件
    output:{
      path:path.resolve(__dirname,"./dist"),   //打包生成在相应的文件目录下
      filename:"bundle.js"    //定义打包生成的文件名
    }
}

```
