# init 阶段的工具

## 动手比较 `vue-cli`、`create-react-app` 和 `angular-cli`

三大框架都有自己的脚手架来初始化项目。可以分别体验一下三大框架是如何生成项目的。

## yeoman

yeoman 是用于生成脚手架的脚手架。

yeoman 的重点集中在：

- user interactions 使用脚手架时，用户交互的 UI
- managing dependencies 脚手架生成的项目中的依赖
- file system 脚手架生成的项目中的文件

使用 yeoman 搭建一个简单的 frank 脚手架的搭建步骤：

1. 生成一个新的 node 项目，名字为 `generator-frank`。注意，脚手架需要符合 `generator-XXX` 规范；
2. 执行 `npm install yeoman-generator`；
3. 构建代码层级。yeoman 要求代码结构需要满足一定层级；
4. 执行 `npm link`，将项目发布到本地全局；

   > `npm link` 命令可以将一个任意位置的 npm 包链接到全局执行环境，从而在任意位置使用命令行都可以直接运行该 npm 包

   该命令只需执行一次。每次更新代码后，npm 能找到最新的代码。

使用 frank 脚手架步骤：

1. 执行`npm install -g yo`，全局安装 yeoman；
2. 执行 `yo frank`，相当于使用 frank 这个脚手架生成项目。类似于 `create-react-app`。

[点击这里获取源码](##)

## 使用 `ttys` 搭建一个 console 工具，达到用户交互的目的

我们在使用三大框架时，经常能看到 bash 中有让你选择的情况。其实，`ttys` 这个包也能实现这个功能。
[点击这里获取源码](##)

## 在代码中使用 `npm`，生成新的依赖

[点击这里获取源码](##)
