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
    entry:{
      page1:"./src/script/main.js",
      page2:"./src/script/main.js"
      },  //需打包的文件
    output:{
      path:path.resolve(__dirname,"./dist"),   //打包生成在相应的文件目录下
      filename:"[name]-[hash]bundle.js"    //定义打包生成的文件名
    }
}

```

## webpack配置文件
```
    entry: string 单个入口单独文件 | object 多个入口多个文件 | array 多个入口合并在一个文件中

    [name]值 -> 指entry中传入文件定义的key值
    [chunkhash] -> 指每个文件的hash值
```
