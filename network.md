# 1.1：Network
## Contents

1.  [Commands](#commands)
	1. [canClearBrowserCache](#command-canClearBrowserCache)
	+ [canClearBrowserCookies](#command-canClearBrowserCookies)
	+ [clearBrowserCache](#command-clearBrowserCache)
	+ [clearBrowserCookies](#command-clearBrowserCookies)
	+ [disable](#command-disable)
	+ [enable](#command-enable)
	+ [getResponseBody](#command-getResponseBody)
	+ [setCacheDisabled](#command-setCacheDisabled)
	+ [setExtraHTTPHeaders](#command-setExtraHTTPHeaders)
	+ [setUserAgentOverride](#command-setUserAgentOverride)


2. [Notifications](#events)

	1. [dataReceived](#event-dataReceived)
	+ [loadingFailed](#event-loadingFailed)
	+ [loadingFinished](#event-loadingFinished)
	+ [requestServedFromCache](#event-requestServedFromCache)
	+ [requestWillBeSent](#event-requestWillBeSent)
	+ [responseReceived](#event-responseReceived)

3. [Types](#types)

	1. [CachedResource](#type-CachedResource)
	+ [Headers](#type-Headers)
	+ [Initiator](#type-Initiator)
	+ [LoaderId](#type-LoaderId)
	+ [Request](#type-Request)
	+ [RequestId](#type-RequestId)
	+ [ResourceTiming](#type-ResourceTiming)
	+ [Response](#type-Response)
	+ [Timestamp](#type-Timestamp)
	
	
Network 域可以追踪页面的网络活动。它提供关于 http，file，data 和其他的请求和应答，header 消息，body 主题,timing 信息，等等。


<a name="commands"></a>
### Commands
<a name="command-canClearBrowserCache"></a>
#### Network.canClearBrowserCache
```javascript
request: {
"id": <number>,
"method": "Network.canClearBrowserCache"
}
response: {
"id": <number>,
"error": <object>,
"result": {
  "result": <boolean>
}
}
```
识别是否支持清除浏览器缓存

#### Returns

***result ( boolean )***
如果浏览器缓存可以被清除返回为 true.

<a name="command-canClearBrowserCookies"></a>
#### Network.canClearBrowserCookies
```javascript
request: {
"id": <number>,
"method": "Network.canClearBrowserCookies"
}
response: {
"id": <number>,
"error": <object>,
"result": {
  "result": <boolean>
}
}
```
识别是否支持清除浏览器 cookies 信息

##### Returns
***result ( boolean )***
如果浏览器 cookie 信息能被清除返回为 true

<a name="command-clearBrowserCache"></a>
#### Network.clearBrowserCache
```javascript
request: {
"id": <number>,
"method": "Network.clearBrowserCache"
}
response: {
"id": <number>,
"error": <object>
}
```
清除浏览器缓存

<a name="command-clearBrowserCookies"></a>
#### Network.clearBrowserCookies
```javascript
request: {
"id": <number>,
"method": "Network.clearBrowserCookies"
}
response: {
"id": <number>,
"error": <object>
}
```
清除浏览器 cookies 信息

<a name="command-disable"></a>
#### Network.disable
```javascript
request: {
"id": <number>,
"method": "Network.disable"
}
response: {
"id": <number>,
"error": <object>
}
```
禁用网络跟踪，阻止网络事件发送到用户端


<a name="command-enable"></a>
#### Network.enable
```javascript
request: {
"id": <number>,
"method": "Network.enable"
}
response: {
"id": <number>,
"error": <object>
}
```
启用网络跟踪，网络事件会被发送到用户端。


<a name="command-getResponseBody"></a>
#### Network.getResponseBody
```javascript
request: {
"id": <number>,
"method": "Network.getResponseBody",
"params": {
  "requestId": <RequestId>
}
}
response: {
"id": <number>,
"error": <object>,
"result": {
  "body": <string>,
  "base64Encoded": <boolean>
}
}
```
返回给定请求的内容

##### Parameters
***requestId ( [RequestId ](#type-RequestId))***
用于获取网络请求的标识符

##### Returns
***body ( string )***
请求主体

***base64Encoded ( boolean )***
true， 以 64 位编码发送内容


<a name="command-setCacheDisabled"></a>
#### Network.setCacheDisabled
```javascript
request: {
"id": <number>,
"method": "Network.setCacheDisabled",
"params": {
  "cacheDisabled": <boolean>
}
}
response: {
"id": <number>,
"error": <object>
}
```
将每个请求设为忽略缓存的请求。若为 true，缓存就没有用到。

##### Parameters
***cacheDisabled ( boolean )***
缓存是否是禁用状态

<a name="command-setExtraHTTPHeaders"></a>
#### Network.setExtraHTTPHeaders
```javascript
request: {
"id": <number>,
"method": "Network.setExtraHTTPHeaders",
"params": {
  "headers": <Headers>
}
}
response: {
"id": <number>,
"error": <object>
}
```
指定是否总是发送带有多余 HTTP 请求头的请求至这个页面

##### Parameters
***headers ( [Headers](#type-Headers) )***
用多余 HTTP 请求头标识


<a name="command-setUserAgentOverride"></a>
#### Network.setUserAgentOverride
```javascript
request: {
"id": <number>,
"method": "Network.setUserAgentOverride",
"params": {
  "userAgent": <string>
}
}
response: {
"id": <number>,
"error": <object>
}
```
可以用给定的字符串替换用户代理。


##### Parameters
***userAgent ( string )***
要使用的用户代理



<a name="events"></a>
### Notifications
<a name="event-dataReceived"></a>
#### Network.dataReceived
```javascript
{
"method": "Network.dataReceived",
"params": {
  "requestId": <RequestId>,
  "timestamp": <Timestamp>,
  "dataLength": <integer>,
  "encodedDataLength": <integer>
}
}
```
当数据块通过网络接收时时间被触发

#### Parameters
***requestId ( [RequestId](#type-RequestId) )***
请求标识符

***timestamp ( [Timestamp](#type-Timestamp) )***
时间戳 Timestamp.

***dataLength ( integer )***
数据块长度

***encodedDataLength ( integer )***
实际接收到的字节（可能以为压缩编码会比数据长度要短）



<a name="event-loadingFailed"></a>
#### Network.loadingFailed
```javascript
{
"method": "Network.loadingFailed",
"params": {
  "requestId": <RequestId>,
  "timestamp": <Timestamp>,
  "errorText": <string>,
  "canceled": <boolean>
}
}
```
当 HTTP 请求载入失败时会被触发。

##### Parameters
***requestId ( [RequestId](#type-RequestId) )***
请求标识符

***timestamp ( [Timestamp](#type-Timestamp) )***
时间戳 Timestamp.

***errorText ( string )***
用户友好的错误提示

***canceled ( optional boolean )***
设为true，载入过程会被取消。


<a name="event-loadingFinished"></a>
#### Network.loadingFinished
```javascript
{
"method": "Network.loadingFinished",
"params": {
  "requestId": <RequestId>,
  "timestamp": <Timestamp>
}
}
```
如果 HTTP 请求完成载入，事件会被触发。


##### Parameters
***requestId ( [RequestId](#type-RequestId))***
请求标识符

***timestamp ( [Timestamp](#type-Timestamp) )***
时间戳 Timestamp.


<a name="event-requestServedFromCache"></a>
#### Network.requestServedFromCache
```javascript
{
"method": "Network.requestServedFromCache",
"params": {
  "requestId": <RequestId>
}
}
```
如果从请求完成从缓存载入时，时间会被触发
Fired if request ended up loading from cache.

##### Parameters
***requestId ( [RequestId](#type-RequestId) )***
请求标识符


<a name="event-requestWillBeSent"></a>
#### Network.requestWillBeSent
```javascript
{
"method": "Network.requestWillBeSent",
"params": {
  "requestId": <RequestId>,
  "loaderId": <LoaderId>,
  "documentURL": <string>,
  "request": <Request>,
  "timestamp": <Timestamp>,
  "initiator": <Initiator>,
  "redirectResponse": <Response>
}
}
```
当页面要发送 HTTP 请求时，会被触发

##### Parameters
***requestId ( [RequestId](#type-RequestId) )***
请求标识符

***loaderId ( [LoaderId](#type-LoaderId) )***
加载容器标识符

***documentURL ( string )***
这个请求加载的文件的 URL

***request ( [Request](#type-Request) )***
请求数据

***timestamp ( [Timestamp](#type-Timestamp) )***
时间戳 Timestamp.

***initiator ( [Initiator](#type-Initiator) )***
请求初始启动器

***redirectResponse ( optional [Response](#type-Response) )***
重定向响应数据



<a name="event-responseReceived"></a>
#### Network.responseReceived
```javascript
{
"method": "Network.responseReceived",
"params": {
  "requestId": <RequestId>,
  "loaderId": <LoaderId>,
  "timestamp": <Timestamp>,
  "type": <Page.ResourceType>,
  "response": <Response>
}
}
```
当 HTTP 响应收到时被触发

##### Parameters
***requestId ([RequestId](#type-RequestId) )***
请求标识符

***loaderId ( [LoaderId](#type-LoaderId) )***
加载容器标识符

***timestamp ( [Timestamp](#type-Timestamp) )***
时间戳 Timestamp.

***type ( [Page.ResourceType](page.html#type-ResourceType))***
资源源类型

***response ( [Response](#type-Response))***
响应数据

<a name="types"></a>
### Types
<a name="type-CachedResource"></a>
#### CachedResource: object
***bodySize ( number )***
缓存的响应消息主体的大小

***response ( optional Response )***
缓存的响应数据

***type ( Page.ResourceType )***
资源的类型

***url ( string )***
资源的 URL 路径。这是原始网络请求的 url。

<a name="type-Headers"></a>
#### Headers: object

<a name="type-Initiator"></a>
#### Initiator: object
***lineNumber ( optional number )***
初始构造器（Initiator）的行，为解析器（Parser）类型而设

***stackTrace ( optional [Console.StackTrace](console.html#type-StackTrace) )***
初始构造器（Initiator） JavaScript 栈追踪器，为 Script 脚本而设

***type ( enumerated string [ "other" , "parser" , "script" ] )***
初始构造器的类型（initiator）

***url ( optional string )***
初始构造器（Initiator）URL 路径，为解析器（Parser）类型而设

<a name="type-LoaderId"></a>
#### LoaderId: string

<a name="type-Request"></a>
#### Request: object
***headers ( [Headers](#type-Headers) )***
HTTP 请求头

***method ( string )***
HTTP 请求方法

***postData ( optional string )***
HTTP POST 请求的数据

***url ( string )***
请求的 URL 路径。

<a name="type-RequestId"></a>
#### RequestId: string

<a name="type-ResourceTiming"></a>
#### ResourceTiming: object

***connectEnd ( number )***
连接到的远程主机
Connected to the remote host.

***connectStart ( number )***
开始连接远程主机

***dnsEnd ( number )***
完成 DNS 地址解析

***dnsStart ( number )***
开始 DNS 地址解析

***proxyEnd ( number )***
完成代理设置

***proxyStart ( number )***
开始代理设置

***receiveHeadersEnd ( number )***
完成接收响应头

***requestTime ( number )***
定时的 requestTime 以秒为基准，而其他的数字相对于 requestTime 是非常大的。

***sendEnd ( number )***
完成发送请求

***sendStart ( number )***
开始发送请求

***sslEnd ( number )***
完成 SSL 握手。

***sslStart ( number )***
开始 SSL 握手。

<a name="type-Response"></a>
#### Response: object
***connectionId ( number )***
被实际用于这一请求的物理连接的 ID。

***connectionReused ( boolean )***
指定物理连接是否被重用于这个请求

***fromDiskCache ( optional boolean )***
指定是否利用本地缓存发送请求

***headers ( [Headers](#type-Headers) )***
HTTP 响应头对象

***headersText ( optional string )***
HTTP 响应头文本

***mimeType ( string )***
资源的 mimeType，由浏览器来确定。

***requestHeaders ( optional Headers )***
精细化通过网络传输传输的 HTTP 请求头

***requestHeadersText ( optional string )***
HTTP 请求头文本

***status ( number )***
HTTP 响应状态码

***statusText ( string )***
HTTP 响应状态文本形式

***timing ( optional [ResourceTiming](#type-ResourceTiming) )***
对于给定的请求定时信息。

***url ( string )***
响应 URL。此 URL 可以从不同 CachedResource.url 的情况下重定向。

<a name="type-Timestamp"></a>
#### Timestamp: number
