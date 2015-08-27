# 整合 DevTools
Chrome DevTools  是可扩展的。因此，如果 DevTools 缺少你需要一个功能，你可以找到一个现有的插件，或者自己写一个扩展程序。或者你也可以将开发者工具功能集成到你的应用程序中。

有两种基本方式使用 DevTools 建立一个自定义的解决方案：

+ DevTools Extension（开发者工具扩展程序）。一个 [Chrome 插件](http://developer.chrome.com/extensions/)，可插入 DevTools 来添加他的功能并扩展其 UI。
+ 调试协议客户端。一个第三方应用，使用 Chrome 的[远程调试协议](https://developer.chrome.com/devtools/docs/debugger-protocol.html)来插入到低版本调试支持的 Chrome 中.



以下各节讨论这两种方法。

## DevTools Chrome 插件
DevTools UI 是一个嵌入在 Chrome 浏览器中的网络应用。DevTools 插件（扩展程序）使用 [Chrome 扩展系统](http://developer.chrome.com/extensions/)来添加功能到 DevTools 中。一个 DevTools 插件可以添加新的面板到 DevTools 中，可以添加新的窗格到 Elements 和 Sources 面板侧边栏，可以检查资源和网络事件，同样也能在被检查的浏览器选项卡中计算 JavaScript 表达式。

如果你想开发一个 DevTools 插件：

+ 如果你之前没有开发过 Chrome 插件，见 [Chrome 插件（扩展程序）全览](http://developer.chrome.com/extensions/overview.html)
+ 具体创建一个 Chrome DevTools 插件，见 [扩展DevTools](http://developer.chrome.com/extensions/devtools.html)

一系列 DevTools 插件的示例，见[ DevTools 插件实例](sample-extensions.md)，这些实例包含了许多可供参考的开源插件。

## 协议调试客户机 ##
许多第三方应用，例如 IDE（集成开发环境），编辑器，持续集成工具和测试框架，可以用 Chrome 调试器来整合，以此来调试代码，实时预览代码，改变 CSS 样式，以及控制浏览器。客户机使用 [Chrome 调试协议](https://developer.chrome.com/devtools/docs/debugger-protocol.html)来与另一个可以跑在同样系统或者远程系统的 Chrome 实例进行通信。

注意： 目前，Chrome 调试协议只支持每个网页中只有一个客户端。所以，你可以使用 DevTools 来检查一个页面，或者使用第三方客户机，但不要同时使用。

有两种方式整合调试协议：

+ 运行在 Chrome 上的应用程序（例如基于 web 的 IDE）可以利用调试器模块 [chrome.debugger](http://developer.chrome.com/extensions/debugger.html) 创建一个 Chrome 扩展程序。 这个模块让插件直接与调试器通信，避开 Devtools UI。更多信息见 [使用调试器扩展程序API](http://developer.chrome.com/extensions/debugger.html)
+ 其他应用程序可以使用无线协议直接接入调试器。这个协议包括通过一个 WebSocket (网络套接字）连接交换 JSON 数据格式的信息。

一些整合的例子，见 [调试协议客户机实例](debugging-clients.md)



