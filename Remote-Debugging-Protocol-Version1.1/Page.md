# 1.1:Page

## 内容

1. [Commands](#commands)
	1. [clearGeolocationOverride](#command-clearGeolocationOverride)
	+ [disable](#command-disable)
	+ [enable](#command-enable)
	+ [navigate](#command-navigate)
	+ [reload](#command-reload)
	+ [setGeolocationOverride](#command-setGeolocationOverride)

2. [Notifications](#events)
	1. [domContentEventFired](#event-domContentEventFired)
	+ [frameAttached](#event-frameAttached)
	+ [frameDetached](#event-frameDetached)
	+ [frameNavigated](#event-frameNavigated)
	+ [loadEventFired](#event-loadEventFired)

3. [Types](#types)
	1. [Frame](#type-Frame)
	+ [FrameId](#type-FrameId)
	+ [ResourceType](#type-ResourceType)

行为和事件，有关于属于页面域中被审查的页面。

<a name="commands"></a>
### Commands

<a name="command-clearGeolocationOverride"></a>
#### Page.clearGeolocationOverride
```javascript
request: {
"id": <number>,
"method": "Page.clearGeolocationOverride"
}
response: {
"id": <number>,
"error": <object>
}
```
清除重写 Geolocation 位置和错误

<a name="command-disable"></a>
#### Page.disable
```javascript
request: {
"id": <number>,
"method": "Page.disable"
}
response: {
"id": <number>,
"error": <object>
}
```
是整个页域（page domain）提示器失效

<a name="command-enable"></a>
#### Page.enable
```javascript
request: {
"id": <number>,
"method": "Page.enable"
}
response: {
"id": <number>,
"error": <object>
}
```
启用页域（page domain）的提示器。

<a name="command-navigate"></a>
#### Page.navigate
```javascript
request: {
"id": <number>,
"method": "Page.navigate",
"params": {
  "url": <string>
}
}
response: {
"id": <number>,
"error": <object>
}
```
将当页面导向给定的 URL.

##### Parameters 参数
***url ( string )***
页面导向的 URL


<a name="command-reload"></a>
#### Page.reload
```javascript
request: {
"id": <number>,
"method": "Page.reload",
"params": {
  "ignoreCache": <boolean>,
  "scriptToEvaluateOnLoad": <string>
}
}
response: {
"id": <number>,
"error": <object>
}
```
忽略缓存有选择性地重载给定的页面

##### Parameters
***ignoreCache ( optional boolean )***
如果返回为 true，浏览器缓存会被忽略。（和用户按 <kbd>Shift</kbd>+<kbd>refresh</kbd> 效果一样）



***scriptToEvaluateOnLoad ( optional string )***
如果被设定，在重载后，这个脚本会被注入到审查页面的所有帧中。



<a name="command-setGeolocationOverride"></a>
#### Page.setGeolocationOverride
```javascript
request: {
"id": <number>,
"method": "Page.setGeolocationOverride",
"params": {
  "latitude": <number>,
  "longitude": <number>,
  "accuracy": <number>
}
}
response: {
"id": <number>,
"error": <object>
}
```
重新 Geolocation 的位置或者错误。

##### Parameters参数
***latitude ( optional number )***
模拟纬度

***longitude ( optional number )***
模拟经度

***accuracy ( optional number )***
模拟精度

<a name="events"></a>
### Notifications

<a name="event-domContentEventFired"></a>
#### Page.domContentEventFired
```javascript
{
"method": "Page.domContentEventFired",
"params": {
  "timestamp": <number>
}
}
```

##### Parameters 参数
***timestamp ( number )***


<a name="event-frameAttached"></a>
#### Page.frameAttached
```javascript
{
"method": "Page.frameAttached",
"params": {
  "frameId": <FrameId>
}
}
```
当帧添加到他的父帧时才会被触发。

##### Parameters
***frameId ( [FrameId](#type-FrameId) )***
被添加帧帧的 ID



<a name="event-frameDetached"></a>
#### Page.frameDetached
```javascript
{
"method": "Page.frameDetached",
"params": {
  "frameId": <FrameId>
}
}
```
当帧与他的父帧分离才会被触发。

##### Parameters
***frameId ( FrameId )***
被分离的帧 ID



<a name="event-frameNavigated"></a>
#### Page.frameNavigated
```javascript
{
"method": "Page.frameNavigated",
"params": {
  "frame": <Frame>
}
}
```
当帧的导航完成了，立即触发。
帧现在与新的载入容器相关联。


##### Parameters

***frame ( [Frame ](#type-FrameId))***
Frame 对象



<a name="event-loadEventFired"></a>
#### Page.loadEventFired
```javascript
{
"method": "Page.loadEventFired",
"params": {
  "timestamp": <number>
}
}
```
##### Parameters
***timestamp ( number )***



<a name="types"></a>
### Types
<a name="type-Frame"></a>
#### Frame: object
***id ( string )***
帧唯一一个识别器。

***loaderId ( [Network.LoaderId](network.html#type-LoaderId) )***
与这个帧相关载入容器的识别器。

***mimeType ( string )***
帧文档的 mimeType，由浏览器决定。

***name ( optional string )***
在指定标签里帧的名字。

***parentId ( optional string )***
父帧的识别器。

***securityOrigin ( string )***
父帧文本的安全源

***url ( string )***
帧对象文本的 URL


<a name="type-FrameId"></a>
#### FrameId: string


<a name="type-ResourceType"></a>
#### ResourceType: enumerated string
***[ "Document" , "Font" , "Image" , "Other" , "Script" , "Stylesheet" , "WebSocket" , "XHR" ]***