# publish 阶段的工具

## 搭建 Ubuntu 中的 Node.js 环境

1. 安装 `virtual box` 和 `Ubuntu`
2. 安装 `nvm`
3. 安装 `Node.js`

## 搭建 `publish-tool`

`publish-tool`作为发布工具，发送 http 请求至 `publish-server`。

`publish-tool` 流式上传文件。很多时候我们都会将所有文件打包上传，所以就要用到 `archiver` 包，将所有文件进行压缩传给 `server`。

## 搭建 `publish-server` 和 `publish-server-vanilla`

`publish-server` 作为发布服务器，接收来自 `publish-tool` 的请求，将更改结果提交给 `server`。

执行 `npx express-generator --no-view` 产生模板代码。将默认的端口号更改为：8081。

它主要实现两个功能：

1. 对用户权限进行认证
2. 响应 `publish-tool` 的请求，更改 `server` 中的静态文件

注意，http 是流式传输的，但是 express 默认的处理方式是将流式全部接收完毕后再处理。所以，我们决定放弃 express，搭建一个 `publish-server-vanilla`。

流式处理中，我们可以采用 pipe 的方式直接将流传给 `server`。

## 搭建 `server`

`server` 作为静态服务器，接受来自 `publish-server` 的请求，将静态文件更改，从而让用户访问最新的资源。

执行 `npx express-generator` 产生模板代码。默认的端口号为：3000。

有时候为了省力，可以直接将静态文件放在 public 文件夹下。

由于从 publish-tool 传过来的是压缩包，所以在这里要进行解压缩。

## 架构

内网 your computer(`publish tool`) -> 内网 `publish server` 8081 -> 外网 `server` 3000 <- `customer's computer`
