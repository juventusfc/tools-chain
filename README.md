# 工具链设计

本项目脱胎于 winter 的前端训练营课程，希望将前端们常用的工具链做一个串讲。

## 工具链设计各个阶段

- [init 阶段的工具](./init.md)

  - `yeoman`
  - `create-react-app`
  - `vue-cli`
  - `angular-cli`

- dev 阶段的工具

  - Server

    - build

      - `webpack`
      - `babel`
      - `vue-compiler-sfc`
      - `jsx`
      - `postcss`

    - watch

      - `fsevent` 不支持 window
      - `chokidar` 支持 windows

    - mock
    - http

      - `ws`
        - `webpack-dev-server`
      - `wireshark`

  - Client

    - debugger

      - `vscode debugger`
      - `chrome devtool`

    - `sourcemap`

- test 阶段的工具

  - jest
  - mocha

    - [how to config mocha and nyc](./how-to-config-mocha-and-nyc.md)

- [publish 阶段的工具](./publish.md)

  - lint
  - jenkins

一般的，我们会在初始化阶段就将各个阶段的工具集成进工具链中（比如 `create-react-app`）。我在 Github 上传了一个使用 yeoman 搭建的 toytool 脚手架。[点击这里获取源码](https://github.com/juventusfc/tools-chain-generator-toytool)。

yeoman 中制作脚手架的步骤主要有：

1. 生成 `package.json`
2. 安装依赖
3. 复制模板
