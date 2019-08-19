---
title: hexo-usage
date: 2019-08-16 15:36:00
tags:
categories:
---

### Hexo-简单指令

- $ hexo n "博客名称"  => hexo new "博客名称" 
- $ hexo p  => hexo publish
- $ hexo g  => hexo generate  #生成
- $ hexo s  => hexo server  #启动服务预览
- $ hexo d  => hexo deploy  #部署

### Hexo-文章目录

<https://pengloo53.gitbooks.io/hexo/content/chapter2/7%20%E6%B7%BB%E5%8A%A0%E6%96%87%E7%AB%A0%E7%9B%AE%E5%BD%95.html>

### Hexo-数学公式

<https://www.jianshu.com/p/7ab21c7f0674>

### Hexo-图片插入

hexo本质是把markdown转义称为了html.在图片插入的过程中，只要保证图片链接没有问题就可以了.

解决方案有二：

- 公共链接
- 本地路径

#### 公共链接

把图片上传到网上，再用网上的链接就可以了(绝对链接不会随着转义的变化而变化).  

可以用的可以有(图层、github、csdn)等等.

#### 本地路径

把图片保存在本地，让hexo在转义文章的时候，把相关的图片资源也传上去.保证文章和图片的相对链接不变就可以了.  

##### 1.修改_config.yml

```
_config.yml
post_asset_folder: true
```

作用：在*hexo new "new_post"*生成md文件的时候，会生成一个同名的文件夹(该例子中就是*new_post*),我们可以把该md中需要引用的图片放入到此文件夹中，比如加入了图片1.png;2.png，此时直接用相对路径引用就可以了(eg. *\[title](new_post/1.png)*)  

**问题**：自己看md文件没啥问题，因为可以解析链接；但是hexo在解析的时候，会把**new_post**文件夹下的内容和解析出来的**index.html**文件放在**同一目录下**；这样就出现了矛盾；对于**index.html**，其对应的相对链接应该为*\[](1.png)*才对.

**2.安装 "hexo-asset-image"**

该插件的功能就是把markdown中的*\[title](new_post/1.png)*转变为了*\[](1.png)*.  

问题解决.



