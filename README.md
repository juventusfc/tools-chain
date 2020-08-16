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
- publish 阶段的工具
  - lint
  - jenkins

## 工具链整合

## 参考资料
