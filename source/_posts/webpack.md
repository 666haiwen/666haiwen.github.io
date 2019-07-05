---
title: 前端引入第三方库
date: 2019-06-18 12:59:57
tags:
categories:
- [frontend]
---

在使用第三方库的情况下，可能会有以下的问题：

```
\src
	index.js
```

我们在*index.js*中使用了*d3*这个库，引入方式是：

```
import * as THREE from 'three';
```

一切没有问题，可以直接使用诸如*THREE.Scene()*等等，但是这个时候你想用第三方的库，例如官方的*THREE.OrbitControls()*，但它并不在*three*库本身当中，这意味着，你不能直接使用*THREE.OrbitControls()*

这个时候，你从官网下载了OrbitControls.js的代码，放在

```
\scr
	index.js
	OrbitControl.js //Add
```

想把它import进来，有以下两种方法。

#### 不用webpack

找到OrbitControls.js

在开头添加如下语句:

```
+ import * as THREE from 'three';

THREE.OrbitControls = function ( object, domElement ) {
...
}
```

接着，在index.js中，增加：

```
import * as THREE from 'three';
+ import './OrbitControls';
```

#### 使用webpack-ProvidePlugin

在webpack的配置文件中添加：

```
const path = require('path');
+ const webpack = require('webpack');

module.exports = {
  ...
+ plugins: [
    new webpack.ProvidePlugin({
      THREE: 'three',
    }),
  ],
};

```

这个新增插件的功能是说，下次再使用THREE的地方，自动加载*three*这个库，同样在*index.js*中增加：

```
import * as THREE from 'three';
+ import './OrbitControls';
```

即可。