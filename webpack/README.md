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

## webpack配置文件
  ```
      entry: string 单个入口单独文件 | object 多个入口多个文件 | array 多个入口合并在一个文件中

      [name]值 -> 指entry中传入文件定义的key值
      [hash]值 -> 文件的版本号
      [chunkhash] -> 指每个文件的hash值
  ```

  ## 自动生成项目中html文件
  html-webpack-plugin


## webpack.config.js
```
var path=require("path");
var htmlwebpackPlugin=require("html-webpack-plugin");

moudle.exports={
    entry:{
      page1:"./src/script/main.js",
      page2:"./src/script/main2.js"
      },  //需打包的文件
    output:{
      path:path.resolve(__dirname,"./dist"),   //打包生成在相应的文件目录下
      filename:"js/[name]-[hash]bundle.js"    //定义打包生成的文件名
      publicpath:""        //生成绝对路径的文件
    },
    module:{
      rules:[
          {
            test:/\.js/,
            use:{
              loader:"babel-loader",
              exclude:path.resolve(__dirname,'/node_modules/') ,
              include:path.resolve(__dirname,'./src/'),
              options:{
                preset:["es2015"]
              }
            }
            },
          {
            test:/\.html/,
            use:{
              loader:"html-loader",    
              options:{
              }
            },
            {
              test:/\.css/,
              exclude:path.resolve(__dirname,'/node_modules/') ,
              include:path.resolve(__dirname,'./src/'),
              use:[
                  {loader:"css-loader"},
                  {loader:"style-loader"},
                  {
                    loader:"postcss-loader",
                    options:{
                      plugins:(loader)=>{
                            require('autoprefixer')();
                      }
                    }
                  }
              ]
            }
          }
      ]
    },
    plugins:[
      new htmlwebpackPlugin({        //该插件自动生成html页面
        filename:"[name]-[hash].html"
        template:"index.html",
        inject:"head",     //脚本文件生成在指定部分
        minify:{     //压缩html文件
          removeComments:true,     //删除注释
          collapseWhitespace:true  //删除空格
        },
        chunks:["page1"]           //选择引用指定js
        excludeChunks:["page1"]    //排除指定js
        });
    ]

}

```
## loader转换器
loader转换器能够将各种类型的资源转换成javascript模块。
