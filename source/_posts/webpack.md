---
title: webpack构建项目
---
webpack是用于JS应用的模块管理工具，webpack会在内部构建依赖图映射整个JS应用所需要的模块，并最终进行打包。
#### 最小系统
用webpack引入lodash构建一个项目。
```shell
npm init -y
npm install webpack webpack-cli --save-dev
```
新建项目后，构建如下的文件结构
```shell
|-dist // 通过wenpack生成main.js
  |-index.html
  |-main.js
|-node_modules
|-src
  |-index.js
|-package.json
|-webpack.config.js
```
./src/index.js
```javascript
import _ from 'lodash'
function component() {
  let ele = document.createElement('div')
  ele.innerHTML = _.join(['Hello','webpack'])
  return ele
}

document.body.appendChild(component())
```
./dist/index.html
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Document</title>
</head>
<body>
  <script src="main.js"></script>
</body>
</html>
```
命令行输入，```npx webpack```，编译生成./dist/main.js。
webpack.config.js的基础配置
```javascript
const path = require('path')

module.exports = {
  entry: './src/index.js',
  output: {
    filename: 'main.js',
    path: path.resolve(__dirname, 'dist')
  }
}const path = require('path')

module.exports = {
  entry: './src/index.js',
  output: {
    filename: 'main.js',
    path: path.resolve(__dirname, 'dist')
  }
}
```
不配置此文件运行```npx webpack```，默认以'./src/index.js'为输入，并最终输出到'./dist/main.js'。配置webpack.config.js按照此文件描述输入输出。
#### 核心概念
webpack的配置文件不是必须的，但是可以通过webpack.config.js高度定制，以满足需求。
核心概念包括：
- Entry
- Output
- Loaders
- Plugins
- Mode
- Browser Compatibility

**Entry**
入口，是webpack构建内部依赖图的起点。webpack会找出入口所需要的模块和库。默认值是```./src/index.js```，可按照如下方法自定义:
```JavaScript
// webpack.config.js
module.exports = {
  entry: './mydir/myentry.js'
}
```
**Output**
输出属性规定了webpack输出打包文件的位置以及文件名称。默认```./dist/main.js```为主文件输出，```./dist```为其他文件输出路径。
可以按照如下方法更改输出配置：
```JavaScript
// webpack.config.js
const path = require('path')

module.exports = {
  entry: './mydir/myentry.js',
  output: {
    path: path.resolve(__dirname, 'dist'),
    filename: 'my-webpack.bundle.js'
  }
}
```