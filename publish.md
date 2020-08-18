# publish 阶段的工具

## 搭建 Ubuntu 中的 Node.js 环境

1. 安装 `virtual box` 和 `Ubuntu`
2. 执行 `sudo apt install nodejs`

安装步骤可参考 [Ubuntu18.04 Install Node.js Npm](https://www.jianshu.com/p/f3dad64d896a)

## 搭建 `server`

`server` 作为静态服务器，接受来自 `publish-server` 的请求，将静态文件更改，从而让用户访问最新的资源。

执行 `npx express-generator` 产生模板代码。默认的端口号为：3000。

有时候为了省力，可以直接将静态文件放在 public 文件夹下。

## 搭建 `publish-server`

`publish-server` 作为发布服务器，接收来自 `publish-tool` 的请求，将更改结果提交给 `server`。

执行 `npx express-generator --no-view` 产生模板代码。将默认的端口号更改为：8081。

它主要实现两个功能：

1. 对用户权限进行认证
2. 响应 `publish-tool` 的请求，更改 `server` 中的静态文件

https://nodejs.org/docs/latest-v13.x/api/fs.html

## 搭建 `publish-tool`

`publish-tool`作为发布工具，发送 http 请求至 publish-server。

## 架构

your computer(`publish tool`) -> `publish server` -> `server` <- `customer's computer`
