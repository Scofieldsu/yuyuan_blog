---
title: npm 详解
date: 2017-05-14 00:02:58
categories: frontend
tags: [npm]
---


#### npm相关知识
- NPM作为Node的模块管理和发布工具，作用与Ruby的gem、Python的pypl或setuptools、PHP的pear和.Net的Nuget一样。

- 包含文件内容符合规范package.json文件的目录或归档文件。并通过”package-name”@”version”来唯一标识每个包。

#### npm init

命令在当前工作目录下以用户引导的方式创建一个全新的package.json文件。然后通过

npm help json

命令打开帮助文档，并根据实际的项目需求自行初始化package.json的项目即可

dependencies、devDependencies

可选项，用于配置模块的生产环境依赖包和开发环境依赖包。当执行npm install时，npm会根据这两个配置项的值去下载安装相关的依赖包。两者的区别是devDependencies是模块开发过程的依赖包（如：grunt只在开发时有用的模块），并且当其他模块需要依赖当前模块时，当通过npm install “package-name”时会自动下载安装dependencies的包而不会下载devDependencies的包。

<!-- more -->

#### 查看配置

查看部分配置信息——

npm config ls

查看所有配置信息——

npm config ls -l

修改配置信息的三种方式：

1. 直接修改配置文件
修改用户家目录的.npmrc文件（没有则新建一个）；

2. 通过命令修改
npm config set "config" "config-value"

命令；

npm config set registry http://registry.npm.taobao.org/
npm config set proxy http://proxy.com:8081/

3. 通过追加命令
比如–registry=”registry-uri”等命令可选项临时配置。

npm install grunt –registry=http://registry.npm.taobao.org

#### 包的种类
全局包

用作在cli上直接调用，而无法在项目中通过require导入依赖包。如将grunt-cli安装到全局时，则可在cli中输入grunt调用了！

npm install -g grunt-cli

cmd或shell中直接调用

grunt
本地包

用作在项目中通过require导入依赖包，供项目使用。

那么全局和本地的依赖包到底是存放在哪里的呢？通过

npm root -g

和

npm root

可分别查看全局和本地的依赖包下载安装的绝对目录了。

#### 包的搜索

搜索依赖包，

npm search "package-name"

查看依赖包的package.json信息，

npm view "package-name"

另外我们可以单独查看package.json某个配置。

查看包的依赖关系

npm view "package-name" dependencies

查看包的源文件地址

npm view "package-name" repository.url

查看包所依赖的node版本号

npm view "package-name" engines

查看本地包信息

查看当前项目的本地依赖包，

npm list

查看全局依赖包，

npm list -g

查看本地依赖包是否不是最新版

npm outdated "package-name"

#### 安装、卸载、更新包

安装包

本地

npm install "package-name"

全局

npm install -g "package-name"

这样会安装最新版的包，若需要安装特定版本，则

npm install "package-name"@"version"

卸载包

卸载本地

npm uninstall "package-name"

卸载全局

npm uninstall -g "package-name"

更新包

更新本地

npm update "package-name"

更新全局

npm update -g "package-name"
