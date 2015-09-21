# 1.1：Input

## 内容
1. [Commands](#commands)
	1. [dispatchKeyEvent](#command-dispatchKeyEvent)
	+ [dispatchMouseEvent](#command-dispatchMouseEvent)

<a name="commands"></a>
### Commands
<a name="command-dispatchKeyEvent"></a>
#### Input.dispatchKeyEvent
```javascript
request: {
"id": <number>,
"method": "Input.dispatchKeyEvent",
"params": {
  "type": <string>,
  "modifiers": <integer>,
  "timestamp": <number>,
  "text": <string>,
  "unmodifiedText": <string>,
  "keyIdentifier": <string>,
  "windowsVirtualKeyCode": <integer>,
  "nativeVirtualKeyCode": <integer>,
  "macCharCode": <integer>,
  "autoRepeat": <boolean>,
  "isKeypad": <boolean>,
  "isSystemKey": <boolean>
}
}
response: {
"id": <number>,
"error": <object>
}
```
为网页分配一个关键事件

##### Parameters

***type ( enumerated string [ "char" , "keyDown" , "keyUp" , "rawKeyDown" ] )***
关键事件的类型


***modifiers ( optional integer )***
代表按键的位字段（Alt=1, Ctrl=2, Meta/Command = 4, Shift = 8 (default: 0).


***timestamp ( optional number )***
事件发生的时刻。从 1970 年 1 月 1 号开始，以 UTC 时间标准以秒计算（默认：当前时间）。


***text ( optional string )***
用键盘布局处理一个虚拟键码生成的文本。对于 KeyUp 和 rawKeyDown 事件是不需要的（默认：""）


***unmodifiedText ( optional string )***
由键盘连续输入的文本，中间没有按键改变（除了<kbd>shift</kbd>外）。对于加快（计算）键位处理很有用（默认：""）


***keyIdentifier ( optional string )***
唯一的键位识别器（例如，“U+ 0041”）默认（:""）


***windowsVirtualKeyCode ( optional integer )***
Windows 系统虚拟键码(默认：0)


***nativeVirtualKeyCode ( optional integer )***
本机虚拟键码（默认：0）


***macCharCode ( optional integer )***
Mac 的字符代码


***autoRepeat ( optional boolean )***
是否自动提交事件（默认：false）


***isKeypad ( optional boolean )***
是否是由键盘生成的事件（默认：false）

***isSystemKey ( optional boolean )***
事件是否是系统的一个关键事件（默认：false）

<a name="command-dispatchMouseEvent"></a>
#### Input.dispatchMouseEvent
```javascript
request: {
"id": <number>,
"method": "Input.dispatchMouseEvent",
"params": {
  "type": <string>,
  "x": <integer>,
  "y": <integer>,
  "modifiers": <integer>,
  "timestamp": <number>,
  "button": <string>,
  "clickCount": <integer>
}
}
response: {
"id": <number>,
"error": <object>
}
```
适配页面的一个鼠标事件

##### Parameters
***type ( enumerated string [ "mouseMoved" , "mousePressed" , "mouseReleased" ] )***
鼠标事件的类型

***x ( integer )***
主框架视图相关事件的 X 坐标

***y ( integer )***。0 代表视图的顶部，随着主帧视图相关事件的 Y 坐标。随着 Y 坐标的增加，他会向视图的底部移动。

***modifiers ( optional integer )***
代表按键组合的位字段。Alt = 1, Ctrl = 2, Meta/Command = 4, Shift = 8 (默认: 0)

***timestamp ( optional number )***
事件触发的时间，从 1970 年 1 月 1 号开始，以 UTC 时间标准以秒计算（默认：当前时间）

***button ( optional enumerated string [ "left" , "middle" , "none" , "right" ] )***
鼠标按键（默认：无）

***clickCount ( optional integer )***
鼠标点击的次数（默认：0）
