---
layout:       post
title:        "发布 npm 包"
subtitle:     "配置"
date:         2019-02-13 13:00:00
author:       "Raquel"
header-img:   "img/post-bg-2015.jpg"
header-mask:  0.3
catalog:      true
tags:
    - npm
    - npm package
    - npm publish
---
#### 解决 git 上版本号过多的问题
**Publish 和 commit
1.修改代码
2.commit
3.publish
4.从代码改动处检出新分支xx-temp 删除旧分支xx 拉去远程分支xx 合并新分支xx-temp到新拉取的分支xx
5.push**

##### 1.创建项目
```
npm init -y
```
在 package.json 中添加代码
```
"bin": {
  "smart-testing": "./bin/smart-testing.js"
}
```
创建 bin 目录和 smart-testing.js 文件
./bin/smart-testing.js:
```
#!/usr/bin/env node
console.log('Hello, world!');
```
通过终端进入到项目的根目录执行 npm link,添加了软链,在命令行中输入 smart-testing 试一下
```
npm link
```
###### 配置 eslint
```
npm i eslint -D
```
初始化 eslint 在项目的根目录下执行 ./node_modules/.bin/eslint --init
1.Use a popular style guide
2.Airbnb
3.Do you use React? 写 n 然后回车.
.eslintrc.js
```
module.exports = {
    "extends": "airbnb-base",
    "parser": 'babel-eslint',
    'rules': {
        'global-require': 0,
        'import/no-unresolved': 0,
        'no-param-reassign': 0,
        'no-shadow': 0,
        'import/extensions': 0,
        'import/newline-after-import': 0,
        'no-multi-assign': 0,
        'no-unused-expressions': ['error', { 'allowTernary': true }],
        // allow debugger during development
        'no-debugger': process.env.NODE_ENV === 'production' ? 2 : 0,
    }
};
```
package.json
```
"scripts": {
    "lint": "eslint ./src",
    "test": "echo \"Error: no test specified\" && exit 1"
  },
```
```
npm run lint
```

###### babel
创建 src 目录, 并添加 index.js a.js 文件, 文件内容如下
```
// index.js
import a from './a';
a.a();

// a.js
export default {
  a() {
    console.log('12345');
  },
};
```
此时执行 node index.js ,顺利打印出 12345
最后改造 bin/smart-testing.js 内容如下:
```
#!/usr/bin/env node
require('../'); // 执行入口文件
```
此时在命令行中执行 smart-testing ,顺利打印出 12345

```
npm install --save-dev babel-cli babel-preset-env
```
```
"build": "npm run lint && babel ./src -d ./lib",
```
创建 .babelrc 文件
```
{
  "presets": ["env"]
}
```

###### git cz
```
npm install -g commitizen
```
```
commitizen init cz-conventional-changelog --save --save-exact
```

##### 2.测试 and 发布
###### 测试
```
如果在项目A中使用组件包B
在B包里：
npm link // 相当于npm install B -g
在A包里：
npm link B // 代码无需修改，package.json中引用B的包会自动指向本地B的打包文件
```
本地测试时版本号不需增加

####### 发布
```
# 版本号从 2.0.0-0 变成 2.0.0-1，就是使预发布版本号加一。
npm version prerelease
```
```
npm publish --tag alpha --access public
```
在0.0.1(第一次提交)的时候会自动产生两个不同的 tag :
0.0.1-----------------alpha
0.0.1-----------------latest

安装测试:
```
npm install @raquelmao/smart-testing@alpha
```
测试完成添加切换tag(第一次提交之后):
```
npm dist-tag add smart-testing@0.0.2 latest
```
安装使用时最好加上@latest:
```
npm install @raquelmao/smart-testing@latest
```

###### 其它
```
// 撤销发布包
npm unpublish @raquelmao/m-promise --force

// 升级补丁版本号
npm version patch

// 升级小版本号
npm version minor

// 升级大版本号
npm version major
```
