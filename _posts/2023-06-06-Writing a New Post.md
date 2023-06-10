---
title: 教程一：文章元数据设置
author: cotes
date: 2023-06-06 14:10:00 +0800
categories: [博客教程]
tags: [教程]
render_with_liquid: false
image:
  path: /assets/images/devices-mockup.png
  lqip: data:image/webp;base64,UklGRpoAAABXRUJQVlA4WAoAAAAQAAAADwAABwAAQUxQSDIAAAARL0AmbZurmr57yyIiqE8oiG0bejIYEQTgqiDA9vqnsUSI6H+oAERp2HZ65qP/VIAWAFZQOCBCAAAA8AEAnQEqEAAIAAVAfCWkAALp8sF8rgRgAP7o9FDvMCkMde9PK7euH5M1m6VWoDXf2FkP3BqV0ZYbO6NA/VFIAAAA
  alt: Responsive rendering of Chirpy theme on multiple devices.
---

本教程将指导您如何在 _Xiaoma_ 中编写文章，即使您之前使用过Jekyll，也值得阅读，因为许多功能需要设置特定的变量。

创建一个名为 `YYYY-MM-DD-TITLE.EXTENSION`{: .filepath} 的新文件，并将其放置在根目录的 `_posts`{: .filepath} 中。请注意，`EXTENSION`{: .filepath} 必须是 `md`{: .filepath} 和`markdown`{: .filepath} 中的一个。如果您想节省创建文件的时间，请考虑使用插件 [`Jekyll-Compose`](https://github.com/jekyll/jekyll-compose) 来完成此操作。

## 前言

基本上，在文章的顶部，您需要填写以下的 [前置元数据](https://jekyllrb.com/docs/front-matter/) ：

```yaml
---
title: TITLE
date: YYYY-MM-DD HH:MM:SS +/-TTTT
categories: [TOP_CATEGORIE, SUB_CATEGORIE]
tags: [TAG]     # 标签名称应始终使用小写字母
---
```

> 默认情况下，帖子的布局在Chirpy模板中已经默认设置为 `post` ，因此在Front Matter块中不需要添加 _layout_ 变量。这意味着您无需在每个帖子中重复定义 _layout_ 变量。模板会自动将新帖子应用于post布局。但是，如果您需要为特定帖子自定义布局，可以在Front Matter块中指定不同的布局值来覆盖默认设置。
{: .prompt-tip }

### 时区

为了准确记录发布日期，您不仅需要在 `_config.yml`{: .filepath} 文件中设置 `timezone`，还需要在文章的 Front Matter 块中的 `date` 变量中提供文章的时区信息。格式为 `+/-TTTT`，例如 `+0800`。

### 目录和标签

每篇文章的 `categories` 字段被设计为最多包含两个元素，而 `tags` 字段的元素数量可以是零到无穷多个。例如：

```yaml
---
categories: [Animal, Insect]
tags: [bee]
---
```

### 作者信息

通常情况下，文章的作者信息不需要在 _Front Matter_ 中填写，它们会默认从配置文件的 `social.name` 和 `social.links` 的第一个条目中获取。但是您也可以按如下方式覆盖默认设置：

在 `_data/authors.yml` 文件中添加作者信息（如果您的网站没有这个文件，请创建一个）。

```yaml
<author_id>:
  name: <full name>
  twitter: <twitter_of_author>
  url: <homepage_of_author>
```
{: file="_data/authors.yml" }

然后可以使用 `author` 来指定单个条目，或者使用 `authors` 来指定多个条目：

```yaml
---
author: <author_id>                     # for single entry
# or
authors: [<author1_id>, <author2_id>]   # for multiple entries
---
```

虽然如此，`author` 关键词也可以识别多个条目。

> 从 `_data/authors.yml` 文件{: .filepath }中读取作者信息的好处是页面将具有元标签  `twitter:creator`，这样可以丰富 [Twitter Cards](https://developer.twitter.com/en/docs/twitter-for-websites/cards/guides/getting-started#card-and-content-attribution) ，对于SEO也很有好处。
{: .prompt-info }

## 目录
默认情况下，文章右侧面板会显示目录（**T**able **o**f **C**ontents，TOC）。如果你想在全局范围内关闭目录，请打开 `_config.yml` 文件{: .filepath}，将变量 `toc` 的值设为 `false`。如果你想针对特定文章关闭目录，请在文章的[Front Matter](https://jekyllrb.com/docs/front-matter/)中添加以下内容：

```yaml
---
toc: false
---
```
## 评论

全局的评论开关由 `_config.yml` 文件{: .filepath} 中的变量 `comments.active` 定义。在该变量中选择一个评论系统后，所有文章的评论功能将会启用。

如果你想关闭特定文章的评论功能，请在文章的 **Front Matter** 中添加以下内容：

```yaml
---
comments: false
---
```

## 数学公式

出于网站性能的考虑，默认情况下不会加载数学公式功能。但是您可以通过以下方式启用它：

```yaml
---
math: true
---
```

## Mermaid

[**Mermaid**](https://github.com/mermaid-js/mermaid) 是一个出色的图表生成工具。要在您的文章中启用它，请在 YAML 块中添加以下内容：

```yaml
---
mermaid: true
---
```

然后，您可以像其他 Markdown 语言一样使用它：使用 ```` ```mermaid ```` 和 ```` ``` ```` 将图表代码括起来。

## 图片

### 标题

在图片的下一行使用斜体，它将成为标题并显示在图片底部：

```markdown
![img-description](/path/to/image)
_Image Caption_
```
{: .nolineno}

### 尺寸

为了避免页面内容在加载图片时发生布局变化，我们应该为每个图片设置宽度和高度。

```markdown
![Desktop View](/assets/img/sample/mockup.png){: width="700" height="400" }
```
{: .nolineno}

> 对于SVG图片，您至少需要指定它的 _width_，否则它将无法渲染。
{: .prompt-info }

从 _Chirpy v5.0.0_ 开始, `height` 和 `width` 支持缩写形式 (`height` → `h`, `width` → `w`)。 面的示例具有与上述示例相同的效果：

```markdown
![Desktop View](/assets/img/sample/mockup.png){: w="700" h="400" }
```
{: .nolineno}

### 位置

默认情况下，图片居中显示，但你可以通过使用 `normal`、`left` 和 `right` 中的一个类来指定位置。

> 一旦指定了位置，就不应该添加图片标题。
{: .prompt-warning }

- **正常位置**

  在下面的示例中，图片将左对齐：

  ```markdown
  ![Desktop View](/assets/images/mockup.png){: .normal }
  ```
  {: .nolineno}

- **左浮动**

  ```markdown
  ![Desktop View](/assets/images/mockup.png){: .left }
  ```
  {: .nolineno}

- **右浮动**

  ```markdown
  ![Desktop View](/assets/images/mockup.png){: .right }
  ```
  {: .nolineno}

  ### 深色/浅色模式

您可以使图像根据深色/浅色模式进行切换。这需要您准备两个图像，一个用于深色模式，一个用于浅色模式，并为它们分配特定的类（ `dark` 或 `light` ）：

```markdown
![Light mode only](/path/to/light-mode.png){: .light }
![Dark mode only](/path/to/dark-mode.png){: .dark }
```

### 阴影

程序窗口的截图可以考虑显示阴影效果：

```markdown
![Desktop View](/assets/img/sample/mockup.png){: .shadow }
```
{: .nolineno}

### CDN URL

如果您将图像托管在CDN上，您可以通过分配 `_config.yml`{: .filepath} 文件中的 `img_cdn` 变量来节省重复编写CDN URL的时间：

```yaml
img_cdn: https://cdn.com
```
{: file='_config.yml' .nolineno}

一旦分配了 `img_cdn`，CDN URL 将会添加到所有以 `/ ` 开头的图像路径（网站头像和文章中的图像）中。

例如，在使用图像时：

```markdown
![The flower](/path/to/flower.png)
```
{: .nolineno}

解析结果会自动在图像路径之前添加 CDN 前缀 `https://cdn.com`：

```html
<img src="https://cdn.com/path/to/flower.png" alt="The flower">
```
{: .nolineno }

### 图像路径

当一篇文章包含许多图片时，反复定义图片路径将是一项耗时的任务。为了解决这个问题，我们可以在文章的 YAML 块中定义路径：

```yml
---
img_path: /img/path/
---
```

然后，在 Markdown 的图片源中可以直接写入文件名：

```md
![The flower](flower.png)
```
{: .nolineno }

输出结果将会是：

```html
<img src="/img/path/flower.png" alt="The flower">
```
{: .nolineno }

### 预览图像

如果您想在文章顶部添加一张图片，请提供一张分辨率为 `1200 x 630` 的图片。请注意，如果图片的长宽比不符合 `1.91:1`，图片将被缩放和裁剪。

了解了这些先决条件，您可以开始设置图片的属性：

```yaml
---
image:
  path: /path/to/image
  alt: image alternative text
---
```

请注意，[`img_path`]() 也可以传递给预览图像，也就是说，如果已经设置了该属性，`path` 属性只需提供图片的文件名。

对于简单使用，您也可以直接使用 `image` 来定义图片的路径：

```yml
---
image: /path/to/image
---
```

### LQIP

对于预览图像：

```yaml
---
image:
  lqip: /path/to/lqip-file # or base64 URI
---
```

> 您可以在文章 [_Text and Typography_](/posts/text-and-typography/) 的预览图像中观察到 LQIP。


对于普通图像：

```markdown
![Image description](/path/to/image){: lqip="/path/to/lqip-file" }
```
{: .nolineno }

## 置顶文章

您可以将一个或多个文章固定在主页的顶部，固定的文章按发布日期的相反顺序进行排序。启用方法如下：

```yaml
---
pin: true
---
```

## 提示

有几种类型的提示框：`tip`（提示）、`info`（信息）、`warning`（警告）和 `danger`（危险）。您可以通过在块引用中添加 `prompt-{type}` 类来生成相应类型的提示框。例如，以下是定义一个类型为 `info` 的提示框的示例：

```md
> 提示框示例行。
{: .prompt-info }
```
{: .nolineno }

## 语法

### 行内代码

```md
`inline code part`
```
{: .nolineno }

### 文件路径高亮

```md
`/path/to/a/file.extend`{: .filepath}
```
{: .nolineno }

### 代码块

Markdown 使用 ```` ``` ```` 符号可以轻松创建代码块，示例如下：

````md
```
This is a plaintext code snippet.
```
````

#### 指定语言

使用 ```` ```{language} ```` 可以获得带有语法高亮的代码块：

````markdown
```yaml
key: value
```
````

> Jekyll 标签 `{% highlight %}` 与该主题不兼容。
{: .prompt-danger }

#### 行号

默认情况下，除了 `plaintext`、`console` 和 `terminal` 之外的所有语言都会显示行号。如果要隐藏代码块的行号，请为其添加 `nolineno` 类：

````markdown
```shell
echo 'No more line numbers!'
```
{: .nolineno }
````

#### 指定文件名

您可能已经注意到代码块的顶部会显示代码语言。如果您想用文件名替换它，可以添加 `file` 属性来实现：

````markdown
```shell
# 内容
```
{: file="path/to/file" }
````

#### Liquid代码

如果您想显示 Liquid 代码片段，请使用 `{% raw %}` 和 `{% endraw %}` 将 Liquid 代码包围起来：

````markdown
{% raw %}
```liquid
{% if product.title contains 'Pack' %}
  This product's title contains the word Pack.
{% endif %}
```
{% endraw %}
````

或者在文章的 YAML 块中添加 `render_with_liquid: false` （要求 Jekyll 版本为 4.0 或更高）。

## 视频

您可以使用以下语法嵌入视频：

```liquid
{% include embed/{Platform}.html id='{ID}' %}
```
其中，`Platform` 是平台名称的小写形式，`ID` 是视频的唯一标识符。

下表展示了如何从给定的视频链接中获取这两个参数，同时您也可以了解当前支持的视频平台。

| 视频链接                                                                                          | 平台  | 视频ID            |
|----------------------------------------------------------------------------------------------------|-----------|:--------------|
| [https://www.**youtube**.com/watch?v=**H-B46URT4mg**](https://www.youtube.com/watch?v=H-B46URT4mg) | `youtube` | `H-B46URT4mg` |
| [https://www.**twitch**.tv/videos/**1634779211**](https://www.twitch.tv/videos/1634779211)         | `twitch`  | `1634779211`  |

请根据视频链接中的平台和视频ID，替换上述语法中的 `{Platform}` 和 `{ID}` 部分。


## 了解更多

要了解更多关于Jekyll文章的知识，请访问[Jekyll文档：文章](https://jekyllrb.com/docs/posts/)。
