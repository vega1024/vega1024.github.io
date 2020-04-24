---
layout:     post                    # 使用的布局（不需要改）
title:      动态规划入门               # 标题 
subtitle:   本文将介绍动态规划基本实现以及LeetCode几道简单的题目 #副标题
date:       2020-04-23              # 时间
author:     Vega                      # 作者
header-img: img/post-bg-2015.jpg    #这篇文章标题背景图片
catalog: true                       # 是否归档
tags:                               #标签
    - Vue.js
---

# 使用Vue CLI Plugin Electron Builder打包Vue Cli3项目

### 前言

本文档只适用于 `windows`下开发，非Ubuntu子系统下，若遇到Ubuntu下创建的项目在windows不能跑，请在windows下创建Vue项目，将代码复制进新项目中。且引入的此插件只适用于Vue Cli3创建的项目

### 安装

在项目位置中，输入

```sh
$ vue add electron-builder
```

### 启动开发环境

如果有yarn：

```sh
$ yarn electron:serve
```

如果使用NPM：

```sh
$ npm run electron:serve
```

### 打包应用

使用yarn

```sh
$ yarn electron:build
```

使用NPM

```sh
$ npm run yarn electron:build
```

### 依赖文件下载失败或下载过慢解决方法

在build过程，会显示下载地址。

#### 1. winCodeSign-2.4.0.7z

   在目录C:\Users\Administrator\AppData\Local\electron-builder\Cache\winCodeSign下，新建文件夹winCodeSign-2.4.0（即报错信息中文件名），将下载文件解压到此文件夹内。

#### 2.  nsis-3.0.3.2

   在目录C:\Users\Administrator\AppData\Local\electron-builder\Cache\nsis下，新建文件夹nsis-3.0.3.2（即报错信息中文件名），将下载文件解压到此文件夹内。

#### 3.  nsis-resources-3.3.0

   在目录C:\Users\Administrator\AppData\Local\electron-builder\Cache\nsis-resources下，新建文件夹nsis-resources-3.3.0（即报错信息中文件名），将下载文件解压到此文件夹内。

#### 最终文件夹如下

```sh
--electron-builder
    --cache
        --nsis
            --nsis-3.0.3.2
                解压nsis-3.0.3.2.7z所得文件
        --nsis-resources
            --nsis-resources-3.3.0
                解压nsis-resources-3.3.0.7z所得文件
        --winCodeSign
            --winCodeSign-2.4.0
                解压winCodeSign-2.4.0.7所得文件
```



### serve环境下正常，build后空白解决方案

当vue-router在history模式下运行时，可能会导致此问题。要解决此问题，请在`mounted`在根Vue组件中添加一个钩子：

```javascript
// src/main.js

new Vue({
  router,
  render: h => h(App),
  mounted() {
    // Prevent blank screen in Electron builds
    this.$router.push('/')
  }
}).$mount('#app')
```

### 请求发不到后端解决方案

在serve环境下，请在`.env.development`中填入后端API的URL

```javascript
VUE_APP_API_URL = 'http://127.0.0.1:8080'
```

在build环境下，请在`.env.production`中填入后端API的URL

```javascript
VUE_APP_API_URL = 'http://127.0.0.1:8080'
```

### 参考

<https://github.com/nklayman/vue-cli-plugin-electron-builder>

