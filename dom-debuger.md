# 1.1: DOMDebugger
## 内容

1. [命令](#commands)
	1. [removeDOMBreakpoint](#command-removeDOMBreakpoint)
	+ [removeEventListenerBreakpoint](#command-removeEventListenerBreakpoint)
	+ [removeXHRBreakpoint](#command-removeXHRBreakpoint)
	+ [setDOMBreakpoint](#command-setDOMBreakpoint)
	+ [setEventListenerBreakpoint](#command-setEventListenerBreakpoint)
	+ [setXHRBreakpoint](#command-setXHRBreakpoint)

2. [类型](#types)
	1. [DOMBreakpointType](#type-DOMBreakpointType)

DOM 调试允许在指定的 DOM 操作符和事件上设置断点。如果在这些操作符上有一些列常规断点，Javascript 会停止执行。

<a name="commands"></a>
### 命令

<a name="command-removeDOMBreakpoint"></a>
#### DOMDebugger.removeDOMBreakpoint
```javascript
request: {
"id": <number>,
"method": "DOMDebugger.removeDOMBreakpoint",
"params": {
  "nodeId": <DOM.NodeId>,
  "type": <DOMBreakpointType>
}
}
response: {
"id": <number>,
"error": <object>
}
```
移除使用 <code>setDOMBreakingpoint</code>方法设置的 DOM 断点。
##### 参数
***nodeId ( [DOM.NodeId ](#type-NodeId))***
移除断点的节点的识别器。

***type ( DOMBreakpointType )***
要移除的断点的类型。

<a name="command-removeEventListenerBreakpoint"></a>
#### DOMDebugger.removeEventListenerBreakpoint
```javascript
request: {
"id": <number>,
"method": "DOMDebugger.removeEventListenerBreakpoint",
"params": {
  "eventName": <string>
}
}
response: {
"id": <number>,
"error": <object>
}
```
移除指定 DOM 时间上的断点。

#####  参数
***eventName ( string )***
事件名

<a name="command-removeXHRBreakpoint"></a>
#### DOMDebugger.removeXHRBreakpoint
```javascript
request: {
"id": <number>,
"method": "DOMDebugger.removeXHRBreakpoint",
"params": {
  "url": <string>
}
}
response: {
"id": <number>,
"error": <object>
}
```
移除 XMLHttpRequest 上的断点。

##### 参数
***url(string)***
源 URL 的子字符串。

<a name="command-setDOMBreakpoint"></a>
#### DOMDebugger.setDOMBreakpoint
```javascript
request: {
"id": <number>,
"method": "DOMDebugger.setDOMBreakpoint",
"params": {
  "nodeId": <DOM.NodeId>,
  "type": <DOMBreakpointType>
}
}
response: {
"id": <number>,
"error": <object>
}
```
在特定的 DOM 操作符上设置断点。

##### 参数
***nodeId ( [DOM.NodeId ](#type-NodeId))***
移除断点的节点的识别器。

***type ( DOMBreakpointType )***
要移除的断点的类型。


<a name="command-setEventListenerBreakpoint"></a>
#### DOMDebugger.setEventListenerBreakpoint
```javascript
request: {
"id": <number>,
"method": "DOMDebugger.setEventListenerBreakpoint",
"params": {
  "eventName": <string>
}
}
response: {
"id": <number>,
"error": <object>
}
```
在指定的 DOM 时间上设置断点。
##### 参数
eventName ( string )
要被停止的 DOM 事件名（任何 DOM 事件都会起作用）


<a name="command-setXHRBreakpoint"></a>
#### DOMDebugger.setXHRBreakpoint
```javascript
request: {
"id": <number>,
"method": "DOMDebugger.setXHRBreakpoint",
"params": {
  "url": <string>
}
}
response: {
"id": <number>,
"error": <object>
}
```

在 XMLHttpRequest 上设置断点。

参数
***url(string)***
源 URL 的子字符串。所有包含有 这个子字符串的 XHR都会立即停止。

<a name="types"></a>
### 类型

<a name="type-DOMBreakpointType"></a>
#### DOMBreakpointType: enumerated string
***[ "attribute-modified" , "node-removed" , "subtree-modified" ]***
