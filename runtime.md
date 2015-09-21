# 1.1：Runtime

## Contents

1. [Commands](#commands)
	1. [callFunctionOn](#command-callFunctionOn)
	+ [enable](#command-enable)
	+ [evaluate](#command-evaluate)
	+ [getProperties](#command-getProperties)
	+ [releaseObject](#command-releaseObject)
	+ [releaseObjectGroup](#command-releaseObjectGroup)

2. [Notifications](#events)
	1. [executionContextCreated](#event-executionContextCreated)
3. [Types](#types)

	1. [CallArgument](#type-CallArgument)
	+ [ExecutionContextDescription](#type-ExecutionContextDescription)
	+ [ExecutionContextId](#type-ExecutionContextId)
	+ [PropertyDescriptor](#type-PropertyDescriptor)
	+ [RemoteObject](#type-RemoteObject)
	+ [RemoteObjectId](#type-RemoteObjectId)

Runtime 域通过远程测试和镜面对象表示 JavaScript 运行。计算结果返回一个镜面对象表示对象的类别，字符串表示并唯一化标识符。该标示符可用于之后对象的参考。原始对象被保持在内存中，除非它们被显式释放或连同它们的对象组中的其他对象被释放。

<a name="commands"></a>
### Commands
<a name="command-callFunctionOn"></a>
#### Runtime.callFunctionOn
```javascript
request: {
"id": <number>,
"method": "Runtime.callFunctionOn",
"params": {
  "objectId": <RemoteObjectId>,
  "functionDeclaration": <string>,
  "arguments": <array of CallArgument>,
  "returnByValue": <boolean>
}
}
response: {
"id": <number>,
"error": <object>,
"result": {
  "result": <RemoteObject>,
  "wasThrown": <boolean>
}
}
```
在给定对象上调用有指定声明的方法。结果的对象组从目标对象中继承而来。

##### Parameters
***objectId ( [RemoteObjectId](#type-RemoteObjectId) )***
调用方法对象的标示符

***functionDeclaration ( string )***
函数声明

***arguments ( optional array of [CallArgument](#type-CallArgument) )***
调用参数。所有的调用参数必须属于同一个 JavaScript 世界，即目标对象。

***returnByValue ( optional boolean )***
结果是否设为成 JSON 对象来发送

##### Returns
***result ([ RemoteObject ](#type-RemoteObject))***
调用结果

***wasThrown ( optional boolean )***
在计算过程中如果要抛出结果则设为 true

<a name="command-enable"></a>
#### Runtime.enable
```javascript
request: {
"id": <number>,
"method": "Runtime.enable"
}
response: {
"id": <number>,
"error": <object>
}
```
通过<code>executionContextCreated</code>事件启用执行文本创建的报告。当报告被启用，事件会发送到每个存在的执行上下文。


<a name="command-evaluate"></a>
#### Runtime.evaluate
```javascript
request: {
"id": <number>,
"method": "Runtime.evaluate",
"params": {
  "expression": <string>,
  "objectGroup": <string>,
  "contextId": <Runtime.ExecutionContextId>,
  "returnByValue": <boolean>
}
}
response: {
"id": <number>,
"error": <object>,
"result": {
  "result": <RemoteObject>,
  "wasThrown": <boolean>
}
}
```
在一个全局对象上计算表达式


##### Parameters

***expression ( string )***
要计算的表达式

***objectGroup ( optional string )***
可用于释放多个对象符号组名

***contextId ( optional [Runtime.ExecutionContextId](#type-ExecutionContextId) )***
指定在执行计算的相关上下文。每个脚本都存在于一个相关文本，这个参数会被用来指定其中一个上下文本。如果参数被省略或者为 0，计算会在被审查会页面的上下文中执行。

***returnByValue ( optional boolean )***
结果是否被设为一个 JSON 对象来发送

##### Returns
***result ( [RemoteObject](#type-RemoteObject) )***
计算表达式的结果

***wasThrown ( optional boolean )***
在计算过程中若要结果被抛出，设为 true.

<a name="command-getProperties"></a>
#### Runtime.getProperties
```javascript
request: {
"id": <number>,
"method": "Runtime.getProperties",
"params": {
  "objectId": <RemoteObjectId>,
  "ownProperties": <boolean>
}
}
response: {
"id": <number>,
"error": <object>,
"result": {
  "result": <array of PropertyDescriptor>
}
}
```
返回给定对象的属性。返回结果是从目标对象继承而来。

##### Parameters
***objectId ([ RemoteObjectId](#type-RemoteObjectId) )***
要返回属性的对象的标示符（可用：布尔值）

***ownProperties ( optional boolean )***
如果设为 true ，返回只属于元素自身的属性，而不是它的属性链。

##### Returns
*result ( array of [PropertyDescriptor](#type-PropertyDescriptor) )*
对象属性


<a name="command-releaseObject"></a>
#### Runtime.releaseObject
```javascript
request: {
"id": <number>,
"method": "Runtime.releaseObject",
"params": {
  "objectId": <RemoteObjectId>
}
}
response: {
"id": <number>,
"error": <object>
}
```
释放指定 ID 的远程对象

##### Parameters

***objectId ( [RemoteObjectId](#type-RemoteObjectId) )***
要释放对象的标示符

<a name="command-releaseObjectGroup"></a>
#### Runtime.releaseObjectGroup
```javascript
request: {
"id": <number>,
"method": "Runtime.releaseObjectGroup",
"params": {
  "objectGroup": <string>
}
}
response: {
"id": <number>,
"error": <object>
}
```
释放指定组中所有的远程对象

##### Parameters

***objectGroup ( string )***
对象组的标识名称

<a name="events"></a>
### Notifications
<a name="event-executionContextCreated"></a>
#### Runtime.executionContextCreated
```javascript
{
"method": "Runtime.executionContextCreated",
"params": {
  "context": <ExecutionContextDescription>
}
}
```
当一个新的执行文本被创建会进行提示


##### Parameters
***context ( [ExecutionContextDescription](#type-ExecutionContextDescription) )***
新创建的执行文本

<a name="types"></a>
### Types
<a name="type-CallArgument"></a>
#### CallArgument: object
***objectId ( optional [RemoteObjectId ](#type-ExecutionContextId))***
远程对象处理

***value ( optional any )***
原始值
<a name="ype-ExecutionContextDescription"></a>
#### ExecutionContextDescription: object

***frameId ( [Page.FrameId](page.html#type-FrameId) )***
宿主帧的（owning frame）ID

***id ( [ExecutionContextId ](#type-ExecutionContextId))***
执行文本唯一的 ID.它可以用来指定在其中执行上下文中，脚本在哪执行。
<a name="type-ExecutionContextId"></a>
#### ExecutionContextId: integer
<a name="type-PropertyDescriptor"></a>
#### PropertyDescriptor: object

***configurable ( boolean )***
如果这个属性的描述可能被改变或者这个属性可能从响应的对象中被删除，则为 true

***enumerable ( boolean )***
如果在对应对象属性列举时，这个属性出现了，则为 true

***get ( optional [RemoteObject](#type-RemoteObjectId) )***
一个相当于获取对象属性方法的函数，或者未定义如果没有获取函数（只是存取描述符）

***name ( string )***
属性名称

***set ( optional [RemoteObject](#type-RemoteObjectId) )***
一个相当于设置对象属性方法的函数，或者未定义如果没有 setter 函数（只是存取描述符）

***value ( optional [RemoteObject](#type-RemoteObjectId) )***
与这个属性相关连的值

***wasThrown ( optional boolean )***
如果在计算过程中，结果被抛出，则为 true

***writable ( optional boolean )***
如果属性关联的值可能被改变，则设为 true
<a name="type-RemoteObject"></a>
#### RemoteObject: object

***className ( optional string )***
对象类（构造函数）的名称。只是限定对象类型的值。

***description ( optional string )***
代表对象的字符串表示。

***objectId ( optional [RemoteObjectId](#type-RemoteObjectId) )***
对象唯一的标示符（对于没有初始值的）。

***subtype ( optional enumerated string [ "array" , "date" , "node" , "null" , "regexp" ] )***
对象子类型的提示。只是限定对象类型的值。

***type ( enumerated string [ "boolean" , "function" , "number" , "object" , "string" , "undefined" ] )***
对象类型

***value ( optional any )***
远程对象的值（如果被要求，初始化值 或者 JSON 值）
<a name="type-RemoteObjectId"></a>
#### RemoteObjectId: string