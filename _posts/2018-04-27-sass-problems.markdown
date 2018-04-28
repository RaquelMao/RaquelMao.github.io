---
layout:       post
title:        "sacc webpack配置"
subtitle:     "webpack摸索"
date:         2018-04-11 13:00:00
author:       "Raquel"
header-img:   "img/post-bg-2015.jpg"
header-mask:  0.3
catalog:      true
tags:
    - sass
    - scss
---

在使用 sass 时，写了一个 globals.scss，作为全局的样式，但发现无法导入，出现错误($primary-color 为使用的一个颜色，sass支持)：
```
Module build failed:
undefined
          ^
      Undefined variable: "$primary-color".
      in C:\Users\Raquel\Documents\simple-qa\src\components\item.vue (line 85, column 12)

 @ ./node_modules/vue-style-loader!./node_modules/css-loader?{"sourceMap":true}!./node_modules/vue-loader/lib/style-compiler?{"vue":true,"id":"data-v-403398fa","scoped":false,"hasInlineConfig":false}!./node_modules/sass-loader/lib/loader.js?{"sourceMap":true}!./node_modules/vue-loader/lib/selector.js?type=styles&index=0!./src/components/item.vue 4:14-372 13:3-17:5 14:22-380
 ···
```
解决方法如下：
webpack.base.conf.js:
```
const vueLoaderConfig = require('./vue-loader.conf')
···
module: {
  rules: [
    ...(config.dev.useEslint ? [createLintingRule()] : []),
    {
      test: /\.vue$/,
      loader: 'vue-loader',
      options: vueLoaderConfig
    },
···
```
vue-loader.conf.js:
```
'use strict'
const utils = require('./utils')
const config = require('../config')
const isProduction = process.env.NODE_ENV === 'production'
const sourceMapEnabled = isProduction
  ? config.build.productionSourceMap
  : config.dev.cssSourceMap

module.exports = {
  loaders: utils.cssLoaders({
    sourceMap: sourceMapEnabled,
    extract: isProduction
  }),
  cssSourceMap: sourceMapEnabled,
  cacheBusting: config.dev.cacheBusting,
  transformToRequire: {
    video: ['src', 'poster'],
    source: 'src',
    img: 'src',
    image: 'xlink:href'
  }
}
```
更改为：
```
'use strict'
const utils = require('./utils')
const config = require('../config')
const isProduction = process.env.NODE_ENV === 'production'
const sourceMapEnabled = isProduction
  ? config.build.productionSourceMap
  : config.dev.cssSourceMap

module.exports = {
  loaders: {
    sass: 'vue-style-loader!css-loader!sass-loader?indentedSyntax=1&data=@import "./src//assets/scss/globals"',
    scss: 'vue-style-loader!css-loader!sass-loader?data=@import "./src/assets/scss/globals";',
    i18n: '@kazupon/vue-i18n-loader'
  },
  cssSourceMap: sourceMapEnabled,
  cacheBusting: config.dev.cacheBusting,
  transformToRequire: {
    video: ['src', 'poster'],
    source: 'src',
    img: 'src',
    image: 'xlink:href'
  }
}
```
然后在使用 bourbon 时，遇到了新的问题
```
Module build failed:
var path = require("path");

module.exports = {
  includePaths: [
    path.join(__dirname, "core")
  ]
};

^
      Invalid CSS after "v": expected 1 selector or at-rule, was "var path = require("
      in C:\Users\Raquel\Documents\simple-qa\node_modules\bourbon\index.js (line 1, column 1)
```
最后更改了 import 路径 为 ’@import "~bourbon/core/bourbon"’

然后出现了新的问题
```
No mixin named transition
```
网上的解决方法：“I found no other solution than to downgrade node-sass to 3.3.3.” 然而我并不想尝试降低我的 node-sass 版本
