# Vuepress Blog

## 前言

为了记录一下学习笔记以及遇到的坑，一直想搭建自己的博客，然后了解到[hexo](https://hexo.io/zh-cn/),[wordpress](https://wordpress.com/zh-cn/),[typecho](https://typecho.org/)以及一些有后端数据库的博客(这种要维护服务器以及数据库，小白以及不是很闲的，比如我，一开始就不考虑这种，大佬请随意)，基于种种考虑，就打算选择能够结合gitpages静态博客框架(官方gitpages也有博客框架，但是英文水平要好一点)，后来机缘巧合之下知道了[Vuepress](https://vuepress.vuejs.org/zh/)，俗话说，要想生活过的去，就得带点绿，就很对口味，毫不犹豫地选择了vuepress,当然了以上提到的一些框架都是可以选择的，网络资料也很多。甚至可以完全自己构建一个博客框架。


## 工具

- [Vuepress](https://vuepress.vuejs.org/zh/):个人觉得是一个简约朴素大方的博客框架，而且可以基于[vue](https://v3.cn.vuejs.org/)做自定义主题开发，以及自定义组件开发(我很中意vue，也不知道为什么)
- [git](https://git-scm.com/)
- [node.js](https://nodejs.org/en/):需要10.0以上版本，下一个最新稳定版
- [yarn](http://yarnpkg.top/index.html)：一个依赖包管理工具,没有别人就是好用
- npm:也是包管理工具
- [valine](https://valine.js.org/):后端评论系统,搭配leancloud使用
- [leancloud](https://www.leancloud.cn/):免费的数据托管管理云服务平台
- vscode,typora:个人博客管理




## 模板使用
[我的博客模板地址](https://github.com/LJoson/Vuepress_blog)

[效果](https://ljoson.github.io/)

使用的是一个国人开源的主题[vuepress-theme-reco](https://vuepress-theme-reco.recoluan.com/en/),搭建博客最快的方法就是扒自己喜欢的博客再改成自己的，省事。
### 架构
##需要自己写主题样式的话，在.vuepress/ 下新建theme文件夹，参考如下目录布局
Vuepress_blog
├── deploy.sh	//部署脚本
├── docs
│   ├── about 		//项目模块
│   ├── projects	//项目模块
│   ├── README.md //首页
│   ├── views		//项目模块
│   └── .vuepress	//配置目录
│       ├── components  //自定义组件，自动生成异步组件
│       ├── config		//组件设置
│       ├── config.js	//博客设置
│       ├── dist	//生成资源目录
│       ├── plugins		//外部插件
│       ├── public		//静态资源
│       └── theme	//主题，自定义主题可以参考
│           ├── components		//组件
│           ├── global-components	//全局组件
│           ├── index.js		//入口配置
│           ├── layouts		//布局
│           ├── noopModule.js	//依赖注入
│           ├── package.json	//主题依赖
│           ├── README.md	//主题说明
│           └── styles	//样式
├── package-lock.json
├── package.json //项目依赖
### 使用模板
在项目文件夹下执行命令，加载依赖：yarn install  #npm install
在项目文件夹下执行命令，运行项目：yarn run docs:dev  #npm run docs:dev
待启动成功后打开地址即可：http://localhost:8080/
部署：在git执行 bash deploy.sh


## vuepress快速上手

用文字说明篇幅可太多了，更多看[官方文档](https://v1.vuepress.vuejs.org/zh/guide/)
！！！VuePress 需要 Node.js >= 8.6 

- 创建并进入一个新目录
```
mkdir vuepress-starter && cd vuepress-starter
```
- 使用你喜欢的包管理器进行初始化
```
yarn init # npm init
```
- 将 VuePress 安装为本地依赖
```
yarn add -D vuepress # npm install -D vuepress
```
::: tip  注意 
如果你的现有项目依赖了 webpack 3.x，我们推荐使用 Yarn 而不是 npm 来安装 VuePress。因为在这种情形下，npm 会生成错误的依赖树。 
:::

接下来就可以写博客了。更多配置[官方文档](https://v1.vuepress.vuejs.org/zh/guide/)