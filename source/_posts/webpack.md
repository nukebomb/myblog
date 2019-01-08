####  webpack构建项目
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