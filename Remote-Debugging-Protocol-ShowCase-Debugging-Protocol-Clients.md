# 展示 Chrome 调试协议客户端实例

有很多浏览器的调试协议的第三方客户端。本节介绍一个示例。

## Bracket

Bracket 是一个基于 Web 的 IDE ，使用 Chrome 调试协议启用调试，实时编辑 HTML / CSS。


![brackets.png](images/ref_brackets.png)

+ [Brackets 网站](http://brackets.io/)。从 [download.brackets.io ](http://download.brackets.io.)下载该客户端。源代码在 [Github ](https://github.com/adobe/brackets)上
+ [blog post from Mark DuBois](http://www.markdubois.info/weblog/2013/03/adobe-brackets-revisited/) 给了 Brackets 工作的总概。

## DevTools App
[DevTools App](https://chrome.google.com/webstore/detail/dev-tools-app/eichfopopofffkbhjgbabdegakcdmpkm) 是一个 Chrome 应用程序，可以让你轻松尝试不同版本的 DevTools。

![devtoolsapp.png](images/ref_devtoolsapp.png)

例如你可以轻松尝试

+ 库中[最新的 DevTools 源代码](http://src.chromium.org/blink/trunk/Source/devtools/front_end/inspector.html)
+ 内置的 DevTools
+ 本地服务器提供的 Devtools

为了使用，你必须这样打开 <code>--remote-debugging-port=9222</code>

从 [Chrome Web Store](https://chrome.google.com/webstore/detail/dev-tools-app/eichfopopofffkbhjgbabdegakcdmpkm) 安装 DevTools Apps 到 Chrome。
源代码托管在 [Github](https://github.com/sandipchitale/DevToolsApp) 上。

## Light Table
Light Table 是一个新的 IDE，需要一个新的方法来安排开发者的工作区。Light Table 目前在 alpha 。它不是开源的，但 alpha 版本现在是免费提供的。


![lighttable.png](images/ref_lighttable.png)

+ 从[官方网站](http://www.lighttable.com/)下载
+ 这篇 Blog 描述了在版0.4.0 的新功能，包括 DevTools 的整合。


## NodeJS

大量模型被开发，使用 Node 脚本的 Chrome 调试器

### chrome-remote-interface (Chrome 远程接口)
[Chrome远程接口模型](https://github.com/cyrus-and/chrome-remote-interface) 包装一个节点式的 JavaScript API 调试协议。

```
npm install -g chrome-remote-interface
```

![chrome-remote.png](images/ref_chrome-remote.png)

[看看哪个 NPM 项目中使用 Chrome 的远程接口](https://www.npmjs.com/browse/depended/chrome-remote-interface)

### crconsole

crconsole 模型为 Chrome 控制台提供了一个命令行接口。 它使用 <code>chrome-remote-interface</code> 模型与 Chrome 调试协议交互。

### automated-chrome-profiling（Chrome 自动化分析）

[一个基础配置，通过 Node.js 自动JS分析]( recipe for automating JS profiling through Node.js)，检查到存活在协议系统的[其他应用程序](https://github.com/paulirish/automated-chrome-profiling/blob/master/readme.md#way-more-is-possible)

### chrome-debug-protocol (Chrome 调试协议)

Chrome 调试协议模型在 Chrome中用 JavaScript 和 TypeScript 创建自动测试自动检测，这很容易实现。

```
npm install -g chrome-debug-protocol
```

## Sublime Text

Sublime Web 监测项目增加了 Chrome 集成调试器到流行的 Sublime Text 编辑器中。你可以通过 Sublime Text 包管理器安装它。

![sublime.png](images/ref_sublime.png)

+ [官方页面](http://sokolovstas.github.io/SublimeWebInspector/)有概述和安装说明
+ 源代码托管在 [Github](https://github.com/sokolovstas/SublimeWebInspector)


## Telemetry
Telemetry 所使用的 Chromium 项目多个测试版本的 Chrome 浏览器，用来测试框架性能。它使用调试协议来远程控制的 Chrome 实例。

+ [介绍Telemetry 在 Chromium.org](http://http://www.chromium.org/developers/telemetry)

## Vim
Chrom.vim 是 Vim 编辑器的一个实验插件，提供了一些基础的 Chrome 操作,适应 Vim 需求。

+ [vim-chrome on Github](https://github.com/mklabs/vimfiles/tree/master/custom-bundle/vim-chrome)


## WebDriver
Selenium 浏览器自动化工具使用 WebDriver API 来抽象与不同的浏览器的交互。Chrome 上 WebDriver 的实现 使用 Chrome 浏览器调试协议。

+ [Selenium WebDriver project](http://docs.seleniumhq.org/projects/webdriver/)

## WebStorm

WebStorm 是一款商业化的 IDE，支持在 Chrome 上调试和在线编辑。WebStorm 使用一个 [Chrome 插件](http://www.jetbrains.com/webstorm/webhelp/using-jetbrains-chrome-extension.html)，集成了 Chrome 调试器。

![webstorm.png](images/ref_webstorm.png)

+ 从 [JetBrains](http://www.jetbrains.com/webstorm/) 下载
+ [最新调试器特性的描述截屏](http://tv.jetbrains.net/videocontent/improved-javascript-debugger-in-webstorm-7)

## Python
[chrome_remote_shell](https://github.com/minektur/chrome_remote_shell) 为 python 应用提供了一个很好的 API 层。
