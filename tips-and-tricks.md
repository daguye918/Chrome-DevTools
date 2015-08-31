# 技巧和窍门

## 控制台

### 编写多行命令

当你进入控制台的多行编写模式时，你可以像标准文字编辑器那样使用文本块。`Shitf` + `Enter` 允许你从控制台进入多行模式。

![consolemultiline](./images/tat-consolemultiline.png)

当你编写的 JavaScript 远比单行文字要复杂的时候，这是非常有用的。一但你创建了一个文字编写区域，在命令的最后按 `Enter` 就会开始运行。

![consolerun](./images/tat-consolerun.png)

关于多行控制台支持持久性问题，请阅读[Snippets](https://developer.chrome.com/devtools/docs/authoring-development-workflow#snippets)-该特征可以保存并执行开发工具中可用的特定 JavaScript 片段。

### 检查元素模式的快捷启动方式

`Ctrl` + `Shitf` + `C` 或者 `Cmd` + `Shift` + `C` 将会在检查元素模式中打开开发者工具（或者选择让它获取焦点），这样你就可以立即检查当前页面。同时焦点全部都会返回到该页面上。在 Mac 上，使用 `Cmd` + `Shift` + `C` 也可以达到相同的效果。

![image_10](./images/tat-image_10.png)

[更多：使用控制台 | 开发者工具文档](https://developer.chrome.com/devtools/docs/console)

### 对 console.table 命令的支持

这个命令记录了任何使用列表布局的数据。下面是一些例子，包括如何使用：

```
console.table([{a:1, b:2, c:3}, {a:"foo", b:false, c:undefined}]);
console.table([[1,2,3], [2,3,4]]);

```

![consoleg1](./images/tat-consoleg1.png)

也有另一个 `columns` 可选参数，它会以字符串数组的形式展示。下面，我们定义了一个 family 对象，其中包含很多 “Person”，之后选择一行来显示：

```
function Person(firstName, lastName, age) {
  this.firstName = firstName;
  this.lastName = lastName;
  this.age = age;
}

var family = {};
family.mother = new Person("Susan", "Doyle", 32);
family.father = new Person("John", "Doyle", 33);
family.daughter = new Person("Lily", "Doyle", 5);
family.son = new Person("Mike", "Doyle", 8);

console.table(family, ["firstName", "lastName", "age"]);

```

![consoleperson](./images/tat-consoleperson.png)

同时，如果你仅仅是想输出这些数据中的前两行，使用：

```
console.table(family, ["firstName", "lastName"]);
```

[更多:对 console.table 命令的支持已经上线 | G+](https://plus.google.com/+AddyOsmani/posts/PmTC5wwJVEc)

### 预览控制台日志对象

日志输出的对象可以使用 console.log() 方法直接在开发工具中预览，而不需要更多的操作。

![image_12](./images/tat-image_12.png)

### 传递多个参数来指定控制台日志样式

就像我们之前在文档中说过的，你可以使用 %c 给你的控制台添加样式，就像你在 Firebug 中一样。比如：

```
console.log("%cBlue!", "color: blue;");

```

同样也支持多种样式:

```
console.log('%cBlue! %cRed!', 'color: blue;', 'color: red;');

```

![image_13](./images/tat-image_13.png)

[更多：在开发者工具上让日志有自己的风格 | G+](https://plus.google.com/+AddyOsmani/posts/TanDFKEN9Kn)

### 清理控制台历史的快捷键

打开控制台，你可以通过 `Ctrl` + `L` 或者 `Cmd` + `L` [快捷键](https://developer.chrome.com/devtools/docs/shortcuts) 来快速的清理控制台历史.控制台中的 console.clear() 命令通过 JavaScript 的控制台 API 来完成清除工作，就和 shell 下的 clear() 一样。

### 成为一个键盘忍者

在开发者工具上，你可以使用 `?` 来打开通用设置，从那里你可以定位到快捷键面板来查看所有[支持的快捷键](https://developer.chrome.com/devtools/docs/shortcuts)

![image_14](./images/tat-image_14.png)

### 通过控制台使用元素

选择一个元素然后在控制台中输出 $0，它将会使用脚本来执行。如果在这个页面上已经有 jQuery 对象，你可以使用 $($0) 来重新选择这个页面上的元素。

![image_15](./images/tat-image_15.png)

你也可以在任何一个元素上右键然后点击 `Reveal in Elements Panel`，这样就可以在DOM 中找到它。

![image_16](./images/tat-image_16.png)

### 通过 XPath 表达式查询 DOM

XPath 是一个在文档中选择节点的查询语言，一般来说返回一个节点的集合，字符串，boolean,或者数字。你可以在 Javascript 开发者工具控制台中使用 XPath 表达式来查询 DOM。

$x(xpath) 命令允许你执行一个脚本。下面的例子将会展示如何通过 $x('//img') 来搜索图片：

![image_17](./images/tat-image_17.png)

然而，该函数同样能够接受第二个参数，该参数是关于路径上下文的，比如：$x(xpath,context)。这就允许我们选择一个详细的上下文（也就是一个内嵌帧）然后使用 XPath 来查询。

```
var frame = document.getElementsByTagName('iframe')[0].contentWindow.document.body;
$x('//'img, frame);

```

在详细的内嵌帧中查询图片

### 获取控制台最后的结果

使用 $_helper 会允许你获取控制台的最后结果。我们可以用另外一个 XPath 的例子来证明这个：

![image_17a](./images/tat-image_17a.png)

### 使用 console.dir

[console.dir(object)](https://developer.chrome.com/devtools/docs/console-api#consoledirobject) 命令将会以一个可扩展的 JavaScript 对象形式列出所有提供的对象的所有属性。下面的例子展示了 document.body 下的一个表示属性的可扩展对象。

![image_18](./images/tat-image_18.png)

### 在具体的帧中运行 JS 控制台

开发者工具底部是下拉选项，它将根据你当前标签的上下文改变。当你在控制台面板的时候，下拉列表允许你选择一个控制台能够操作的帧上下文。在下拉框中选择你的帧，然后你会马上在右侧找到它。

![image_19](./images/tat-image_19.png)

### 当导航到一个新的页面时停止清理控制台

有时候要跳转到一个新的页面上时，你想保持在控制台上的日志信息。要实现这个，只要在控制台右键，然后选择 "Preserve Log upon Navigation"。当你从当前页面导航到一个不同的页面时，控制台历史信息将不会被清除。

![image_20](./images/tat-image_20.png)

### 使用 console.time() 和 console.timeEnd() 进行标准循环

[console.time()](https://developer.chrome.com/devtools/docs/console-api#consoletimelabel) 用一个特定的标签开启一个新的计时器。当用相同的标签调用 console.timeEnd() 的时候计时器停止，在控制台上会显示两次记录间流逝的时间。在不调用函数的情况下，该方法用于衡量循环或者代码非常有用：

![image_21](./images/tat-image_21.png)

### 使用 **console.profile()** 和 **console.profileEnd()** 来进行配置

打开开发者工具，调用 [console.profile()](https://developer.chrome.com/devtools/docs/console-api#consoleprofilelabel) 来开始一个 Javascript CPU 配置。一般来说一个配置只能标记一个标签，就像下面的 console.("Processing") 一样。要结束这个配置，调用 [console.profileEnd()](https://developer.chrome.com/devtools/docs/console-api#consoleprofileend)。

![image_22](./images/tat-image_22.png)

每一个配置文件运行后都会添加到 [Profiles](https://developer.chrome.com/devtools/docs/profiles) 面板中

![image_23](./images/tat-image_23.png)

同时也会添加到 console.profiles[] 数组中，以供后续的查看：

![image_24](./images/tat-image_24.png)

查看更多有关控制台技巧，请进入[使用控制台](https://developer.chrome.com/devtools/docs/console)。

* 通过[控制台 API](https://developer.chrome.com/devtools/docs/console-api.md)提供的方法来记录程序的诊断信息，比如 **console.log()** 或者是 **console.profile（）**
* [命令行 API](https://developer.chrome.com/devtools/docs/commandline-api)提供的方法,比如选择元素的 $() 命令，或者开启 CPU 配置的 profile() 命令。

<a href="https://developer.chrome.com/devtools/docs/console"><img src="preview_console.png"/></a>

## 时间轴

### 利用时间轴帧模式配置帧

时间轴面板提供了关于加载你的 web 应用时花费时间的预览，比如进入 DOM 事件花费的时间，提交页面布局或者在屏幕渲染元素的花费。它也允许你进入三个单独的方面来查明为什么你的应用会很慢，这三个界面是：时间，帧以及实际内存使用。

![image_0](./images/tat-image_0.png)

时间轴默认情况下并不会显示任何数据。但是通过打开你的 app，然后点击在窗口底部的圆圈 ![recording-off](./images/tat-recording-off.png)，来开启一个 session 的记录。或者使用 `Ctrl` + `E` 或者 `Cmd` + `E` 的快捷键也会开始一个录制的标记。

![image_1](./images/tat-image_1.png)

这个录制按钮将会从灰色变为红色，时间轴也会开始捕获你的 app。在你的 app 中完成几个动作后再次按下按钮来停止录制。

![image_2](./images/tat-image_2.png)

帧模式让你洞察到进行中的任务，你的应用程序会按帧（更新）在屏幕上显示。在这个模式中，阴影的垂直区域标尺对应重新计算的样式，合成等等。每一个垂直长条的透明部分表示空闲时间，至少是在你页面上的空闲时间。

![image_3](./images/tat-image_3.png)

举个例子，你的第一帧需要 15 毫秒，但是执行第二帧需要 30 毫秒。一个常见的情况是帧的刷新率是同步的，所以第二帧将稍微比 15 毫秒多一点去渲染。这里，3 号帧丢失了 “true” 硬件帧并且已经提交给了后面一帧，因此第二帧的时长其实相当于双倍了。

如果你的应用并没有很多的动画在其中，并且在执行输入事件的时候浏览器需要执行大量重复的动作，那么使用帧是个好办法。当你有足够的时间在帧内执行完这样的事件，那么你的应用响应能力会更高，并且将会有良好的用户体验。

![image_4](./images/tat-image_4.png)

当我们设定为 60 fps时，我们有最多 16.66 ms来做点事情。这点时间并不算多，所以让尽可能提升你动画的性能是十分重要的。

[更多：利用时间轴开发工具提升性能|开发者工具文档](https://developer.chrome.com/devtools/docs/timeline)

### 使用警告定位到指定的布局事件

在时间轴中，如果你在记录视图中看见一个黄色的图标，就说明你的一些代码触发了强制/同步布局事件。

你希望避免这些不必要的布局触发器，因为他们能够显著影响到你的页面的性能。

![image_5](./images/tat-image_5.png)

[更多：时间轴警告是一种性能的味道 | G+](https://plus.google.com/+AddyOsmani/posts/A7rYqkMMmW8)

### 通过别人来分享和分析一段时间轴记录

你可以浏览和并且跟其他开发者分享时间轴，这要感谢一个有用的导入/导出插件。使用 `Ctrl` + `E` 或者 `Cmd` + `E` 来开始/结束记录然后在时间轴上右键，选择 Save Timeline data。该菜单还支持重新浏览已经导出的时间轴数据。

![image_6](./images/tat-image_6.png)

### 给时间轴记录做注释

使用 console.timeStamp() 函数可以给你的时间轴记录添加注解。这就帮你把你的 web 中的代码和另外一个窗口或者浏览事件关联在了一起。

![image_7](./images/tat-image_7)

[更多：开发者工具控制台 API-制作时间轴 | 开发者文档](https://developer.chrome.com/devtools/docs/console#marking-the-timeline)

你的应用可以通过调用 console.timeStamp() 函数来对你的时间轴记录进行注释。这就使你可以轻易的将代码和另一个窗口以及浏览事件绑定在一起。在下面的记录中，时间轴被标记为 “Adding Result”。下面来看看通过使用控制台来制作时间轴的例子。

#### FPS 计数器/HUD 展示

real-time FPS 计数器是一个用来视图化帧速和躲闪的工具。该工具可以通过进入设置菜单然后选中 ”Show FPS meter“ 来使用。

![image_8](./images/tat-image_8.png)

当这个工具开始运转，你将会看到在右下角有一个黑色的盒子，同时还有帧的统计数字。该计数器可以在实时编辑中用于诊断你的页面为什么掉帧，而不必在时间轴视图间来回切换。

![image_9](./images/tat-image_9.png)

[更多：使用开发者工具的绘制模式来分析长时间绘制事件 | HTML5Rocks](http://updates.html5rocks.com/2013/02/Profiling-Long-Paint-Times-with-DevTools-Continuous-Painting-Mode)

需要谨记的是如果你只是追踪 FPS 计数器可能会使你没有注意到的断断续续的跳帧现象。在使用 content 的时候一定要注意。如果 FPS 在桌面上的效果与在设备上的效果不一样，这也没有意义。所以要特别的小心在性能上的配置。

更多配置使用时间轴的实用技巧，请跳转到[利用时间轴来进行性能描述](https://developer.chrome.com/devtools/docs/timeline)：

* 一个只要应用运行就会记录并分析所有活动的地方，这是开始调查你的应用性能问题的最好的地方。
* 深入了解帧速，记录中生成的几种类型以及 Chrome 计算页面元素的位置和大小时的布局流程。

<a href="https://developer.chrome.com/devtools/docs/timeline"><img src="preview_timeline.png"/></a>

## 概述

### 通过 `3 snapshot` 技术来查找 Javascript 内存漏洞

1. 打开开发者工具选择概述面板
2. 在你的页面进行一些引起漏洞的操作
3. 生成一个新的堆快照
4. 重复步骤 2 和步骤 3 三次
5. 选择最后的堆快照
6. 将过滤器从”所有对象“改为”快照 1 和 2 之间的对象“
7. 你现在应该已经可以看到漏洞对象的集合。你可以选择其中的一个并在对象保留树中来查看其包含内容的列表，这有助于找到泄露的原因。

![image_25](./images/tat-image_25.png)

![image_26](./images/tat-image_26.png)

[更多：BloatBusters-在 Gmail 中消除内存漏洞](https://docs.google.com/presentation/d/1wUVmf78gG-ra5aOxvTfYdiLkdGaR9OhXRnOlIcEmu2s/pub?start=false&loop=false&delayms=3000&slide=id.g1d65bdf6_0_0)

### 理解堆检测中的节点

红色节点是处于生命周期的，因为他们是分离的 DOM 树中的一部分，并且树中有一个节点被 JavaScript （或者是一个闭包变量，一些属性）引用。

黄色节点表示一个从 DOM 节点，引用的一个对象的属性或者一个数组元素。应该有一系列从 DOM 窗口到元素的属性(比如 window.foo.bar[2].baz)。

![image_27](./images/tat-image_27.jpg)

[更多所：理解堆概述中的节点 | G+](https://plus.google.com/+AddyOsmani/posts/hEMupRLRJSF)

### 理解在 CPU 概述中的时间开销

在 CPU 概述中，”（idel）“，时间是当前标记的。花费在非浏览器中的程序是（”program“）。

![image_28](./images/tat-image_28.png)

### 堆配置视图的更多了解

一个我们经常问的问题：在开发者工具 > Profile > Heap sanpshot 中，Comparison，Dominator，Containment 以及 Summary 视图的区别是什么。这些视图提供了对分析器中数据的更多视角，就像下面一样：

Comparsion 视图通过显示已经被垃圾回收器正确清理的对象来帮助你追踪内存漏洞。通常用于比较某次操作前后的两份（或更多）内存快照。具体内容是通过检查变化区释放的内存和引用计数来确认内存泄漏的存在以及造成泄露的原因。

Dominators 视图用于确认垃圾回收正常工作时出现的本不该存在于对象上的引用（也就是说他们）。

Summary 视图可帮助您在利用构造器名称分组的基础上捕获对象（和它们的内存使用）。这个视图通常对追踪 DOM 漏洞很有帮助。

Containment 视图提供了一个更好的对象构建视图，它帮助我们通过全局的命名空间（也就是窗口）来分析对象，找出是什么是他们一直保持存在。它允许分析程序闭包并从底层深入你的对象。

![image_29](./images/tat-image_29.png)

[更多：驯服独角兽：在谷歌浏览器中对 JavaScript 的内存的简单剖析](http://addyosmani.com/blog/taming-the-unicorn-easing-javascript-memory-profiling-in-devtools/)

更多内存剖析技巧，请参考[内存性能剖析](https://developer.chrome.com/devtools/docs/heap-profiling):

* 该文章会叫你如何使用分析堆内存来找出你的应用中的内存漏洞
* 可以深入查看不同视图的数据 - 包括 Summary 视图，Comparison 视图，Containment 视图以及 Dominator 视图。

<a href="https://developer.chrome.com/devtools/docs/heap-profiling"><img src="preview_memory.png"/></a>

## 源

### 在 DOM 修改器上调试

右键点击一个元素然后选中 “Break on Subtree Modification”:不论什么时候脚本穿过了元素并且修改了他们，调试器都能够自动的运转起来，以便告诉你正在发生什么：

![image_30](./images/tat-image_30.png)

另外值得一提的是，暂停内嵌样式属性的修改，对于调试 DOM 动画非常有用 。

### 追踪未捕获异常

从 Sources 面板中，双击暂停脚本执行按钮![pause-icon](./images/tat-pause-icon.png)会在未捕获异常发生时中断代码执行，并保留调用堆栈和应用程序的当前状态-有些人将之称为紫色暂停。

![image_32](./images/tat-image_32.png)

### 使用 console.log 的条件断点活动

我们知道开发者工具支持条件断点，只需要你在想要的行上点击一下设置一个断点，就跟普通的设置断点一样。

![image_33](./images/tat-image_33.png)

你可以在某一行右键然后选择 "Edit Breakpoint"，然后就出现了一个表达式编辑区域。把你需要的条件写在这里（比如：如果表达式的返回值为真，则断点将会在这里停止）

![image_34](./images/tat-image_34.png)

一个普通的表达式可能是这个样子：x === 5，然而 console.log 声明同样是完全有效的输入。

![image_35](./images/tat-image_35.png)

这个方法十分有效，并且我们也可以轻易的看见在断点上调用的 console.log 语句：

![image_36](./images/tat-image_36.png)

由于 console.log 没有一个真正的返回值，不确定的条件断点不会导致执行被暂停，你的代码将继续运行。这非常像一个通过硬编码来执行 console.log 表达式而不直接修改你的代码。

[更多：JavaScript 断点活动 | randomthink.net](http://www.randomthink.net/blog/2012/11/breakpoint-actions-in-javascript/)

### 格式化 JavaScript

开发者工具支持格式化精简后的 JavaScript 以便阅读。要格式化，你需要：

* 进入 Sources 面板，然后从脚本列表中选择你想要格式化脚本。
* 然后点击在开发者工具底部的格式化按钮![prettyprint-icon](./images/tat-prettyprint-icon.png)(用大括号来标记)
* 你的代码应该已经排版好了

格式化之前：

![image_38](./images/tat-image_38.png)

格式化之后：

![image_39](./images/tat-image_39.png)

### 重点观察一个表达式或者一个变量的值

在一次调试会话中，为了避免重复编写一个你要多次查看的变量或者表达式，你可以把它添加到 “Watch Expression” 列表中。当你修改它们之后可以刷新或者直接运行代码来查看改变后的效果。
![image_40](./images/tat-image_40.png)

### 查看内部属性

假设你定了一个变量，其值为 `s` 并且对它执行下面的操作：

```

s.substring(1, 4)  // returns 'ell'

```

你认为 `s` 是一个字符串么？事实上不一定。它也可能是一个字符串对象的包装。试试看下面的观察表达式：

```

"hello"
Object("hello")

```

第一个是字符串常量，第二个是一个完整的对象。令人困惑是，这两个值几乎是一模一样的。但是第二个有一个真正的属性，你也可以自行设置。

展开属性列表你就会注意到，它为什么不是一个完整的对象：它会有一个内在的属性 **[[PrimitiveValue]]**,这里面存储着字符串原本的值。你并不能通过你的代码来访问这个属性，但是你现在可以通过开发者工具的调试工具来查看它。

[更多： 通过开发者工具学习 Javascript 概念 | GitHub](https://gist.github.com/paulirish/4158604)

### 简化调试 XHRs

从调试器中打开 "XHR 断点"选项，当开始一个 XHR 请求时你可以指定你的代码跳入任何一个 URL (甚至是一个子字符串)。甚至是告诉它加载每一个 XHR 时都中断。

![image_41](./images/tat-image_41.jpg)

### 取消注册在元素上的事件处理器

随着 “Element” 标签的打开，找到在 DOM 树中的元素，然后点击要选择的节点。注意：你也可以通过使用控制台 API 中的 **getEventListener(targetNode)** 来实现。

在右侧，点击展开 “Event Listeners” 选项。在那里你会找到所有注册在元素上的事件监听列表。

![image_42](./images/tat-image_42.png)

### Esc 键显示控制台

当在 Sources 面板中调试的时候，你有时候会希望同时进入控制台。这时你只需要简单的点击下 escape 键就可以打开控制台了。

你可以在这个控制台编写执行 JavaScript 来查看预期效果，但是更好的地方是如果你在一个断点初暂停，已经执行的 JS 将会在当前暂停的上下文中。

![image_43](./images/tat-image_43.png)

### 提升在断点处暂停时的效率

当你的脚本在一个断点处暂停时，会有一些有用的参数供你使用。

![image_44](./images/tat-image_44.png)

你可能会知道通过 “Continue”，“Step Over”,"Step Into" 以及 “Step Out” 来控制代码的执行，但是这些按钮都有键盘快捷键。学习这些会让你的在代码中导航时更加高效。

观察表达式（在侧边栏的右侧）将会将会监视表达式，所以你不必总是跳回控制台（例如 X===Y）。调用堆栈显示了从系统开始运行一直到当前位置时经历过的函数调用。

在 Scope Variables，你可以在任何函数上右键然后使用 “Jump to definition” 来进入定义这个函数的脚本内部。

DOM 断点展示了任何在元素面板中右键一个节点时使用 “Break on” 做出的更改。这对调试监听器是否已经正确的添加到节点上以及当他们被调用时发生了什么很有帮助。

XHR 断点面板也同样十分有用，因为它可以为 XMLHttpRequests 设置断点。通过输入一个你想要查看 URL 子字符串来具体说明断点。

### 在异常中暂停

你可能想在抛出一个异常的时候暂停 JavaScript 的执行，并检查调用栈，范围变量和您的应用程序的状态。

![image_45](./images/tat-image_45.png)

在脚本面板的顶部有一个暂停按钮![pause-gray](./images/tat-pause-gray.png),它可以让你选择不同的异常处理模式。你可能不想暂停所有的异常![pause-blue](./images/tat-pause-blue.png)，除非你正在调试的代码是被 try/catch 包裹着的。

### 全部脚本文本上的搜索

如果你想在所有加载在一个页面上的文件中查找一个指定的字符串，你可以通过下面的快捷键调用搜索面板：

* `Ctr` + `Shift` + `F`（Windows,Linux）
* `Cmd` + `Opt` + `F`（Mac OSX）

这个搜索同时支持正则表达式和区分大小写。

![image_50](./images/tat-image_50.png)

### 通过开发者工具和源映射调试 CoffeeScript

源映射提供了一个语言无关的方法来将编译过的工程代码映射到你原来的开发环境中编写的源代码。

当分析产品代码的时候，代码通常已经被缩小过（以防一个语言被翻译成编译过的 JavaScript），这就使你很难找到哪一行代码是映射到你原本的代码中的。

在编译阶段，源映射（source map）可以保存这个信息以允许你调试产品代码，并且会将你原本文件中的行号返回给你。这使得整个世界都不同了，因为你可以再阅读产品代码的同时进行调试了，不管它是在 CoffeeScript 中或是其它分位置 - 只要它具有一个源映射，你就可以轻松调试。

要在 Chrome 中启用源映射：

* 打开 Setting cog > General
* 选择 “Enable source maps”

![image_51](./images/tat-image_51.png)

下面：

* 要将你的 CoffeeScript 编译到 JavaScript，执行这条命令：coffee -c myexample.coffee
* 安装 [CoffeeScript Redux](https://github.com/michaelficarra/CoffeeScriptRedux)
* 创建一个源映射文件 example.js.map ，这个文件应该保存映射信息：**$ coffee-redux/bin/coffee --source-map -i example.coffee > example.js.map**
* 确保生成的 JavaScript 文件，example.js，在最后一行已经有映射到源文件的 url，就像这样：**//# sourceMappingURL=example.js.map**

![image_52](./images/tat-image_52.png)

当你开始调试你的 CoffeeScript 代码的时候，应该感谢这个声明，是它让开发者工具知道了你的源文件在哪里。

然后，您可以利用这个源映射，在您的优化 / 缩小阶段使用类似 UglifyJS2 的工具引用第一个源映射（ CS 到 JS ），并把它所映射的简化后的 JavaScript 文件返回到 CoffeeScript 上，而不是直接传给编译后的 JavaScript 的输出位置。这就允许你直接调试产品代码，并且改动会直接返回到 CoffeeScript 源代码中。

[更多：NetTuts-Source Maps 101](http://code.tutsplus.com/tutorials/source-maps-101--net-29173)

更多有用的创作工作流程技巧，请转到[创作和开发工作流程](https://developer.chrome.com/devtools/docs/authoring-development-workflow):

* 在这里你可以学习如何优化你的开发工作流程以节省一些常规操作所花的时间，比如定位到文件或者某个函数，持续编辑脚本或样式表以及简化调整布局的过程。
* 学习有关新特性的内容，比如 Snippet，该特性可以用于保存并执行开发工具内置的特定的 JavaScripts 片段。

<a href="https://developer.chrome.com/devtools/docs/authoring-development-workflow"><img src="preview_authoring.png"/></a>

## 元素

### 启用尺子

在 Setting > General > Show rulers 下可以启用一个尺子，当你鼠标悬停在某个元素上或者选中一个元素的时候，它会显示出来。

![image_53](./images/tat-image_53.png)

### CSS 属性的自动完成

开发者工具支持 CSS 属性以及值的自动完成（包括那些需要前缀的），这对于决定为当前元素设置什么属性是很有帮助的。

当你开始为属性或者值输出一个名称的时候就会弹出建议，而且你也可以使用右键在可用的属性列表中滚动。要知道，选中的选项会直接应用到页面样式表中因此它的效果是可以直接看到的。

![image_55](./images/tat-image_55.png)

在样式面板中，使用已命名的字段（比如：“red”）,HSL，HEX 或者 RGB 值可以定义颜色。如果需要的话，你可以按住 shift/鼠标点击以在这些值之间迭代选择。

如果你想要展示所有支持的属性，你可以使用 `Ctrl` + `space` 来展示一个建议列表。

![image_56](./images/tat-image_56.png)

建议列表是和特定内容相关的并且在特定情况下（比如，针对字体的时候）数字，已命名或者带前缀的值也是也可以显示出来的。

![image_57](./images/tat-image_57.png)

### 在开发者工具中的颜色选择器

开发者工具中包含了一个内置的颜色选择器，当你点击任何有效颜色的预览方块时，就会显示出来。

![colorpickercanary](./images/tat-colorpickercanary.png)

你可以 `Shift` + 点击，来更改选中颜色的格式。

### 添加新的 CSS 样式

在 CSS 规则的代码块(包括 "element.style")内点击任何地方都可以添加一个新的 CSS 属性，并且该属性会立即应用到当前页面。

![image_60](./images/tat-image_60.png)

一旦你已经成功添加了一个属性，你可以按下 tab 键来设置下一个属性。

点击 ![plus](./images/tat-plus.png) 按钮，新的选择器将会被添加到右边的 Style 子面板中。这样可以定义一个选择器，同样地，你可以用这种方式添加新的属性以及值。

注意：你也可以通过单击一个选择器的名称来编辑 Style 面板中的任何选择器。一旦名称发生改变，选择器已经存在的属性将会被添加到新的选择器定义的元素中。

![image_62](./images/tat-image_62.png)

新的伪类选择器可以通过一种类似的方式来添加，就是将他们加入到选择器的名称之后。同样需要注意的是点击新建选择器按钮旁边的 “toggle element states” ![attributes-icon](./images/tat-attributes-icon.png) 按钮后，将转换到 "Force element state" 面板中。

![image_64](./images/tat-image_64.png)

返回到 “Matched CSS Rules” 面板中，点击规则后面样式表的链接将会进入 Sources 面板。在该面板中会显示完整的样式表定义，并且会跳转到相应规则所在的行。

![image_65](./images/tat-image_65.png)

### 在元素面板中拖曳

在元素面板中你可以拖拽一个元素来改变他在父类中的位置，或者将它移动到文档中一个完全不同的地方。

![image_66](./images/tat-image_66.png)

### 强制元素状态

想要强制元素适应某种特定状态？

* 右键一个子元素然后选择 “Inspect Element”
* 在元素面板中右键其父元素，并选择 “Force Element State”
* 可以选择其中一个：active，:hover，：focus，：visited 来强制进入其中一种状态。

![image_67](./images/tat-image_67.png)

### 通过开发者工具编写并调试 Sass

> 注意：要在 Chrome 中编写 Sass 你必须要有 [3.3.0（预览版)](http://sass-lang.com/download.html)版本的 Sass 编译器，这是现在仅有的支持源映射的版本。


调整一个含有预编译的 CSS 样式的文件可以算是一种挑战，因为在开发工具中对 CSS 样式做出的修改并不会返回到 Sass 源文件中。这意味着，当你做出更改后，如果你希望这些改动能够生效，那就必须返回到源文件中通过外部编辑器手动做出更改。

最近 Sass 开发工作流做出了改进，使得这不再是问题。要获取 Sass 支持：

1. 确认你有在开发者工具使用 about:flags 的经验
2. 接下来，进入 Setting cog > Experiment 然后启用 “Sass stylesheet debugging”（注意，这个特性很快将会结束实验阶段）
![stylesheetdebugging](./images/tat-stylesheetdebugging.png)
3. 进入 General menu > Settings > Check 选中 “Enable source maps” 和 “Auto-reload CSS upon Sass save“。
![autoreload](./images/tat-autoreload.png)
你可以将超时为默认值。这取决于 Sass 编译器需要花费多长时间编译，你可能需要调整这个自动重载的延迟。如果有必要你也可以让自动重加载失效，改用手动刷新页面。
4. 导航到你想在 Chrome 上对 Sass 进行调试的工程页面（通过开发者工具打开）
5. 接下来，通过使用下面的标示开启 Sass 编译器（也可以指定一个目标 CSS 编译器）：**sass --watch --sourcemap sass/styles.scss:styles.css**。这将会让 Sass 观察你对 Sass 源文件的更改，然后为每一个生成的 CSS 文件创建源映射文件（.map）。接下来，你看到的就像是在控制台中的一样：
![image_70](./images/tat-image_70.png)
这就证明了 Sass 调试器确实在工作
6. 如果按照预期启动了工作，你可以进入元素面板。首先你将会注意到你的样式的文件名现在显示的是相应的 .scss 源文件，并且源文件中对应的行号也显示出来了。
![image_71](./images/tat-image_71.png)
7. 在这里点击文件名将会直接进入到 Sources 面板中去，并且会高亮显示相应选择器所在的行。现在你就可以再开发工具内调整 Sass 源文件了，并且该内置编辑器支持语法高亮。
![image_72](./images/tat-image_72.jpg)
8. 如果你想要在 Source 面板中编辑一个 Sass 文件，首先需要确保的就是开发工具能够知道相应文件存在于本地文件系统的哪个位置。在编辑器中右键，然后选择 ”Save As“ 可以用当前正在编辑的文件重写原本的文件。由于自动重加载已经开启并且 Sass 已经在后台运行，所以我们做的更改会马上的显示在 Chrome 和开发者编辑器中。
![image_73](./images/tat-image_73.png)

更多有关使用元素和样式的技巧，请进入[编辑样式和 Dom ](https://developer.chrome.com/devtools/docs/dom-and-styles)

* 在这里，你可以学习如何查看页面的实际结构。比如，你可能对一个图片是否有 HTML id 属性很好奇，并且想知道这个属性的值是什么。
* 了解如何观察 DOM 树中的每一个信息，包括检查以及快速编辑 DOM 元素。如果你需要确认页面某个部分的 HTML 片段时你可能会经常访问元素选项卡。

<a href="https://developer.chrome.com/devtools/docs/dom-and-styles"><img src="preview_elements.png"/></a>

## 网络

### 重新发出 XHRs 请求

也许你可能知道，网络面板会展示你的页面上所有的请求，包括 XHRs。在请求上右键点击会显示上下文菜单，之后选择 “Replay XHR”，就可以重新发出 XHRs 请求(POST 或者 GET)

![image_74](./images/tat-image_74.png)

### 清除网络缓存和 cookies

在网络面板的任何地方，右键点击/ 按住 `Ctrl` 键然后点击会弹出菜单，在菜单中选择 Clear Browser Cache / Network Cache。

![image_75](./images/tat-image_75.png)

### 记录一个追踪栈 & 导出 waterfall

* 点击 “record” 捕捉一个多页面痕迹
* 要导出 meta-data 请求：右键然后选择 “Copy Entry as HAR”
* 要导出全部 waterfall：右键然后选择 “Copy All as HAR”

![image_76](./images/tat-image_76.png)

[更多：等等，开发者工具可以做什么？| Igvita.com](https://www.igvita.com/slides/2012/devtools-tips-and-tricks/#1)

### 使用网络时间轴上的 large resource rows 查看更多细节

通过启动在网络面板底部的 “Use large resource rows” 图标，你可以在面板中显示 campact/smaller resource rows 视图中看不到的额外信息。

![image_77](./images/tat-image_77.png)

对比 smaller resource rows 视图：

![image_78](./images/tat-image_78.png)

以及 larger row 的情况：

![image_79](./images/tat-image_79.png)

### 在网络面板上获取更多信息的技巧

**左键点击**网络面板中时间轴列的头部，可以访问更多网络请求的细节。你可以在以下的选择中选择一个：

* 时间轴
 
* 开始时间
 
* 响应时间
 
* 结束时间
 
* 持续时间

* 等待时间

![network-left](./images/tat-network-left.png)

**浏览灰色的文字来深入查看：**

* 每次请求的 HTTP 网络定义是什么？

* 每次请求第一个字节是什么时候？

* 什么才是响应时间最慢的资源？

* 什么是持续时间最短的资源？

在网络面板中的任何一行的头部**右键**，你可以启用或者禁用列。默认情况下有 3 列不会显示：

* Coolies

* Domain

* Set-Cookies

![network-right](./images/tat-network-right.png)

### WebSocket 检查

在网络面板中，你可以使用底部窗口的过滤器来观察 WebSocket 信息帧。

![websocketbar](./images/tat-websocketbar.png)

比如：进入 [Echo](http://www.websocket.org/echo.html) 实例中，在网络面板底部选择 “WebSocket” 过滤器然后点击 “Connect” 按钮。你通过 “Send” 按钮发送的任何信息都可以用 “Frames” 子面板观察到。

![websocketdemo](./images/tat-websocketdemo.png)

绿色表示来自你客户端的信息。WebSocket 的观察十分的有效，它允许你在观察 WebSocket handshake 的同时查看 WebSocket 的独立帧。

[更多：等等，开发者工具可以做什么？ | Igvita.com](https://www.igvita.com/slides/2012/devtools-tips-and-tricks/#1)

[更多：使用开发者工具观察 Websocket | Kaazing](http://blog.kaazing.com/2012/05/09/inspecting-websocket-traffic-with-chrome-developer-tools/)

### 在网络面板中查找和过滤 XHRs

当你在网络面板中观察网络请求时，可以通过键盘上的特殊键来缩小查找范围。使用 `Ctrl` + `F` 或者 `Cmd` + `F` 可以让整个过程更轻松。

在搜索输入框中，输入你要搜索的关键字，那些请求中有文件名/ URL 与之匹配的就会高亮显示。结果显示出来后，你可以使用输入框旁边的上下按钮来选择你需要的那一项。

![image_82](./images/tat-image_82.png)

尽管这很有用，但是如果它能够只显示和你搜索的关键字相匹配的选项的话就会更有用。"Filter" 选项就可以做到这一点，下面请看例子：

![image_83](./images/tat-image_83.png)

[更多：评估网络性能 | 开发者工具文档](https://developer.chrome.com/devtools/docs/network)

### 获取网络堆栈内部状态

"about:net-internals" 页面是一个特殊的 URL，它存放了网络堆内部状态的一个临时视图。这对调试性能和连接问题十分有帮助。这里面包括请求性能的信息，代理设置以及 DNS 缓存。

![image_84](./images/tat-image_84.png)

同样需要注意的是 about:net-internals/#tests 是可以对一个特殊的 URL 进行测试的。

更多计算网络性能的技巧，请前往[评估网络性能](https://developer.chrome.com/devtools/docs/network)

* 在这里可以学习如何在你的应用中深入查看网络选项。包括时间数据详情，HTTP 请求和相应头，cookies，WebSocket 数据以及更多。
* 学习哪个资源开始加载的时间最慢？哪个资源占需要最长的加载时间（持续时间）？谁开启了一个网络请求？等等。

<a href="https://developer.chrome.com/devtools/docs/network"><img src="preview_network.png"></a>

## 设置

### 模仿触摸事件

触摸是一种在电脑上很难测试的输入方式，因为大多数桌面上不支持触摸输入。在移动端上测试则会延长你的开发周期，一旦你做出了改变，你就需要上传到服务器然后切换到设备上测试。

这个问题的一个解决方法是在你的开发机器上模拟一个触摸事件。对单点触摸来说，Chrome 开发者工具支持单个[触摸事件](http://www.w3.org/TR/touch-events/)的模拟，这使得在电脑上调试移动应用变得更加简单。

要开启触控仿真：

1. 打开开发者工具中的 overrides 菜单
2. 滚动然后选中 "Enable touch events"

![image_85](./images/tat-image_85.png)

现在我们可以像标准桌面事件那样调试触控事件，也可以在源面板中设置事件监听断点。

[更多：开发者工具设备模式 | DevTools 文档](https://developer.chrome.com/devtools/docs/device-mode)

### 模拟 UA 字符串 & 设备视图

通常在桌面上启动一个样品然后在你想支持的设备上处理具体移动设备部分会更加容易一些，设备模拟器可以帮助我们使这个过程更加简单。

开发者工具支持包括本地 User Agent 以及尺寸的重载在内的设备仿真。这就使开发者可以在不同的设备和操作系统上调试移动端的显示效果。

![image_86](./images/tat-image_86.png)

现在你可以模拟确切设备的尺寸，比如 Galaxy Nexus 以及 iPhone 等来测试你的查询驱动设计。

[更多：开发者工具的设备模式 | 开发者工具文档](https://developer.chrome.com/devtools/docs/network)

### 模拟地理信息

在一个支持地理信息支持的 HTML5 应用中，调试不同经纬度下的输出是十分有用的。

开发者工具支持重写 navigator.geolocation 的位置信息，也可以模拟一个模拟地理位置。

![image_87](./images/tat-image_87.png)

重写地理位置

1. 进入到[地理信息](http://html5demos.com/geo)实例中。

2. 允许页面使用你的位置。这样可以获取精确位置。

3. 打开在开发者工具中的重写菜单。

4. 选中 ”Override Geolocation“ 然后输入 Lat = 41.4949819，Lat = -0.1461206。

![image_88](./images/tat-image_88.png)


1. 刷新页面。这个例子会使用你重写后的位置信息来定位。

![image_89](./images/tat-image_89.png)

1. 现在选中 "Emulate position unavailable" 选项。

2. 刷新页面。页面就会提示你查找你的位置信息失败。

![image_90](./images/tat-image_90.png)

[更多：开发者工具模拟移动设备 | DevTools Docs](https://developer.chrome.com/devtools/docs/device-mode)

### Dock-to-right 的视图调试

Dock-to-right 模式同样对在一个缩小的视图中预览你页面的表现是很有帮助的。要使用这个：

* 通过长按开发者工具窗口底部的布局选择器图标![layout-button](./images/tat-layout-button.png)来开启 dock-to-right 模式。
* 你现在可以拖拽窗口分配器然后左右拖拽来改变视图的宽度，然后触发你的媒体查询断点。

![image_92](./images/tat-image_92.png)

### 让 JavaScript 失效

点击右下角的设置齿轮，然后在 Setting > General 中启用 ”Disable Javascript“。当开发者工具已经打开并且这个选项也被选中，那么当前页面 JavaScript 脚本就会失效。

![disablejavascript](./images/tat-disablejavascript.png)

如果需要该功能，同样的也可以通过 "-disable-javascript" 命令来启动 Chrome。

## 通用

### 在标签中快速切换

`Cmd` + `]` 和 `Cmd` + `[`(或者 `Ctrl` + `]` 和 `Ctrl` + `[`)快捷键允许你轻松地在开发者工具的不同标签之间切换。使用他们就可以避免手动选择标签。

![image_94](./images/tat-image_94.png)

### 尝试改进后的 dock-to-right

改进后的元素面板和源面板是水平分开放置的，并且，只要你打开了 dock-to-right 模式，你就可以在 Chrome 测试版中体验该特性：

![image_95](./images/tat-image_95.png)

然而，如果你已经有一个非常宽的屏幕并且不想使用这个屏幕，只需要在设置面板中取消选中 ”Split panels vertically when docked to right“ 选项即可。

![toolbaricons](./images/tat-toolbaricons.png)

[更多：3 步获取一个更好的 Dock-to-Right 体验 | G+](https://plus.google.com/+AddyOsmani/posts/8bfFX8BVzTQ)

### 使用 `Disable Cache` 让缓存失效

在设置齿轮下面，你可以启用 `Disable cache` 选项来使磁盘缓存失效。这对开发来说用处是巨大的，但是开发者工具必须是可见并打开的才能实现这个功能。

![disablecache](./images/tat-disablecache.png)

### 检查 Shadow DOM

含有 Shadow DOM 的元素并不会在元素标签中显示。

1. 使 `Show Shadow DOM` 的复选框生效。
2. 重启开发者工具

![image_98](./images/tat-image_98.png)

你可以稍微看看里面的 Shadow DOM。比如，你可以在 HTML 5 块中看一下 Shadow DOM [标题](http://www.html5rocks.com/en/tutorials/webcomponents/shadowdom-201/)。

![image_99](./images/tat-image_99.png)

### 预览所有可检查的页面

如果你发现你自己已经会使用 remote 调试了，你可能想试试 ”about:inspect“，它会展示在 Chrome 中展示所有可检查的标签/扩展插件。点击 ”inspect“ 来选择一个页面然后加载开发工具并且跳转到相应页面。

![image_100](./images/tat-image_100.png)

### 详细观察哪个站点有应用缓存

通过访问 "about:appcache-internals",你可以看到有关应用缓存的信息。这允许你查看当最后做出更改的时候哪些站点是有缓存的，以及他们占用了多少空间。你也可以在这里移除这些缓存：

![image_101](./images/tat-image_101.png)

### 在网络/控制台面板中选择多重过滤器

你可能已经意识到在网络和控制台面板中也是可以使用过滤器的，这允许你基于不同的标准缩小数据的范围。

你可能不知道的是你可以使用快捷键（ `Cmd`/`Ctrl` + 点击）来选择过滤器并将其应用到视图中。下面你可以看到在多个面板键的行为：

![image_102](./images/tat-image_102.png)

### 清除缓存然后硬重载

如果你请求一个硬刷新，在开发者工具打开的情况下点击并按住 Chromes 的刷新按钮。你应该会看见一个下拉菜单，它允许你进行清除缓存和并进行硬重载。这有助节省时间！

注意：这个现在只对 Windows 和 ChromeOS 有用

![image_104](./images/tat-image_104.png)

### 深入理解 Chrome 任务管理器

Chrome 中的任务管理可以让你深入了解任何选项卡对应的 GPU，CPU 以及 JavaScript 内存使用状况，CSS 和脚本缓存使用状况。

按照下面的步骤来打开任务管理：

1. 在浏览器工具栏中点击 Chrome 菜单。
2. 选择工具。
3. 选择任务管理器。
4. 从那里，你可以通过右键点击任何一行来进入扩展视图或者通过右键来结束一个程序。

## 扩展工具

### 利用开发者工具测试 iOS 应用

[PonyDebugger](https://github.com/square/PonyDebugger) 是一个客户端的库同时也是一个使用 Chrome 开发工具来调试应用网络状况以及管理对象上下文的网关服务器。

![image_105](./images/tat-image_105.png)

### JSRunTime：开发者工具检索 JavaScript 对象的拓展

[Andrei Kashcha](https://plus.google.com/114708134049085210473) 编写了一个非常有用的开发者工具扩展插件，它可以在内存中检索可用的 JavaScript 对象并生成相应的图，还可以根据值或者名称来进行匹配。

![image_106](./images/tat-image_106.jpg)

[更多：JSRuntime-获取对象的开发者工具拓展插件](https://plus.google.com/+AddyOsmani/posts/ih85hKCyGve)

## 其他资源

除了上面的提示，也有许多有用关于开发工具不常用功能的外部资源，幻灯片，文章和视频。我们推荐你看：

* [Chrome DevTools Revolutions 2013 (I/O 2013)](https://www.youtube.com/watch?v=x6qe_kVaBpg)
* [Improving Your 2013 Productivity With The Chrome DevTools](https://www.youtube.com/watch?v=kVSo4buDAEE)
* [The DevTools Cheatsheet](http://anti-code.com/devtools-cheatsheet/)
* [Wait DevTools can do that?](https://www.igvita.com/slides/2012/devtools-tips-and-tricks/#1)
* [Chrome DevTools Evolution (I/O 2012)](https://www.youtube.com/watch?v=3pxf3Ju2row)
* [A Re-introduction to the Chrome DevTools (I/O 2011)](http://www.paulirish.com/2011/a-re-introduction-to-the-chrome-developer-tools/)
* [TextMate-like features in Chrome DevTools](http://elijahmanor.com/2012/02/textmate-like-t-t-in-chrome-dev-tools.html)
* [Google Chrome Developer Tools: 12 Tricks to Develop Quicker](https://www.youtube.com/watch?v=nOEw9iiopwI)
* [Become a JavaScript Power User With The DevTools](https://www.youtube.com/watch?v=4mf_yNLlgic)
* [Modern Web Development](http://jtaby.com/blog/2012/04/23/modern-web-development-part-1)

以上内容适用于 [CC-By 3.0 license](http://creativecommons.org/licenses/by/3.0/)