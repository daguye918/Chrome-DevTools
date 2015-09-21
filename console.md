# 1.1：Console
## Contents

1. [Command](#comands)
	1. [clearMessages](#command-clearMessages)
	+  [disable](#command-disable)
	+ [enable](#command-enable)

2. [Notification](#events)
	1. [messageAdded](#event-messageAdded)
	+ [messageRepeatCountUpdated](#event-messageRepeatCountUpdated)
	+ [messagesCleared](#event-messageCleared)
3. [types](#types)
	1. [CallFrame](#type-CallFrame)
	+ [控制台信息（ConsoleMessage）](#type-ConsoleMessage)
	+ [栈追踪器（StackTrace）](#type-StackTrace)


控制台域为 JavaScript 控制台接口定义了方法和时间。控制台收集 [Javascript Console API](http://getfirebug.com/wiki/index.php/Console_API) 产生的信息。为了开启接收控制台的消息，需要用 <code>enable</code> 命令来启用这个域。浏览最终产生的消息集合，这时控制台域没有被启用，当它启用时，使用 <code>message</code>通知器提交这些消息集合。

<a name="comands"></a>
### 命令
<a name="command-clearMessages"></a>
#### Console.clearMessages

```
request: {
"id": <number>,
"method": "Console.clearMessages"
}
response: {
"id": <number>,
"error": <object>
}
```

清除浏览器收集的控制台消息。

<a name="command-disable"></a>
#### Console.disable

```
request: {
"id": <number>,
"method": "Console.disable"
}
response: {
"id": <number>,
"error": <object>
}
```

禁用控制台域，阻止控制台消息被提交到用户端。
<a name="command-enable"></a>
#### Console.enable
```javascript
request: {
"id": <number>,
"method": "Console.enable"
}
response: {
"id": <number>,
"error": <object>
}
```
启用控制台域，通过 <code>messageAdded</code> 通知器发送最近收集的消息到用户端。


<a name="events"></a>
### 消息通知器（Notifications#）

<a name="event-messageAdded"></a>
#### Console.messageAdded
```javascript
{
"method": "Console.messageAdded",
"params": {
  "message": <ConsoleMessage>
}
}
```
当新的控制台消息被添加时提示标记。


##### Parameters（参数）
message ( [ConsoleMessage](#type-ConsoleMessage) )
添加的控制台消息

<a name="event-messageRepeatCountUpdated"></a>
#### Console.messageRepeatCountUpdated
```javascript
{
"method": "Console.messageRepeatCountUpdated",
"params": {
  "count": <integer>
}
}

```
当多个消息字符和之前出现的相同时，提示标记。

##### Parameters（参数）
count ( integer )
新出现的重复数量


<a name="event-messageCleared"></a>
#### Console.messagesCleared
```javascript
{
"method": "Console.messagesCleared"
}
```
当控制台消息被清除时提示作用。这个会发生在 <code>clearMessage</code> 命令后或者页面导航后。

<a name="types"></a>
####  类型（Types）
<a name="type-CallFrame"></a>
#### CallFrame: object
***columnNumber ( integer )***
JavaScript 脚本列数。

***functionName ( string )***
JavaScript 函数名.

***lineNumber ( integer )***
JavaScript 脚本行数.

***scriptId ( string )***
JavaScript 脚本 id.

***url ( string )***
JavaScript 脚本名称或者 url.


<a name="type-ConsoleMessage"></a>
#### ConsoleMessage: object

***column ( optional integer )***
这条消息中资源的栏数

***level ( enumerated string [ "debug" , "error" , "log" , "warning" ] )***
消息严重程度

***line ( optional integer )***
这条消息中资源的行数。


***networkRequestId ( optional Network.RequestId )***
获取与这条消息相关的网络请求。

***parameters ( optional array of Runtime.RemoteObject )***
被制式化消息的消息参数。

***repeatCount ( optional integer )***
重复输出消息。

***source ( enumerated string [ "appcache" , "console-api" , "css" , "deprecation" , "javascript" , "network" , "other" , "rendering" , "security" , "storage" , "xml" ] )***
消息源

***stackTrace ( optional StackTrace )***
 Javascript 断言消息和错误的栈追踪器。

***text ( string )*** 
消息文本

***type ( optional enumerated string [ "assert" , "clear" , "dir" , "dirxml" , "endGroup" , "log" , "profile" , "profileEnd" , "startGroup" , "startGroupCollapsed" , "table" , "timing" , "trace" ] )***
控制台消息类型

***url ( optional string )***
消息的 URL 源


<a name="type-StackTrace"></a>
#### StackTrace: array of [CallFrame](#type-CallFrame)