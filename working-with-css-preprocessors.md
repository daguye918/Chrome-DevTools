## 使用 CSS 预处理器

许多开发者使用 CSS 预处理器来产生 CSS 样式表，比如 Sass， Less 或者 Stylus。因为 CSS 文件是生成的，直接修改 CSS 文件是没有用的。

对于支持 CSS 源映射（source maps）的预处理器， DevTools 允许你在源面板中实时编辑预处理器的源文件，并且不需要离开 DevTools 或者刷新页面就能查看结果。当你审查生成的 CSS 文件提供的样式元素时，元素面板会显示一个链接到源文件的链接，而不是生成的 <code>.css</code> 文件。


![sass-debugging](images/sass-debugging.png)


如果要跳转到源文件：


- 在源面板中点击相应链接可打开（可编辑的）源文件。
- `Control` + <kbd>鼠标左键</kbd>（或者在Mac上用 `Command` + <kbd>鼠标左键</kbd>）点击 CSS 属性名或者属性值可以打开源文件并且跳转到相应的行。


![sass-sources](images/sass-sources.png)


当你通过 DevTools 来保存对 CSS 预处理器做出的更改时，CSS 预处理器会重新生成 CSS 文件。然后 DevTools 会重新加载新生成的 CSS 文件。


>在外部编辑器中做出的修改不会被 DevTools 侦测到，除非 Source 选项卡包含的相关源文件重新获得了焦点。而且，手动编辑由  Sass/LESS/其他编译器 产生的 CSS 文件将会中断源映射的关联，直到重新加载页面为止。


>如果你正在使用 Workspaces（工作空间），你需要确认产生的文件是否映射到了 Workspace 中。你可以在源面板右侧的树中来查看并验证源自本地的 CSS。

### 要求

使用 CSS 预处理器的时候有一些要求需要满足：

- 如果要使用该工作流，你的 CSS 预处理器必须支持 CSS 源映射，特别是源映射 v3 协议。CSS 源映射必须和 CSS 文件一同建立，所以 DevTools 可以将每个 CSS 属性映射到源文件中的正确位置。（比如，.scss 文件）
- 为了让你改动源文件时， DevTools 会自动加载样式，你的预处理器必须设置为当源文件发生变动时就重新生成 CSS 文件的模式。否则，你只有手动创建新的 CSS 文件并重新加载页面后才能查看到生效后的更改。
- 你必须从 web 服务器来访问你的站点或者应用（不是一个类似于 **file://** 的 URL），而且服务器必须能够支持 CSS 文件以及源映射（source map）（.css .map）和源文件（.scss）。
- 如果你没有使用工作空间的特性，那么 web 服务器也必须能够提供上次修改的文件头。<code>Python SimpleHTTPServer</code> 模块默认会提供这个文件头。你可以像这样启动一个 web 服务来服务当前目录：

```python

python -m SimpleHTTPServer

```


### 启用 CSS 源映射

默认情况下，CSS 源映射是启用的。你可以选择是否要启用自动重新加载生成的 CSS 文件模式。

如果想要启用 CSS 源映射，重载 CSS 文件，请参照以下步骤：

- 打开 DevTools 设置，然后点击 **General**。
- 打开 **Enable CSS source maps** 和 **Auto-reload generated CSS**。

### 利用 CSS 源映射来使用 Sass

要在 Chrome 中实时编辑 Sass 文件，你需要3.3以上的 Sass，因为只有这样才支持源映射。

```

gem install sass

```

当 Sass 安装好以后，开启 Sass 编译器来监测你的 Sass 源文件的改变并为每个产生的 CSS 文件创建源映射文件，例如：

```

sass --watch --sourcemap sass/styles.scss:styles.css

```

### CSS 预编译器支持

DevTools 支持 [Source Map Revision 3 proposal](https://docs.google.com/a/google.com/document/d/1U1RGAehQwRypUTovF1KRlpiOFze0b-_2gc6fAH0KY0k/edit#)。该协议在几个 CSS 预编译器中实施（2014年8月更新）：

- **Sass**：如上面所说的，在 Sass 3.3 以后支持。
- **Compass**：--sourcemap 标签在 [Compass 1.0](http://compass-style.org/blog/2014/08/15/omg-compass-1-0/) 后开始使用。你可以在 config.rb 文件中加入 sourcemap: true 来选择是否启用。这里有一份 [Demo](https://github.com/grayghostvisuals/sourcemaps) 可供参考。开发日志在 [issue 1108](https://github.com/Compass/compass/issues/1108#issuecomment-52432075)。
- **Less**：从1.5.0中开始实现。参考 [issue #1050](https://github.com/less/less.js/issues/1050#issuecomment-25566463) 来了解详细信息和使用模式。
- **Autoprefix**：从 1.0 中开始实现。[Autoprefixer docs](https://github.com/ai/autoprefixer#source-map) 说明了怎么使用它，以及怎么（从另一个预处理器中）接收一个输入的源映射。
- **Libsass**：[详细](https://github.com/hcatlin/libsass/commit/366bc110c39c26c9267a1cc06e578beb94cd93ef)。
- **Stylus**：已支持，最新的信息请见 [issue #1655](https://github.com/LearnBoost/stylus/pull/1655#issuecomment-52826158)。

### 源映射是如何工作的

对于每个生成的 CSS 文件，预处理器另外为编译的 CSS 生成一个[源映射](http://www.html5rocks.com/en/tutorials/developertools/sourcemaps/)文件（.map）。源映射是一个 JSON 格式的文件，它定义了每个生成的 CSS 声明和在原文件中相应行的映射。每个 CSS 文件的最后一行都会含有一个说明其源文件路径的特别注释。

```JSON

/*# sourceMappingURL=<url> */

```

例如，给定一个名为 **styles.css** 的 CSS 文件：

```css

$textSize: 26px;
$fontColor: red;
$bgColor: whitesmoke;

h2 {
    font-size: $textSize;
    color: $fontColor;
    background: $bgColor;
}

```

Sass 会生成一个 **styles.css** 文件并且在后面添加源文件路径映射的注释：

```css

h2 {
  font-size: 26px;
  color: red;
  background-color: whitesmoke;
}
/*# sourceMappingURL=styles.css.map */

```

下面是关于源映射文件的例子：

```JSON

{
  "version": "3",
  "mappings":"AAKA,EAAG;EACC,SAAS,EANF,IAAI;EAOX,KAAK"
  "sources": ["sass/styles.scss"],
  "file": "styles.css"
}

```


### 参考资源

很多开发者会在使用 CSS 预处理器的过程中形成自己的工作流。有关教程和备用工作流的内容请参照下面的文章：

- [Getting Started with CSS sourcemaps and in-browser Sass editing](https://medium.com/what-i-learned-building/b4daab987fb0)
- [Faster Sass debugging and style iteration with source maps, Chrome Web Developer Tools and Grunt](http://benfrain.com/add-sass-compass-debug-info-for-chrome-web-developer-tools/)

>注意：外部资源可能不是有关最新版 Chrome 的资料。

以上内容适用于 [CC-By 3.0 license](http://creativecommons.org/licenses/by/3.0/)