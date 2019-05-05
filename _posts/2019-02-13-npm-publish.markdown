---
layout:       post
title:        "���� npm ��"
subtitle:     "����"
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
#### ��� git �ϰ汾�Ź��������
**Publish �� commit
1.�޸Ĵ���
2.commit
3.publish
4.�Ӵ���Ķ�������·�֧xx-temp ɾ���ɷ�֧xx ��ȥԶ�̷�֧xx �ϲ��·�֧xx-temp������ȡ�ķ�֧xx
5.push**

##### 1.������Ŀ
```
npm init -y
```
�� package.json ����Ӵ���
```
"bin": {
  "smart-testing": "./bin/smart-testing.js"
}
```
���� bin Ŀ¼�� smart-testing.js �ļ�
./bin/smart-testing.js:
```
#!/usr/bin/env node
console.log('Hello, world!');
```
ͨ���ն˽��뵽��Ŀ�ĸ�Ŀ¼ִ�� npm link,���������,�������������� smart-testing ��һ��
```
npm link
```
###### ���� eslint
```
npm i eslint -D
```
��ʼ�� eslint ����Ŀ�ĸ�Ŀ¼��ִ�� ./node_modules/.bin/eslint --init
1.Use a popular style guide
2.Airbnb
3.Do you use React? д n Ȼ��س�.
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
���� src Ŀ¼, ����� index.js a.js �ļ�, �ļ���������
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
��ʱִ�� node index.js ,˳����ӡ�� 12345
������ bin/smart-testing.js ��������:
```
#!/usr/bin/env node
require('../'); // ִ������ļ�
```
��ʱ����������ִ�� smart-testing ,˳����ӡ�� 12345

```
npm install --save-dev babel-cli babel-preset-env
```
```
"build": "npm run lint && babel ./src -d ./lib",
```
���� .babelrc �ļ�
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

##### 2.���� and ����
###### ����
```
�������ĿA��ʹ�������B
��B���
npm link // �൱��npm install B -g
��A���
npm link B // ���������޸ģ�package.json������B�İ����Զ�ָ�򱾵�B�Ĵ���ļ�
```
���ز���ʱ�汾�Ų�������

####### ����
```
# �汾�Ŵ� 2.0.0-0 ��� 2.0.0-1������ʹԤ�����汾�ż�һ��
npm version prerelease
```
```
npm publish --tag alpha --access public
```
��0.0.1(��һ���ύ)��ʱ����Զ�����������ͬ�� tag :
0.0.1-----------------alpha
0.0.1-----------------latest

��װ����:
```
npm install @raquelmao/smart-testing@alpha
```
�����������л�tag(��һ���ύ֮��):
```
npm dist-tag add smart-testing@0.0.2 latest
```
��װʹ��ʱ��ü���@latest:
```
npm install @raquelmao/smart-testing@latest
```

###### ����
```
// ����������
npm unpublish @raquelmao/m-promise --force

// ���������汾��
npm version patch

// ����С�汾��
npm version minor

// ������汾��
npm version major
```
