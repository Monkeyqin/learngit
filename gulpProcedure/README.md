## Gulp
Gulp是Node.js中的自动任务处理器,并且能够完成js/css/sass/less/image/html等文件的测试、检查、合并、格式化等步骤,前端开发过程中对代码进行构造的工具,是自动化项目构建的利器。该工具可以对网站资源进行优化,而且重复的任务可以使用正确的工具完成。

### Gulp的使用步骤
安装Node.js ->  全局安装gulp -> 项目中安装gulp和配置gulp插件 ->配置gulpfile.babel.js文件 -> 运行任务

### 使用命令行
+ node -v / npm -v / gulp -v 查看node和npm的版本号
+ cd 定位到目录
+ dir 列出文件列表
+ cls 清除命令窗口中的内容

### npm的介绍
npm(node pakeage manager)是node.js的包管理器,用于node插件管理(安装/卸载/管理依赖);
+ npm安装的命令:  npm install -g -D
+ npm卸载的命令:  npm uninstall -g -D
+ npm更新全部的命令:  npm update -g -D
+ 当前目录已安装的插件: npm list

### 选装cnpm
这是一个完整 npmjs.org 镜像，你可以用此代替官方版本(只读)，同步频率目前为 10分钟 一次以保证尽量与官方服务同步。
+ 命令提示符执行npm install cnpm -g --registry=https://registry.npm.taobao.org
+ 注意：安装完后最好查看其版本号cnpm -v或关闭命令提示符重新打开，安装完直接使用有可能会出现错误,cnpm跟npm用法完全一致，只是在执行命令时将npm改为cnpm（以下操作将以cnpm代替npm）

### 全局安装gulp
全局安装gulp的目的是为了通过它执行gulp任务。
+ 安装命令 cnpm install gulp -g

### 本地安装gulp
本地安装gulp的命令 cnpm install gulp -D

### 本地安装gulp插件
本地安装gulp的命令 cnpm install -D

### 新建pakeage.JSON
pakeage.json文件是基于nodejs中的配置文件,它是存放在项目根目录的普通json文件
+ 新建配置文件的命令 cnpm init

### 运行gulp
命令提示符执行 gulp [任务名称];当执行gulp default 或者是 gulp 时,将会调用default中的所有任务。
