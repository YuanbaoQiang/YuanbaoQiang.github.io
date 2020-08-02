---
title: Hexo 添加代码块Mac Panel特效
date: 2020-07-14 09:24:37
tags: Hexo
categories: Hexo 美化
---

# 引入JS

在`~/themes/next/scripts/`下分别创建`events.js`和`codeblock.js`。

## events.js

```js
// mac Panel效果代码块相关
var exec = require('child_process').exec;

// new 后自动打开编辑器
hexo.on('new', function(data){
  exec('open -a MacDown ' + data.path);
});
```

<!--more-->

## codeblock.js

```js
// mac Panel效果代码块相关
var attributes = [
  'autocomplete="off"',
  'autocorrect="off"',
  'autocapitalize="off"',
  'spellcheck="false"',
  'contenteditable="true"'
]

var attributesStr = attributes.join(' ')

hexo.extend.filter.register('after_post_render', function (data) {
  while (/<figure class="highlight ([a-zA-Z]+)">.*?<\/figure>/.test(data.content)) {
    data.content = data.content.replace(/<figure class="highlight ([a-zA-Z]+)">.*?<\/figure>/, function () {
      var language = RegExp.$1 || 'plain'
      var lastMatch = RegExp.lastMatch
      lastMatch = lastMatch.replace(/<figure class="highlight /, '<figure class="iseeu highlight /')
      return '<div class="highlight-wrap"' + attributesStr + 'data-rel="' + language.toUpperCase() + '">' + lastMatch + '</div>'
    })
  }
  return data
})

```

# highlight.styl配置

## 创建`macPanel.styl`

`~/themes/next/source/css/_common/scaffolding/highlight/`下创建`macPanel.styl`。

```css
.highlight-wrap[data-rel] {
  position: relative;
  overflow: hidden;
  border-radius: 5px;
  box-shadow: 0 10px 30px 0px rgba(0,0,0,0.4);
  margin: 35px 0;
  ::-webkit-scrollbar {
    height: 10px;
  }

  ::-webkit-scrollbar-track {
      -webkit-box-shadow: inset 0 0 6px rgba(0,0,0,0.3);
      border-radius: 10px;
  }

  ::-webkit-scrollbar-thumb {
      border-radius: 10px;
      -webkit-box-shadow: inset 0 0 6px rgba(0,0,0,0.5);
  }
  &::before {
    color: white;
    content: attr(data-rel);
    height: 38px;
    line-height: 38px;
    background: #21252b;
    color: #fff;
    font-size: 16px;
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    font-family: 'Source Sans Pro', sans-serif;
    font-weight: bold;
    padding: 0px 80px;
    text-indent: 15px;
    float: left;
  }
  &::after {
    content: " ";
    position: absolute;
    -webkit-border-radius: 50%;
    border-radius: 50%;
    background: #fc625d;
    width: 12px;
    height: 12px;
    top: 0;
    left: 20px;
    margin-top: 13px;
    -webkit-box-shadow: 20px 0px #fdbc40, 40px 0px #35cd4b;
    box-shadow: 20px 0px #fdbc40, 40px 0px #35cd4b;
    z-index: 3;
  }
}
```

## 引入`macPanel.styl`

`~/themes/next/source/css/_common/scaffolding/highlight/highlight.styl`文件顶部添加`@require "macPanel"`。

```diff
// https://github.com/chriskempson/tomorrow-theme
$highlight-theme = hexo-config('codeblock.highlight_theme');

@import 'theme';
@import 'diff';

@import 'copy-code' if (hexo-config('codeblock.copy_button.enable'));

+ @require "macPanel"
```

# 主题配置文件配置

`~/themes/next/source/_config.yml`中修改`highlight_theme`为自己想要的样式。