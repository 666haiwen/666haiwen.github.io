---
title: Npm&&package.json&&package-lock.json&&yarn
date: 2019-06-15 13:28:55
tags:
categories:
- [frontend]
---

### Npm

淘宝镜像cnpm:

 npm install -g cnpm --registry=https://registry.npm.taobao.org

### Package

packages中申明了需要下载的依赖包和其对应的版本。

其中，版本号的申明有多种规则，即不同的语义内容，具体如下：

```
 "devDependencies": {
    "@babel/core": "^7.4.4", // >=v7.4.4 but <v8
    "@babel/preset-env": "~7.4.4", // >=v7.4.4 but <v7.5
    "@babel/preset-react": "7.0.0", // ==v7.0.0
    "qux" : "<1.0.0 || >=2.3.1 <2.4.5 || >=2.5.2 <3.0.0", 
    "asd" : "http://asdf.com/asdf.tar.gz", // 指定包地址
    "thr" : "*",  // 任意版本
    "thr2": "", // 任意版本
    "lat" : "latest", // 当前最新
    "dyl" : "file:../dyl", // 本地地址
    "xyz" : "git+ssh://git@github.com:npm/npm.git#v1.0.27", // git 地址
    ...
  }
```



更新一个包和对应的package内容:

package.json中的内容会自动更新（npm >=v5.0)

```
npm update <package.name>
```



### Package-lock

Package中相同的语义规则下，安装的可能是不同版本的package，这可能会造成一些问题。然后npm更新了一个版本(v5.0)，至此之后，会多出一个package-lock.json，显示了安装的真正版本。

那么出现一个问题，package和package-lock安装的内容可能还是不一样的,因为lock文件只是显示了具体安装的版本，而package语义规则下的版本可能与lock版本不同，所以，需要以其中一个为主才行。

如果package-lock下的版本符合package的语义规则，那么就按照lock所记录的版本。

如果package-lock不符合package的语义规则*(例如我更新了package中的一个包依赖)*，那么按照package所记录的版本，同时更新package-lock文件。

### [Yarn](<https://yarnpkg.com/zh-Hant/>)

同样是对package进行包管理，但是并行下载更快，也更方便一些。

使用指令和npm差不太多.

安装：

```
npm install -g yarn
```

淘宝镜像:

```
yarn config set registry https://registry.npm.taobao.org
```

常用命令

```
- npm install === yarn
- npm install <package-name> --save  === yarn add <package-name>
- npm uninstall <package-name> --save  === yarn remove <package-name>
- npm install <package-name> --save-dev  === yarn add <package-name> --dev
- npm update --save === yarn upgrade

- npm install taco@latest --save === yarn add taco
- npm install taco --global === yarn global add taco
- npm init === yarn init
- npm init --yes/-y === yarn init --yes/-y
- npm link === yarn link
- npm outdated === yarn outdated
- npm publish === yarn publish
- npm run === yarn run
- npm cache clean === yarn cache clean
- npm login === yarn login
- npm test === yarn test
```

