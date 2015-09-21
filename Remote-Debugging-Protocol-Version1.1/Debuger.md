# 1.1: Debugger

## Contents

1. [Commands](#commands)
	1. [canSetScriptSource](#command-canSetScriptSource)
	+ [continueToLocation](#command-continueToLocation)
	+ [disable](#command-disable)
	+ [enable](#command-enable)
	+ [evaluateOnCallFrame](#command-evaluateOnCallFram)
	+ [getScriptSource](#command-getScriptSource)
	+ [pause](#command-pause)
	+ [removeBreakpoint](#command-removeBreakpoint)
	+ [resume](#command-resume)
	+ [searchInContent](#command-searchInContent)
	+ [setBreakpoint](#command-setBreakpoint)
	+ [setBreakpointByUrl](#command-setBreakpointByUrl)
	+ [setBreakpointsActive](#command-setBreakpointsActive)
	+ [setPauseOnExceptions](#command-setPauseOnExceptions)
	+ [setScriptSource](#command-setScriptSource)
	+ [stepInto](#command-stepInto)
	+ [stepOut](#command-stepOut)
	+ [stepOver](#command-stepOver)


2. [Notifications](#events)

	1. [breakpointResolved](#event-breakpointResolved)
	+ [globalObjectCleared](#event-globalObjectCleared)
	+ [paused](#event-paused)
	+ [resumed](#event-resumed)
	+ [scriptFailedToParse](#event-scriptFailedToParse)
	+ [scriptParsed](#event-scriptParsed)




3. [Types](#types)
	1. [BreakpointId](#type-BreakpointId)
	+ [CallFrame](#type-CallFrame)
	+ [CallFrameId](#type-CallFrameId)
	+ [Location](#type-Location)
	+ [Scope](#type-Scope)
	+ [ScriptId](#type-ScriptId)


调试器域公开暴露了 JavaScript 调试功能。它允许设置与删除断点，逐步执行，探索堆栈跟踪等。

<a name="commands"></a>
### Commands
<a name="command-canSetScriptSource"></a>
#### Debugger.canSetScriptSource

```javascript
request: {
"id": <number>,
"method": "Debugger.canSetScriptSource"
}
response: {
"id": <number>,
"error": <object>,
"result": {
  "result": <boolean>
}
}
```
总是返回 true

##### Returns
***result ( boolean )***
如果 <code>setScriptSource</code>被支持，返回 true.


<a name="command-continueToLocation"></a>
#### Debugger.continueToLocation

```javascript
request: {
"id": <number>,
"method": "Debugger.continueToLocation",
"params": {
  "location": <Location>
}
}
response: {
"id": <number>,
"error": <object>
}

```
连续执行到指定的地方

##### Parameters
***location ( Location )***
继续执行的地方

<a name="command-disable"></a>
#### Debugger.disable
```javascript
request: {
"id": <number>,
"method": "Debugger.disable"
}
response: {
"id": <number>,
"error": <object>
}
```
使被给定页面的调试器失效。


<a name="command-enable"></a>
#### Debugger.enable

```javascript
request: {
"id": <number>,
"method": "Debugger.enable"
}
response: {
"id": <number>,
"error": <object>
}
```
启用给定页面的调试器。直到这条命令被执行，用户端才会认为调试功能被启用。

<a name="command-evaluateOnCallFram"></a>
#### Debugger.evaluateOnCallFrame
```javascript
request: {
"id": <number>,
"method": "Debugger.evaluateOnCallFrame",
"params": {
  "callFrameId": <CallFrameId>,
  "expression": <string>,
  "objectGroup": <string>,
  "returnByValue": <boolean>
}
}
response: {
"id": <number>,
"error": <object>,
"result": {
  "result": <Runtime.RemoteObject>,
  "wasThrown": <boolean>
}
}
```
计算给定调用框架的上的表达式。

##### Parameters
***callFrameId ( CallFrameId )***
调用框架识别器来计算框架

***expression ( string )***
要计算的表达式

***objectGroup ( optional string )***
输出结果到字符串对象组的名字。（使用 releaseObjectGroup 能够快速释放结果对象）

***returnByValue ( optional boolean )***
发送结果的值是否被设为 JSON 对象。

##### Returns
***result ( [Runtime.RemoteObject ](#type-RemoteObject))***
计算结果的对象包装

***wasThrown ( optional boolean )***
如果在计算过程中抛出异常，则返回为真



<a name="command-getScriptSource"></a>
#### Debugger.getScriptSource
```javascript
request: {
"id": <number>,
"method": "Debugger.getScriptSource",
"params": {
  "scriptId": <ScriptId>
}
}
response: {
"id": <number>,
"error": <object>,
"result": {
  "scriptSource": <string>
}
}
```
使用给定的 ID 返回脚本的源。

##### Parameters
***scriptId ( ScriptId )***
获取源的脚本 ID

##### Returns
***scriptSource ( string )***
Script source.

<a name="command-pause"></a>
#### Debugger.pause
```javascript
request: {
"id": <number>,
"method": "Debugger.pause"
}
response: {
"id": <number>,
"error": <object>
}
```
在下一个 JavaScript 语句中停止。

#### Debugger.removeBreakpoint
```javascript
request: {
"id": <number>,
"method": "Debugger.removeBreakpoint",
"params": {
  "breakpointId": <BreakpointId>
}
}
response: {
"id": <number>,
"error": <object>
}

```
移除 JavaScript 对象上的断点

<a name="command-removeBreakpoint"></a>
##### Parameters
***breakpointId ( [BreakpointId](#type-BreakpointId) )***


<a name="command-resume"></a>
#### Debugger.resume
```javascript
request: {
"id": <number>,
"method": "Debugger.resume"
}
response: {
"id": <number>,
"error": <object>
}
```
恢复 JavaScript 的执行


<a name="command-searchInContent"></a>
#### Debugger.searchInContent
```javascript
request: {
"id": <number>,
"method": "Debugger.searchInContent",
"params": {
  "scriptId": <ScriptId>,
  "query": <string>,
  "caseSensitive": <boolean>,
  "isRegex": <boolean>
}
}
response: {
"id": <number>,
"error": <object>,
"result": {
  "result": <array of Page.SearchMatch>
}
}
```
在脚本内容中搜寻给定字符串

##### Parameters
***scriptId ( [ScriptId](#type-ScriptId) )***
要搜寻的主体脚本的 ID

***query ( string )***
要搜寻的字符串

***caseSensitive ( optional boolean )***
如果设为 true ，本次搜寻是区分大小写的。

***isRegex ( optional boolean )***
如果设为 true ，把字符串参数当作正则表达式。

##### Returns

***result ( array of [Page.SearchMatch](page.html#type-SearchMatch) )***
搜寻匹配到结果的列表


<a name="command-setBreakpoint"></a>
#### Debugger.setBreakpoint
```javascript
request: {
"id": <number>,
"method": "Debugger.setBreakpoint",
"params": {
  "location": <Location>,
  "condition": <string>
}
}
response: {
"id": <number>,
"error": <object>,
"result": {
  "breakpointId": <BreakpointId>,
  "actualLocation": <Location>
}
}
```
将 JavaScript 断点设在指定的地方

##### Parameters
***location ( [Location ](#type-Location))***
断点设置的位置

***condition ( optional string )***
用作设定断点条件的表达式。当被指定，编译器只会在断点处停滞，如果表达式的结果为 true.

##### Returns
***breakpointId ( [BreakpointId](#type-BreakpointId) )***
未来参考的断点的 ID

***actualLocation ( [Location](#type-Location) )***
断点归结的位置

<a name="command-setBreakpointByUrl"></a>
#### Debugger.setBreakpointByUrl

```javascript
request: {
"id": <number>,
"method": "Debugger.setBreakpointByUrl",
"params": {
  "lineNumber": <integer>,
  "url": <string>,
  "urlRegex": <string>,
  "columnNumber": <integer>,
  "condition": <string>
}
}
response: {
"id": <number>,
"error": <object>,
"result": {
  "breakpointId": <BreakpointId>,
  "locations": <array of Location>
}
}
```
通过 URL 或 URL 指定正则表达式，在指定的地方设置断点。一旦这个命令被执行，所有现有的解析脚本都将断点解决并返回在指定的位置。进一步匹配脚本解析将导致后续 breakpointResolved 事件发生。这个逻辑断点将使页面重新加载。


##### Parameters
***lineNumber ( integer )***
断点设置位置的行数

***url ( optional string )***
断点设置源的 URL

***urlRegex ( optional string )***
匹配断点设置源 URL 的正则表达式。URL 和 urlRegex 都必须被指定。

***columnNumber ( optional integer )***
设置断点行数的偏移量

***condition ( optional string )***
用来描述断点条件的表达式。当被指定，编译器只会停止断点如果表达式返回为true.

##### Returns

***breakpointId ( [BreakpointId](type-BreakpointId) )***
未来作参考的断点的 ID.

***locations ( array of [Location](#type-Location) )***
断点设置位置的列表。

<a name="command-setBreakpointsActive"></a>
#### Debugger.setBreakpointsActive

```javascript
request: {
"id": <number>,
"method": "Debugger.setBreakpointsActive",
"params": {
  "active": <boolean>
}
}
response: {
"id": <number>,
"error": <object>
}
Activates / deactivates all breakpoints on the page.
```

##### Parameters
***active ( boolean )***
设置断点状态（是否激活）


<a name="command-setPauseOnExceptions"></a>
#### Debugger.setPauseOnExceptions
```javascript
request: {
"id": <number>,
"method": "Debugger.setPauseOnExceptions",
"params": {
  "state": <string>
}
}
response: {
"id": <number>,
"error": <object>
}
```
在异常状态设置暂停。可以被设置来停止所有异常，未捕获异常或者没有异常。在异常状态下初始化的没有暂停状态。

##### Parameters
***state ( enumerated string [ "all" , "none" , "uncaught" ] )***
在异常模型上暂停


<a name="command-setScriptSource"></a>
##### Debugger.setScriptSource
```javascript
request: {
"id": <number>,
"method": "Debugger.setScriptSource",
"params": {
  "scriptId": <ScriptId>,
  "scriptSource": <string>
}
}
response: {
"id": <number>,
"error": <object>,
"result": {
  "callFrames": <array of CallFrame>
}
}
```
实时在线编辑 JavaScript 源代码。

##### Parameters

***scriptId ( [ScriptId ](#type-ScriptId))***
编辑脚本的ID

***scriptSource ( string )***
脚本中的新内容

##### Returns
callFrames ( optional array of [CallFrame](#type-CallFrame) )
VM 停止时，编辑产生的栈追踪器。



<a name="command-stepInto"></a>
#### Debugger.stepInto
```javascript
request: {
"id": <number>,
"method": "Debugger.stepInto"
}
response: {
"id": <number>,
"error": <object>
}
```
直接调用函数


<a name="command-stepOut"></a>
#### Debugger.stepOut
```javascript
request: {
"id": <number>,
"method": "Debugger.stepOut"
}
response: {
"id": <number>,
"error": <object>
}
```
跳出函数调用.

<a name="command-stepOver"></a>
#### Debugger.stepOver
```javascript
request: {
"id": <number>,
"method": "Debugger.stepOver"
}
response: {
"id": <number>,
"error": <object>
}
```
跳过语句



<a name="events"></a>
### Notifications


<a name="event-breakpointResolved"></a>
#### Debugger.breakpointResolved
```javascript
{
"method": "Debugger.breakpointResolved",
"params": {
  "breakpointId": <BreakpointId>,
  "location": <Location>
}
}
```
当断点在真正脚本和指定位置遇到，才会被触发。

##### Parameters

***breakpointId ( [BreakpointId](type-BreakpointId) )***
断点独一无二的识别器

***location ( [Location](type-Location) )***
断点的实际位置

<a name="event-globalObjectCleared"></a>
#### Debugger.globalObjectCleared
```javascript
{
"method": "Debugger.globalObjectCleared"
}
```
当全局环境被清除，调试客户机需要重置它的状态才会被调用。在导航和重载时会发生。


<a name="event-paused"></a>
#### Debugger.paused
```javascript
{
"method": "Debugger.paused",
"params": {
  "callFrames": <array of CallFrame>,
  "reason": <string>,
  "data": <object>
}
}
```
当出现虚拟机在断点停止或者异常，或者其他停止标准，才会被触发。

##### Parameters
***callFrames ( array of [CallFrame](#type-CallFrame) )***
虚拟机停止的栈空间的调用

***reason ( enumerated string [ "CSPViolation" , "DOM" , "EventListener" , "XHR" , "assert" , "debugCommand" , "exception" , "other" ] )***
暂停 reason.

***data ( optional object )***
包括断点辅助属性的对象



<a name="event-resumed"></a>
#### Debugger.resumed
```javascript
{
"method": "Debugger.resumed"
}
```
当虚拟机处理异常时才会被触发。


<a name="event-scriptFailedToParse"></a>
#### Debugger.scriptFailedToParse
```javascript
{
"method": "Debugger.scriptFailedToParse",
"params": {
  "url": <string>,
  "scriptSource": <string>,
  "startLine": <integer>,
  "errorLine": <integer>,
  "errorMessage": <string>
}
}
```
当虚拟机停止脚本失败时才会被触发

##### Parameters
***url ( string )***
分析失败的 Url。

***scriptSource ( string )***
分析失败的脚本原文。

***startLine ( integer )***
在资源中换行的脚本


***errorLine ( integer )***
出错误的行。

***errorMessage ( string )***
分析错误信息。



<a name="event-scriptParsed"></a>
#### Debugger.scriptParsed
```javascript
{
"method": "Debugger.scriptParsed",
"params": {
  "scriptId": <ScriptId>,
  "url": <string>,
  "startLine": <integer>,
  "startColumn": <integer>,
  "endLine": <integer>,
  "endColumn": <integer>,
  "isContentScript": <boolean>,
  "sourceMapURL": <string>
}
}
```
当虚拟机暂停了脚本会被触发。这个事件一样会被触发，对于所有已知还有未收集的脚本，但它们启用调试器时。

##### Parameters
***scriptId ( [ScriptId](type-ScriptId) )***
暂停脚本的识别器

***url ( string )***
暂停脚本的 URL 或者名称。

***startLine ( integer )***
在指定 URL 资源的脚本中的行偏移量

***startColumn ( integer )***
在指定 URL 资源的脚本中的列偏移量

***endLine ( integer )***
脚本的最后一行

***endColumn ( integer )***
脚本最后一行的长度

***isContentScript ( optional boolean )***
辨别这个脚本是否是一个用户扩展脚本。

***sourceMapURL ( optional string )***
与脚本有关的源映射的 URL（如果有）



<a name="types"></a>
### Types


<a name="type-BreakpointId"></a>
#### BreakpointId: string


<a name="type-CallFrame"></a>
#### CallFrame: object
***callFrameId ( [CallFrameId](#type-CallFrameId) )***
Call frame 识别器.这个识别器只有当虚拟机被暂停才有用

***functionName ( string )***
在这个 call frame 中被调用的 JavaScript 函数的名称。

***location ( [Location](type-Location) )***
源代码的位置

***scopeChain ( array of[ Scope](type-Scope) )***
这个 call frame 的作用域链

***this ([ Runtime.RemoteObject](runtime.html#type-RemoteObject) )***
call frame 的对象


<a name="type-CallFrameId"></a>
#### CallFrameId: string


<a name="type-Location"></a>
#### Location: object
***columnNumber ( optional integer )***
这个 script 的列号（0开始）

***lineNumber ( integer )***
这个 script 的行号（0开始）

***scriptId ( [ScriptId ](#type-ScriptId))***
在 <code>Debugger.scriptParsed</code>中声明的脚本识别器。


<a name="type-Scope"></a>
#### Scope: object
object ( [Runtime.RemoteObject](runtime.html#type-RemoteObject) )
代表范围的对象。在全局环境范围，它表示一个实实在在的对象。对于剩下的范围，它是人工瞬态对象列举范围变量的属性。


***type ( enumerated string [ "catch" , "closure" , "global" , "local" , "with" ] )***
Scope type.


<a name="type-ScriptId"></a>
#### ScriptId: string