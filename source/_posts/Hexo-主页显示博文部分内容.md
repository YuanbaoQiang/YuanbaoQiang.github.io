---
title: 'Hexo 主页显示博文部分内容'
date: 2020-07-11 21:44:29
tags: Hexo
categories: Hexo 美化
description: 本文讲述了让博文在主页部分显示的三种方法。
---

> Next默认是会显示全文的，这样显然很不方便，因此需要一些方法去只显示前面一部分。

<!--more-->

# 配置修改

Next主题的_config.yml文件找到如下：

```bash
# Automatically excerpt description in homepage as preamble text.
excerpt_description: true
```

> 默认为打开状态

# 方法一：添加Description

对博文的`front-matter`进行`Description`描述，之后该博文在主页中只显示Description内容。

```markdown
---
title: #标题
date: #博文的创建时间
description: #本博文的描述
---
```



# 方法二：设置截断点

在需要显示的内容后插入代码：

```markdown
这是博文在主页上显示的内容
<!--more-->
这是点击readmore之后显示的内容
```

# 方法三：自动截断

打开 themes/ 目录下的对应的主题的theme文件夹下的 `_config.yml` 文件，找到这段代码，如果没有则新建，可能不同的主题会不支持这种方法：

```bash
# Automatically Excerpt. Not recommend.
# Please use <!-- more --> in the post to control excerpt accurately.
  auto_excerpt:
	enable: false
    length: 150
```

> 我的Next主题是没有成功。

个人推荐的话用前两种方法，尤其是Description，类似于论文的Abstract，可以让人很清楚的这篇博文讲的是啥。

# 参考

[设置hexo首页只显示部分摘要（不显示全文）](https://blog.csdn.net/yueyue200830/article/details/104470646)

[让hexo的首页只显示文章的部分内容而不是全部](https://rogchen.github.io/2019/09/16/hexo-more/)