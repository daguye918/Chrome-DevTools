# 1.1: DOM

## Contents
1. [Commands](#commands)
	1. [getAttributes](#command-getAttributes)
	+ [getDocument](#command-getDocument)
	+ [getOuterHTML](#command-getOuterHTML)
	+ [hideHighlight](#command-hideHighlight)
	+ [highlightNode](#command-highlightNode)
	+ [highlightRect](#command-highlightRect)
	+ [moveTo](#command-moveTo)
	+ [querySelector](#command-querySelector)
	+ [querySelectorAll](#command-querySelectorAll)
	+ [removeAttribute](#command-removeAttribute)
	+ [removeNode](#command-removeNode)
	+ [requestChildNodes](#command-requestChildNodes)
	+ [requestNode](#command-requestNode)
	+ [resolveNode](#command-resolveNode)
	+ [setAttributeValue](#command-setAttributeValue)
	+ [setAttributesAsText](#command-setAttributesAsText)
	+ [setNodeName](#command-setNodeName)
	+ [setNodeValue](#command-setNodeValue)
	+ [setOuterHTML](#command-setOuterHTML)

2. [Notifications](#events)
	1. [attributeModified](#event-attributeModified)
	+ [attributeRemoved](#event-attributeRemoved)
	+ [characterDataModified](#event-characterDataModified)
	+ [childNodeCountUpdated](#event-childNodeCountUpdated)
	+ [childNodeInserted](#event-childNodeInserted)
	+ [childNodeRemoved](#event-childNodeRemoved)
	+ [documentUpdated](#event-documentUpdated)
	+ [setChildNodes](#event-setChildNodes)


3. [Types](#types)
	1. [HighlightConfig](#type-HighlightConfig)
	+ [Node](#type-Node)
	+ [NodeId](#type-NodeId)
	+ [RGBA](#type-RGBA)

这个域暴露 DOM 的读写操作。每个 DOM 节点代表着携带有 id 的镜面对象。这个 id 是用来获取节点其余信息，将其装入 JavaScript 对象的包装器中，还要其他。用户端只接受它已知的节点产生的　DOM　事件，这是很重要的。后台追踪节点发送到用户端，并且不会发送同一个节点两次。收集发送过来节点的信息是用户端负责的。

> 注意: iframe 宿主元素会返回对应文本元素作为子节点。


<a name="commands"></a>
### Commands
<a name="command-getAttributes"></a>
#### DOM.getAttributes
```javascript
request: {
"id": <number>,
"method": "DOM.getAttributes",
"params": {
  "nodeId": <NodeId>
}
}
response: {
"id": <number>,
"error": <object>,
"result": {
  "attributes": <array of string>
}
}
```
返回指定节点的属性

##### Parameters

***nodeId ( [NodeId ](#type-NodeId))***
要接受节点的 id


##### Returns
***attributes ( array of string )***
交错数组节点的名称和值

<a name="command-getDocument"></a>
#### DOM.getDocument
```javascript
request: {
"id": <number>,
"method": "DOM.getDocument"
}
response: {
"id": <number>,
"error": <object>,
"result": {
  "root": <Node>
}
}
```
返回根 DOM 节点到调用者

##### Returns
***root ( [Node](#type-Node) )***
结果节点


<a name="command-getOuterHTML"></a>
#### DOM.getOuterHTML
```javascript
request: {
"id": <number>,
"method": "DOM.getOuterHTML",
"params": {
  "nodeId": <NodeId>
}
}
response: {
"id": <number>,
"error": <object>,
"result": {
  "outerHTML": <string>
}
}
```
返回节点的 HTML 加成

##### Parameters

***nodeId ( [NodeId](#type-NodeId) )***
需要加成的节点编号。

##### Returns
***outerHTML ( string )***
超出 HTML 加成。

<a name="command-hideHighlight"></a>
#### DOM.hideHighlight

```javascript
request: {
"id": <number>,
"method": "DOM.hideHighlight"
}
response: {
"id": <number>,
"error": <object>
}
```

隐藏 DOM 节点高亮

<a name="command-highlightNode"></a>
#### DOM.highlightNode
```javascript
request: {
"id": <number>,
"method": "DOM.highlightNode",
"params": {
  "highlightConfig": <HighlightConfig>,
  "nodeId": <NodeId>
}
}
response: {
"id": <number>,
"error": <object>
}
```
高亮显示给定 id 和给定 JavaScript 对象包装的 DOM 元素，nodeId 或者 objectId 必须被指定一个。

##### Parameters
***highlightConfig ( [HighlightConfig](#type-HighlightConfig) )***
高亮显示的描述

***nodeId ( optional [NodeId](#type-NodeId) )***
高亮节点的标示符

<a name="command-highlightRect"></a>
#### DOM.highlightRect
```javascript
request: {
"id": <number>,
"method": "DOM.highlightRect",
"params": {
  "x": <integer>,
  "y": <integer>,
  "width": <integer>,
  "height": <integer>,
  "color": <RGBA>,
  "outlineColor": <RGBA>
}
}
response: {
"id": <number>,
"error": <object>
}
```
高亮给定的矩形区域。坐标是相对于主框架视图绝对定位的。

##### Parameters
***x ( integer )***
X 轴坐标

***y ( integer )***
Y 轴坐标

***width ( integer )***
矩形宽

***height ( integer )***
矩形高

***color ( optional [RGBA](#type-RGBA) )***
高亮填充颜色（默认：透明）

***outlineColor ( optional [RGBA](#type-RGBA) )***
高亮轮廓颜色（默认：透明）

<a name="command-moveTo"></a>
#### DOM.moveTo
```javascript
request: {
"id": <number>,
"method": "DOM.moveTo",
"params": {
  "nodeId": <NodeId>,
  "targetNodeId": <NodeId>,
  "insertBeforeNodeId": <NodeId>
}
}
response: {
"id": <number>,
"error": <object>,
"result": {
  "nodeId": <NodeId>
}
}
```
将节点移动到一个新的容器，将其放置在给定锚之前。

##### Parameters

***nodeId ( [NodeId](#type-NodeId) )***
要移动节点的 id


***targetNodeId ( [NodeId](#type-NodeId) )***
节点移动到的元素 id


***insertBeforeNodeId ( optional [NodeId](#type-NodeId) )***
给定节点之前插入本节点

##### Returns

***nodeId ( [NodeId](#type-NodeId) )***
节点移动后的新 id


<a name="command-querySelector"></a>
#### DOM.querySelector
```javascript
request: {
"id": <number>,
"method": "DOM.querySelector",
"params": {
  "nodeId": <NodeId>,
  "selector": <string>
}
}
response: {
"id": <number>,
"error": <object>,
"result": {
  "nodeId": <NodeId>
}
}
```
对给定节点执行<code>querySelector</code>操作。

##### Parameters
***nodeId ( [NodeId](#type-NodeId) )***
要进行查询操作的节点的 id

***selector ( string )***
选择符

##### Returns
***nodeId ( [NodeId](#type-NodeId) )***
查询筛选后的结果


<a name="command-querySelectorAll"></a>
#### DOM.querySelectorAll
```javascript
request: {
"id": <number>,
"method": "DOM.querySelectorAll",
"params": {
  "nodeId": <NodeId>,
  "selector": <string>
}
}
response: {
"id": <number>,
"error": <object>,
"result": {
  "nodeIds": <array of NodeId>
}
}
```
对一个节点进行 <code>querySelectorAll</code>操作

##### Parameters

***nodeId ( [NodeId](#type-NodeId) )***
要进行操作的节点的 id.
Id of the node to query upon.

***selector ( string )***
选择符


##### Returns
***nodeIds ( array of [NodeId](#type-NodeId) )***
查询操作返回结果


<a name="command-removeAttribute"></a>
#### DOM.removeAttribute
```jvascript
request: {
"id": <number>,
"method": "DOM.removeAttribute",
"params": {
  "nodeId": <NodeId>,
  "name": <string>
}
}
response: {
"id": <number>,
"error": <object>
}
```
移除给定 id 元素上的给定名称的属性

##### Parameters
***nodeId ( [NodeId](#type-NodeId) )***
要移除属性的元素的 id

***name ( string )***
要移除属性的名称

<a name="command-removeNode"></a>
#### DOM.removeNode
```javascript
request: {
"id": <number>,
"method": "DOM.removeNode",
"params": {
  "nodeId": <NodeId>
}
}
response: {
"id": <number>,
"error": <object>
}
```
移除给定 id 的节点


##### Parameters
***nodeId ( [NodeId](#type-NodeId) )***
要移除节点的 id

<a name="command-requestChildNodes"></a>
#### DOM.requestChildNodes
```javascript
request: {
"id": <number>,
"method": "DOM.requestChildNodes",
"params": {
  "nodeId": <NodeId>
}
}
response: {
"id": <number>,
"error": <object>
}
```
发送请求，返回在设置子节点事件的表单里，给定 id 节点的子节点给调用者，在表单中，不仅当前子节点被检索，所有到达指定深度的节点都会被检索到

##### Parameters
***nodeId ( [NodeId](#type-NodeId) )***
获取子节点的节点的 id


<a name="command-requestNode"></a>
#### DOM.requestNode
```javascript
request: {
"id": <number>,
"method": "DOM.requestNode",
"params": {
  "objectId": <Runtime.RemoteObjectId>
}
}
response: {
"id": <number>,
"error": <object>,
"result": {
  "nodeId": <NodeId>
}
}
```
发送请求，节点被返回到有着 JavaScript 节点对象参照的调用者。所有有从节点到根路径的节点，同样以一系列设置子节点的通知，发送到用户端。

##### Parameters
***objectId ( [Runtime.RemoteObjectId](runtime.html#type-RemoteObjectId) )***
要转换成节点的 JavaScript 对象的 id.


##### Returns
***nodeId ([NodeId](#type-NodeId) )***
给定对象的节点 id


<a name="command-resolveNode"></a>
#### DOM.resolveNode
```javascript
request: {
"id": <number>,
"method": "DOM.resolveNode",
"params": {
  "nodeId": <NodeId>,
  "objectGroup": <string>
}
}
response: {
"id": <number>,
"error": <object>,
"result": {
  "object": <Runtime.RemoteObject>
}
}
```
解析给定节点 id 的 JavaScript 节点对象。

##### Parameters
***nodeId ( [NodeId](#type-NodeId) )***
要解析的节点的 id

***objectGroup ( optional string )***
象征性组名，能被用来释放多组对象。

##### Returns
***object ( [Runtime.RemoteObjectId](runtime.html#type-RemoteObjectId)  )***
给定节点的 JavaScript 对象包装器。

<a name="command-setAttributeValue"></a>
#### DOM.setAttributeValue
```javascript
request: {
"id": <number>,
"method": "DOM.setAttributeValue",
"params": {
  "nodeId": <NodeId>,
  "name": <string>,
  "value": <string>
}
}
response: {
"id": <number>,
"error": <object>
}
```
为给定 id 元素设置属性

##### Parameters
***nodeId ([NodeId](#type-NodeId) )***
要设置属性元素的 id

***name ( string )***
属性名

***value ( string )***
属性值

<a name="command-setAttributesAsText"></a>
#### DOM.setAttributesAsText
```javascript
request: {
"id": <number>,
"method": "DOM.setAttributesAsText",
"params": {
  "nodeId": <NodeId>,
  "text": <string>,
  "name": <string>
}
}
response: {
"id": <number>,
"error": <object>
}
```
为给定 id 的节点设置属性。当用户在多属性 name/value 组中编辑一些存在属性的值和类型的时候是很有用的。

##### Parameters
***nodeId ( [NodeId](#type-NodeId) )***
要设置属性的元素的 id

***text ( string )***
表示许多属性的文本。使用HTML解析器将解析这个文本。

***name ( optional string )***
属性名称，成功解析文本后以取代在来自文本的新属性。

<a name="command-setNodeName"></a>
#### DOM.setNodeName
```javascript
request: {
"id": <number>,
"method": "DOM.setNodeName",
"params": {
  "nodeId": <NodeId>,
  "name": <string>
}
}
response: {
"id": <number>,
"error": <object>,
"result": {
  "nodeId": <NodeId>
}
}
```
为给定 id 的节点设置节点名（name)

##### Parameters
***nodeId ( [NodeId](#type-NodeId) )***
要设置 name 的节点的 id

***name ( string )***
节点新名称

##### Returns
***nodeId ([NodeId](#type-NodeId) )***
节点新名称

<a name="command-setNodeValue"></a>
#### DOM.setNodeValue
```javascript
request: {
"id": <number>,
"method": "DOM.setNodeValue",
"params": {
  "nodeId": <NodeId>,
  "value": <string>
}
}
response: {
"id": <number>,
"error": <object>
}
```
为给定 id 的节点设置节点值（value）

##### Parameters
***nodeId ( [NodeId](#type-NodeId))***
要设置 value  节点的 id

***value ( string )***
节点新的值

<a name="command-setOuterHTML"></a>
#### DOM.setOuterHTML
```javascript
request: {
"id": <number>,
"method": "DOM.setOuterHTML",
"params": {
  "nodeId": <NodeId>,
  "outerHTML": <string>
}
}
response: {
"id": <number>,
"error": <object>
}
```
为节点设置 HTML 标记，返回一个新节点。

##### Parameters
***nodeId ( [NodeId](#type-NodeId))***
要设置标记的节点


***outerHTML ( string )***
要设置的外部 HTML 标记。

<a name="events"></a>
### Notifications
<a name="event-attributeModified"></a>
#### DOM.attributeModified
```javascript
{
"method": "DOM.attributeModified",
"params": {
  "nodeId": <NodeId>,
  "name": <string>,
  "value": <string>
}
}
```
当元素的属性被修改会被触发

##### Parameters
***nodeId ( [NodeId](#type-NodeId) )***
修改了的节点的 id

***name ( string )***
属性名称

***value ( string )***
属性值

<a name="event-attributeRemoved"></a>
#### DOM.attributeRemoved
```javascript
{
"method": "DOM.attributeRemoved",
"params": {
  "nodeId": <NodeId>,
  "name": <string>
}
}
```

当元素属性值被修改，会被触发。

##### Parameters
***nodeId ( [NodeId](#type-NodeId) )***
被修改了的节点的 id

***name ( string )***
属性名

<a name="event-characterDataModified"></a>
#### DOM.characterDataModified
```javascript
{
"method": "DOM.characterDataModified",
"params": {
  "nodeId": <NodeId>,
  "characterData": <string>
}
}
```
反射 <code>DOMCharacterDataModified</code>事件

##### Parameters
***nodeId ( [NodeId](#type-NodeId) )***
被修改了的节点的 id

***characterData ( string )***
下一个文本的值

<a name="event-childNodeCountUpdated"></a>
#### DOM.childNodeCountUpdated
```javascript
{
"method": "DOM.childNodeCountUpdated",
"params": {
  "nodeId": <NodeId>,
  "childNodeCount": <integer>
}
}
```
当子节点数被修改后被触发

#### Parameters
***nodeId ( [NodeId](#type-NodeId) )***
被修改节点的 id

***childNodeCount ( integer )***
新节点数

<a name="event-childNodeInserted"></a>
#### DOM.childNodeInserted
```javascript
{
"method": "DOM.childNodeInserted",
"params": {
  "parentNodeId": <NodeId>,
  "previousNodeId": <NodeId>,
  "node": <Node>
}
}
```

反映 <code>DOMNodeInserted</code> 事件.

##### Parameters
***parentNodeId ( [NodeId](#type-NodeId) )***
被修改的节点的 id

***previousNodeId ( [NodeId](#type-NodeId) )***
 如果有前兄弟节点

***node ( [NodeId](#type-NodeId) )***
插入的节点的数据

<a name="event-childNodeRemoved"></a>
#### DOM.childNodeRemoved
```javascript
{
"method": "DOM.childNodeRemoved",
"params": {
  "parentNodeId": <NodeId>,
  "nodeId": <NodeId>
}
}
```
反映<code>DOMNodeRemoved</code>事件.

##### Parameters
***parentNodeId ( [NodeId](#type-NodeId))***
父节点 id


***nodeId ( [NodeId](#type-NodeId))***
被移除了的节点的 id

<a name="event-documentUpdated"></a>
#### DOM.documentUpdated
```javascript
{
"method": "DOM.documentUpdated"
}
```
当文档被完全更新才会被触发。节点的 id 都不再有效

<a name="event-setChildNodes"></a>
#### DOM.setChildNodes
```javascript
{
"method": "DOM.setChildNodes",
"params": {
  "parentId": <NodeId>,
  "nodes": <array of Node>
}
}
```
当后台想为用户端提供丢失 DOM 结构时会被触发。当大多数调用请求节点 id 时会发生。

##### Parameters
***parentId ( [NodeId](#type-NodeId) )***
要填充子节点的父节点的 id

***nodes ( array of Node )***
子节点数组

<a name="types"></a>
### Types
<a name="type-HighlightConfig"></a>
#### HighlightConfig: object

***borderColor ( optional RGBA )***
边框高亮颜色（默认：透明）

***contentColor ( optional [RGBA ](#type-RGBA))***
内容盒子的高亮颜色（默认：透明）

***marginColor ( optional [RGBA ](#type-RGBA) )***
margin 填充高亮颜色（默认：透明）

***paddingColor ( optional [RGBA ](#type-RGBA) )***
padding 填充高亮颜色（默认：透明）

***showInfo ( optional boolean )***
节点信息提示是否显示（默认：false）

<a name="type-Node"></a>
#### Node: object
***attributes ( optional array of string )***
一维数组 [name1, value1, name2, value2] 表单中，元素节点的属性。

***childNodeCount ( optional integer )***
容器节点的子节点数

***children ( optional array of [Node](#type-Node) )***
需要填充的子节点数

***contentDocument ( optional [Node](#type-Node) )***
frame 宿主元素的内容文档

***documentURL ( optional string )*** 
Document 节点或者 FrameOwner 节点指向的 Document URL

***internalSubset ( optional string )***
DocumentType 的内置子集

***localName ( string )***
节点的本地名名

***name ( optional string )***
属性的名称

***nodeId ( [NodeId](#type-NodeId) )***
作为 nodeId 传入 DOM 消息 的节点标识符。后台只会一次性推送给定 id 的节点。它知道所有请求节点，只会为已知的客户机节点触发 DOM 事件。

***nodeName ( string )***
节点名

***nodeType ( integer )***
节点类型

***nodeValue ( string )***
节点值

***publicId ( optional string )***
DocumentType 的公开 id（publicId）

***systemId ( optional string )***
DocumentType 的系统 id（systemId）

***value ( optional string )***
属性值

***xmlVersion ( optional string )***
如果是 XML 文档，XML 版本。
<a name="type-NodeId"></a>
#### NodeId: integer
<a name="type-RGBA"></a>
#### RGBA: object
***a ( optional number )***
alpha 分量，在 [0-1] 范围（默认值：1）。

***b ( integer )***
蓝色分量，在[0-255]范围内。

***g ( integer )***
绿色分量，在[0-255]范围内。

***r ( integer )***
红色分量，在[0-255]范围内。

