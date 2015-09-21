# 控制台 API 参考
控制台 API 为 Web 应用程序提供输入信息到控制台、创建 JavaScript 文件和启动调试会话的方法。

## console.assert(expresson,object)
如果指定表达式返回 false，返回结果会随着一个栈跟踪器输入到控制台上。在接下来的示例中，只要当文档中包含的子节点少于 10 个，断言消息才会被输入到控制台。

 ```javascript
 var list =  document.querySelector('#myList');
 console.assert(list.childNodes.length < 10, "List item count is >= 10");
 ```

![assert-failed-list.png](images/ref_assert-failed-list.png)

## console.clear()
清除控制台

```javascript
console.clear();
```

同样在[清除控制台](https://developer.chrome.com/devtools/docs/console.md#clearing-console-history)可见。

但是，如果 Preserve Logs 是开启状态，当一些框架调用 <code>console.clear()</code>时，它不会做任何事，这会让你的调试过程变得更难。"Clear console"在主菜单还是依然起作用的，能清除控制台的信息。


## console.count(label)
这个函数输出 <code>count()</code>在同一行用同一个标签调用的次数。

下面例子中 每次 <code>login()</code> 函数被调用时， <code>count()</code> 也同样被调用。

```javascript
function login(user) {    console.count("Login called");    // login() code...}
```

![count.png](images/ref_count.png)

在这个例子中，<code>count()</code> 在不同的标签里被调用，每次返回结果都是单独增加（不会累加）。

```javascript
function login(user) {    console.count("Login called for user '" +  user + "'");    // login() code...}
```

![count-unique.png](images/ref_count-unique.png)


## console.debug(object [, object, ...])

这种方法是与 <code>console.log()</code> 相同的。

## console.dir(object)

输出指定对象的 JavaScript 的描述. 如果被记录的对象是一个 HTML 元素，那么它的 DOM 对象的属性被输出显示，示例如下：

```javascript
console.dir(document.body);
```

![consoledir-body.png](images/ref_consoledir-body.png)

你也可以在一个 <code>console.log()</code>语句中使用对象制式（%0）来输出一个元素的 JavaScript 属性：

```javascript
console.log("document body: %O", document.body);
```

![consolelog-object-formatter.png](images/ref_consolelog-object-formatter.png)

在 JavaScript 对象上调用 <code>console.dir()</code> 同在相同对象上调用 console.log() 是等效的。他们都以树的形式输出对象的 Javascript 属性。

将它与 <code>console.log()</code>的执行进行对比，<code>console.log()</code>会以 XML 的格式输出元素，输出在 Elements 面板中：

```javascript
console.log(document.body);
```

![consolelog-body.png](images/ref_consolelog-body.png)

## console.dirxml(object)

输出一个指定对象的 XML 形式，它会在 Elements 面板中显示。对于 HTML 元素来讲，调用这个方法同调用 <code>console.log()</code>是等价的。

```javascript
var list = document.querySelector("#myList");console.dirxml();
```

+ <code>%0</code>是 dir 的简写
+ <code>%o</code>是和 dir 一样还是和 dirxnl 一样取决于对象类型(无 DOM 或 DOM)

## console.error(object [, object, ...])

与 [console.log()](https://developer.chrome.com/devtools/docs/console-api#consolelog) 、<code>console.error()</code> 相似，在该方法被调用的地方同样包括一个栈追踪器。

```javascript
function connectToServer() {    var errorCode = 1;    if (errorCode) {        console.error("Error: %s (%i)", "Server is  not responding", 500);    }}connectToServer();
```


![error-server-not-resp.png](images/ref_error-server-not-resp.png)

## console.group(object[, object, ...])

以可选标题项开始一个新的记录组。调用此方法后再调用 <code>console.groupEnd()</code> 后,所有控制台输出输出在同一个视组。

```javascript
console.group("Authenticating user '%s'", user);console.log("User authenticated");console.groupEnd();
```

![log-group-simple.png](images/ref_log-group-simple.png)

你也可以嵌套组：

```javascript
// New group for authentication:console.group("Authenticating user '%s'", user);// later...console.log("User authenticated", user);// A nested group for authorization:console.group("Authorizing user '%s'", user);console.log("User authorized");console.groupEnd();console.groupEnd();
```

![nestedgroup-api.png](images/ref_nestedgroup-api.png)

## console.groupCollapsed(object[, object, ...])

创建一个初始闭合而不是开放的记录组，就像用 <code>console.group()</code>一样

```javascript
console.groupCollapsed("Authenticating user '%s'", user);console.log("User authenticated");console.groupEnd();console.log("A group-less log trace.");
```
![groupcollapsed.png](images/ref_groupcollapsed.png)



## console.groupEnd()

关闭最近用 <code>console.group()</code> 或 <code>console.groupCollapsed()</code>  创建的记录组。见 [console.group()](https://developer.chrome.com/devtools/docs/console-api#consolegroupobject-object) 和 [console.groupCollapsed()](https://developer.chrome.com/devtools/docs/console-api#consolegroupcollapsedobject-object) 的例子。

## console.info(object [, object, ...])

这个方法与 [console.log()](https://developer.chrome.com/devtools/docs/console-api#consolelogobject-object) 是等效的

## console.log(object [, object, ...])

这个方法在控制台输出消息。传递一个或多个对象作为这个方法的参数，每一个对象被单独计算并连接成一个空间分隔的字符串。你传入 <code>log()</code> 的第一个参数,可能包含**格式说明（format specifiers）**。一个标记字符串由百分号（%），接着一个字母，来表示要应用的格式。

DevTools 支持以下格式说明：

| name  | age |
|:-------|:--------------------|
| %s |  字符串格式 |
|%d or %i | 整型格式 |
| %f  | 浮点数格式   |
| %o  | 可扩展的 DOM 元素(在 Elements 面板里)格式  |
| %O |   可扩展的 Javascript 对象格式 |
| %c  |  以你提供的 CSS 样式的格式输出   |

基本的例子：

```javascript
console.log("App started");
```

下面是使用字符串（%s）和整数（%d）格式说明插入所包含的变量 userName 和 userPoints 值的例子：

```javascript
console.log("User %s has %d points", userName, userPoints);
```

![log-format-specifier.png](images/ref_log-format-specifier.png)

下面是一个在相同 DOM 元素中使用元素格式 (%o) 和对象格式 (%0) 的例子：

```javascript
console.log("%o, %O", document.body, document.body);
```


![log-object-element.png](images/ref_log-object-element.png)

下面的示例使用 %c 格式说明上色的输出字符串：

```javascript
console.log("%cUser %s has %d points", "color:orange; background:blue; font-size: 16pt", userName, userPoints);
```


![log-format-styling.png](images/ref_log-format-styling.png)


## console.prifile([label])

当 Chrome DevTools 被打开，用一个可选标签调用这个函数来开启一个 JavaScript CPU 状态分析。为了完成这个分析，调用 <code> console.profileEnd() </code>方法. 每个分析结果都会被添加到 Profiles 选项卡中。

在下面的实例中，CPU 状态分析在一个函数入口开始，从而消耗过多的 CPU 资源，而当函数退出时，状态分析也随之结束。

```javascript
function processPixels() {  console.profile("Processing pixels");  // later, after processing pixels  console.profileEnd();}
```

## console.profileEnd()

只有一个会话进行时，停止当前 CPU 的 JavaScript 分析会话，并且输出结果到 Profiles 面板。

```javascript
console.profileEnd()
```
见 [console.profile()](https://developer.chrome.com/devtools/docs/console-api#consoleprofilelabel) 有更多使用示例。


## console.time(label)

开始一个新的计时器，与标签关联。当 <code>console.timeEnd()</code>被相同的标签调用时，计时器停止计时，在控制台中显示的经过时间。计时器的值精确到亚毫秒级。

```javascript
console.time("Array initialize");var array= new Array(1000000);for (var i = array.length - 1; i >= 0; i--) {    array[i] = new Object();};console.timeEnd("Array initialize");
```


![time-duration.png](images/ref_time-duration.png)

> 注意：传递给 time() 和 timeEnd() 方法的字符串必须与定时器预期的结束返回的值相符。


## console.timeEnd(label)

停止指定标签的计时器，输出经过的时间。

使用实例，见 [console.time()](https://developer.chrome.com/devtools/docs/console-api#consoletimelabel)

## console.timeStamp([label])

这个方法在记录期间增加了一个事件到时间轴。这可以让你直观地在时间戳上关联生成的代码到其他事件上，如屏幕布局和绘制，这些都被自动添加到时间轴上。

使用 console.timeStamp() [标记时间轴](https://developer.chrome.com/devtools/docs/console.md#marking-the-timeline)的。

## console.trace(object)
输出从这个方法被调用的那个点的栈追踪路径，包括在 Javascript 源代码中指向特定行的链接。计数器输出 <code>trace()</code>方法在那个点被调用的次数，如下图屏幕显示的一样。


![console-trace.png](images/ref_console-trace.png)

向 <code>trace</code>中传入参数也是可能的，例如：


![console-trace-args.png](images/ref_console-trace-args.png)


## console.warn(object [, object, ...])

这个方法和 [console.log()](https://developer.chrome.com/devtools/docs/console-api#consolelogobject-object) 很像，但也输出带有黄色警告图标的日志消息。

```javascript
console.warn("User limit reached! (%d)", userPoints);
```

![log-warn.png](images/ref_log-warn.png)

## debugger

全局调试 （debugger) 功能使 Chrome 停止程序的执行，并在它被调用的行启动一个调试会话。它相当于在 Chrome DevTools 的 Sources 选项卡设置 “手动” 断点。

注意：debugger 命令不是控制台对象的方法。

在下面的示例中， 当一个对象的 <code>brightness()</code> 方法被调用 JavaScript 调试器被打开：

```javascript
brightness : function() {    debugger;    var r = Math.floor(this.red*255);    var g = Math.floor(this.green*255);    var b = Math.floor(this.blue*255);    return (r * 77 + g * 150 + b * 29) >> 8;}
```

![debugger.png](images/ref_debugger.png)







