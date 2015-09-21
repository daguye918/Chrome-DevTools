# 远程调试协议1.1
工具栏被分成若干域（DOM，Debugger，NetWork等）的。每个域定义了一些它支持的命令和它产生的事件。命令和事件是固定结构序列化的 JSON 对象。你可以在[调试](https://developer.chrome.com/devtools/docs/debugger-protocol)使用原始消息，因为它们在相应域的文档资料中被定义，或使用[扩展的 JavaScript API](https://developer.chrome.com/devtools/docs/debugger-protocol#extension)。
<table style="border:none">
<tbody><tr>
<td style="border:none">
<ul>
  <li> <a href="console.md">Console</a> </li>
  <li> <a href="debugger.md">Debugger</a> </li>
  <li> <a href="dom.md">DOM</a> </li>
</ul>
</td>
<td style="border:none">
<ul>
  <li> <a href="dom-debuger.md">DOM Debugger</a> </li>
  <li> <a href="input.md">Input</a> </li>
  <li> <a href="network.md">Network</a> </li>
</ul>
</td>
<td style="border:none">
<ul>
  <li> <a href="page.md">Page</a> </li>
  <li> <a href="runtime.md">Runtime</a> </li>
  <li> <a href="timeline.md">Timeline</a> </li>
</ul>
</td>
</tr>
</tbody></table>