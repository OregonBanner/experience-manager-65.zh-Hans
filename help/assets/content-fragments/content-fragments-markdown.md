---
title: Markdown
seo-title: Markdown
description: 在创作时，内容片段编辑器使用Markdown语法来让您轻松编写内容。
seo-description: 在创作时，内容片段编辑器使用Markdown语法来让您轻松编写内容。
uuid: afcbf82f-3a75-4491-9172-706188db65bb
contentOwner: Alison Heimoz
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: content-fragments
content-type: reference
discoiquuid: b193f28c-46c2-4eab-bbb8-578530f80ba5
docset: aem65
feature: 内容片段
role: Business Practitioner, Administrator
exl-id: 28e1052f-62b5-47bc-9bc8-f2d92f0254f6
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '541'
ht-degree: 4%

---

# Markdown{#markdown}

当您处于[创作](content-fragments-variations.md#authoring-your-content)时，内容片段编辑器会使用&#x200B;*markdown*&#x200B;语法来轻松编写内容：

![markdown编辑器](/help/assets/content-fragments/assets/cfm-6420-08.png)

您可以定义：

* [标题符号](/help/assets/content-fragments/content-fragments-markdown.md#heading-notation)
* [段落和换行符](/help/assets/content-fragments/content-fragments-markdown.md#paragraphs-and-line-breaks)
* [链接](/help/assets/content-fragments/content-fragments-markdown.md#links)
* [图像](/help/assets/content-fragments/content-fragments-markdown.md#images)
* [块引号](/help/assets/content-fragments/content-fragments-markdown.md#block-quotes)
* [列表](/help/assets/content-fragments/content-fragments-markdown.md#lists)
* [强调](/help/assets/content-fragments/content-fragments-markdown.md#emphasis)
* [代码块](/help/assets/content-fragments/content-fragments-markdown.md#code-blocks)
* [反斜线转义](/help/assets/content-fragments/content-fragments-markdown.md#backslash-escapes)

## 标题符号{#heading-notation}

要通过在标题前面放置井号(#)来创建标题，请执行以下操作： 一个哈希标记(#)用于H1，两个哈希标记(##)用于H2等。 您最多可以使用6个哈希标记。 例如：

    `## This is an H2`

    `### This is an H3`

    `###### This is a H6`

或者，您也可以通过以等号加下划线来创建H1，并通过以减号加下划线来创建H2。 例如：

    `This is an H1`

    `=============`

    `This is an H2`

    `-------------`

## 段落和换行符{#paragraphs-and-line-breaks}

段落只是一行或多行连续的文本，用一行或多行空白行分隔。 空行是只包含空格或制表符的行。 不应使用空格或制表符缩进普通段落。

换行符的创建方法是：在返回后，用两个或多个空格结束一行。

## 链接 {#links}

您可以创建内联链接和引用链接。

在这两种样式中，链接文本都由方括号`[]`分隔。

以下是内联链接的示例：

    `This is [an example](https://example.com/ "Title") inline link.`

    `This is [an example of an email link](emailto:myaddress@mydomain.info)`

    `[This link](https://example.net/) has no title attribute.`

引用链接的语法如下：

    `Hey you should [checkout][0] this [cool thing][wiki] that I [made][].`

    `[0]: https://www.google.ca`

    `[wiki]: https://www.wikipedia.org`

    `[made]: https://www.stackoverflow.com`

## 图像 {#images}

图像的语法与链接类似。 您可以创建内联和引用的图像。

例如，内联图像的语法如下：

    `![Alt text](/path/to/img.jpg)`

    `![Alt text](/path/to/img.jpg "Optional title")`

语法包括：

* 一个感叹号：!;
* 后跟一组方括号，其中包含图像的alt属性文本；
* 后跟一组括号（包含图像的URL或路径），以及一个可选的标题属性，它用双引号或单引号括起来。

引用样式图像的语法如下：

    `![Alt text][id]`

其中，“id”是定义的图像引用的名称。 图像引用是使用与链接引用相同的语法来定义的：

    `[id]: url/to/image "Optional title attribute"`

## 块引号{#block-quotes}

可以在文本前添加>符号来引用文本。 例如：

    `>This is block quotes`

    `>asdhfjlkasdhlf`

    `>asdfahsdlfasdfj`

您可以使用嵌套的块引号。 例如：

    `> This is the first level of quoting.`

    `>`

        `>> This is nested blockquote.`

    `>`

    `> Back to the first level.`

## 列表 {#lists}

您可以创建已排序和未排序的列表。

要创建无序列表，请使用&amp;ast;符号。 例如：

    `* item in list`

    `* item in list`

    `* item in list`

要创建有序列表，请在列表中每个项目之前添加数字，后跟一个句点。 例如：

    `1. First item in list.`

    `2. Second item in list.`

    `3. Third item in list.`

## 强调 {#emphasis}

您可以为文本添加斜体或粗体样式。

要按如下方式添加斜体，请执行以下操作：

    `*single asterisks*`

    `_single underscores_`

    `Keyboard shortcut: Ctrl-I (Cmd-I)`

您可以按如下方式显示粗体文本：

    `**double asterisks**`

    `__double underscores__`

    `Keyboard shortcut: Ctrl-B (Cmd-B)`

要指示代码跨度，请用反勾号(&#39;)将代码换行。 与预格式化的代码块不同，代码范围表示普通段落中的代码。

例如：

    ``Use the `printf()` function.``

## 代码块{#code-blocks}

代码块通常用于说明源代码。 您可以通过使用制表符缩进代码，或者最少使用4个空格来创建代码块。 例如：

    `This is a normal paragraph.`

        `This is a code block.`

## 反斜线转义{#backslash-escapes}

您可以使用反斜杠转义生成在格式语法中具有特殊含义的文字字符。 例如，如果您想要在单词周围加上文字星号（而不是HTML &lt;em>标记），则可以在星号之前使用反斜杠，如下所示：

    `\\*literal asterisks\\*`

反斜杠转义可用于以下字符：

    ` \ backslash`

    `` ` backtick``

    ` * asterisk`

    ` _ underscore`

    ` {} curly braces`

    ` [] square brackets`

    ` () parentheses`

    ` # hash mark`

    ` + plus sign`

    ` - minus sign (hyphen)`

    ` . dot`
