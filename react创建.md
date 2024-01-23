## 创建项目

```bash
npx create-react-app react-demo
```

使用vite创建项目

```shell
 npm create vite my-react-app
```

## 部分插件安装

安装prettier

```shell
npm i -D prettier eslint-config-prettier eslint-plugin-prettier
```

安装路由

```shell
 npm i react-router-dom  
```

 安装 redux

```shell
 npm i @reduxjs/toolkit react-redux  
```



## 项目配置根目录别名

1）安装craco

```shell
 npm i -D craco
```

2）在根目录下新建craco.config,js

```javascript
const path = require("path");

//配置根目录别名
module.exports = {
  webpack: {
    alias: {
      "@": path.resolve(__dirname, "src"),
    },
  },
};
```

3） 新建jsconfig.json

```json
{
  "compilerOptions": {
    "baseUrl": "./",
    "paths": {
      "@/*": [
        "src/*"
      ]
    }
  }
}
```

4）修改package.json中运行脚本

```json
  "scripts": {
    "start": "craco start",
    "build": "craco build",
    "test": "craco test",
    "eject": "react-scripts eject"
  },
```

