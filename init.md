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

[点击这里获取源码](https://github.com/juventusfc/tools-chain-generator-frank)

## 命令行搭建类似 yeoman 的东西

我们在使用三大框架时，经常能看到 bash 中有让你选择的情况。其实，用命令行也能实现这个功能。

### 命令行中显示问题

- 使用 [`readline`](https://nodejs.org/api/readline.html#readline_rl_question_query_callback)

  ```javascript
  const readline = require("readline");

  const rl = readline.createInterface({
    input: process.stdin,
    output: process.stdout,
  });

  async function ask(question) {
    return new Promise((resolve, reject) => {
      rl.question(question, (answer) => {
        resolve(answer);
      });
    });
  }

  void (async function () {
    console.log(await ask("your project name?"));
  })();
  ```

- 使用 `stdout.write` 直接输出

### 命令行中移动光标

使用 `stdout.write` 来移动光标: [Cursor Movement](http://www.tldp.org/HOWTO/Bash-Prompt-HOWTO/x361.html)

```javascript
var tty = require("tty");
var ttys = require("ttys");

var stdin = ttys.stdin;
var stdout = ttys.stdout;

stdout.write("Hello1 World!\n");
stdout.write("\033[1A"); // 光标向上移动一行
stdout.write("winter");
```

### 命令行中进行选择

打印输入的字符：

```javascript
var stdin = process.stdin;
stdin.setRawMode(true);
stdin.resume();
stdin.setEncoding("utf8");

stdin.on("data", function (key) {
  if (key === "\u0003") {
    process.exit();
  }

  process.stdout.write(key.toString().charCodeAt(0).toString());
});
```

[点击这里获取源码](https://github.com/juventusfc/tools-chain-console-tookit)。

## 在代码中使用 `npm`，安装新的依赖

```javascript
/**
 * 代码中实现安装 webpack 包
 * */
const npm = require("npm");

const config = {
  name: "npm-demo",
  version: "1.0.0",
  description: "",
  main: "index.js",
  scripts: {
    test: 'echo "Error: no test specified" && exit 1',
  },
  keywords: [],
  author: "",
  license: "ISC",
  dependencies: {
    npm: "^6.14.7",
  },
};

npm.load(config, (err) => {
  npm.install("webpack", (err) => {
    console.log(err);
  });
});
```
