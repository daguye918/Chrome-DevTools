# 1.1: 时间轴

## Contents
1. [Commands](#commands)
	1. [start](#command-start)
	+ [stop](#command-stop)


2. [Notifications](#events)

	2. [eventRecorded](#event-eventRecorded)
[Types](#types)
	+ [TimelineEvent](#type-TimelineEvent)

时间轴为用户端提供了仪表记录，这些记录实在页面运行时候产生的。时间轴仪表可以使用对应的命令来开关。当时间轴开始后，它会收集时间轴的事件记录。

<a name="commands"></a>
### Commands
<a name="command-start"></a>
#### Timeline.start
```javascript
request: {
"id": <number>,
"method": "Timeline.start",
"params": {
  "maxCallStackDepth": <integer>
}
}
response: {
"id": <number>,
"error": <object>
}
```
开始捕捉时间轴仪表事件。


#### Parameters
***maxCallStackDepth ( optional integer )***
JavaScript 栈追踪器最多为 <code>maxCallStackDepth</code>个，默认到 5 个。

<a name="command-stop"></a>
#### Timeline.stop
```javascript
request: {
"id": <number>,
"method": "Timeline.stop"
}
response: {
"id": <number>,
"error": <object>
}
```
停止捕捉时间轴仪盘表事件。

<a name="events"></a>
### Notifications
<a name="event-eventRecorded"></a>
#### Timeline.eventRecorded
```javascript
{
"method": "Timeline.eventRecorded",
"params": {
  "record": <TimelineEvent>
}
}
```
当时间轴开启，每个仪表事件都会触发。

#### Parameters
***record ( TimelineEvent )***
Timeline 事件记录数据。

<a name="types"></a>
### Types
<a name="type-TimelineEvent"></a>
#### TimelineEvent: object
***children ( optional array of TimelineEvent )***
嵌套记录

***data ( object )***
事件数据

***type ( string )***
事件类型