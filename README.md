# LearnES6

个人学习ES6的笔记

### 安装Babel

[查阅](http://babeljs.io/docs/setup/#babel_cli)

#### 安装Babel6 

* 要在命令行中执行安装babel-cli, 要在node项目中执行安装babel-core

````$ npm install --save-dev babel-cli````

* 安装插件

````$ npm install babel-preset-es2015 --save-dev````

 安装完成之后，会在 ``package.json`` 中添加对应信息

#### 使用 

* 在 ``package.json`` 中添加 ``scripts``字段

    "scripts": {
       "build": "babel src -d lib"
     }

 之后便可以直接运行 ``$ npm run build``

* 或者可以直接执行 ``$ babel src -d lib``

* 如果使用webstorm，可以直接在ide中配置

- 配置支持es6
Setting > Languages & Frameworks > JavaScript

- 自动转码为ES5
Setting > Tools > File watchers

#### 创建.babelrc配置文件

````echo { "presets": ["es2015"] } > .babelrc````

