# publish 阶段的工具

## 搭建 Ubuntu 中的 Node.js 环境

1. 安装 `virtual box` 和 `Ubuntu`
2. 安装 `nvm`
3. 通过 `nvm`安装 `Node.js`

## 搭建一个完整的发布系统

### 搭建 `publish-tool`

`publish-tool`作为内网发布工具，发送 http 请求至 `publish-server`。它以流式形式上传文件。

很多时候我们都会将所有文件放到一个文件夹下，然后通过 `archiver` 包，将该文件夹下所有文件进行压缩传给 `server`。

### 搭建 `publish-server` 和 `publish-server-vanilla`

`publish-server` 主要实现两个功能：

1. 对用户权限进行认证
2. 作为发布服务器，作为内外网之间的桥梁，接收来自内网 `publish-tool` 的请求，更改外网 `server` 上的资源

我们可以执行 `npx express-generator --no-view` 产生模板代码并将默认的端口号更改为 8081。但是要注意，http 是流式传输的，但是 express 默认的处理方式是将流式全部接收完毕后再处理。

所以，我们决定放弃 express，使用原生 http 包搭建一个 `publish-server-vanilla`。

由于从 `publish-tool` 传过来的是压缩包，所以在这里要进行解压缩。然后，以 pipe 的方式将流传给 `server`。

### 搭建 `server`

`server` 作为静态服务器，接受来自 `publish-server` 的请求，将静态文件更改，从而让用户访问最新的资源。

执行 `npx express-generator` 产生模板代码。默认的端口号为 3000。有时候为了省力，可以直接将静态文件放在 public 文件夹下。

### 架构

内网 your computer(`publish tool`) -> 内网 `publish server` 8081 -> 外网 `server` 3000 <- `customer's computer`
