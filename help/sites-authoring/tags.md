---
title: 使用标记
seo-title: 使用标记
description: 标记是用于对网站中的内容进行分类的简单快捷方法
seo-description: 标记是用于对网站中的内容进行分类的简单快捷方法
uuid: 5d922443-f924-426e-acf4-27dffd1053f6
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 9fb6d603-eb17-4192-bfa6-6c316f14ac7d
docset: aem65
translation-type: tm+mt
source-git-commit: 52cb99353ae33c8097b6b5bd29f6c040df30b42d
workflow-type: tm+mt
source-wordcount: '584'
ht-degree: 84%

---


# 使用标记{#using-tags}

标记是用于对网站中的内容进行分类的简单快捷方法。可以将标记视为可附加到页面、资产或其他内容，以便在进行搜索时能够找到该内容及相关内容的关键字或标签。

* See [Administering Tags](/help/sites-administering/tags.md) for information about creating and managing tags, as well as to which content tags have been applied.
* See [Tagging for Developers](/help/sites-developing/tags.md) for information about the tagging framework as well as including and extending tags in custom applications.

## 使用标记的十大理由 {#ten-reasons-to-use-tagging}

1. **组织内容** - 标记使作者的工作更轻松，因为他们可以轻而易举地快速组织内容。
1. **组织标记** - 使用标记组织内容时，层次分类/命名空间会组织标记。
1. **深度组织标记** - 有了创建标记和子标记的功能，就可以表示整个分类系统，其中涵盖术语、子术语及其关系。这允许您创建与正式内容层次结构平行的第二个（或第三个）内容层次结构。
1. **控制标记** - 可以通过对标记和/或命名空间应用权限来控制标记创建和应用，从而控制标记。
1. **灵活标记** - 标记有许多名称和面孔：标记、分类术语、类别、标签等等。标记的内容模型和使用方式很灵活；例如，在概括目标人口统计、对内容进行分类或评级，或者创建辅助内容层次结构时，均可使用标记。
1. **改进搜索** - AEM 中的默认搜索组件包含大量已创建的标记和已应用的标记，可以对其应用筛选器以将结果缩小到相关范围。
1. **启用 SEO** - 作为页面属性应用的标记将自动显示在页面的元标记中，以对搜索引擎可见。
1. **化繁为简** - 可以简单地通过一个词语和触摸按钮来创建标记。之后，可以添加标题、描述和无限数量的标签以向标记提供更多语义。
1. **核心一致性** - 标记系统是 AEM 的核心组件，可供所有 AEM 功能用来对内容分类。此外，开发人员可以使用标记 API 来创建支持标记的应用程序，以便访问相同的分类。
1. **结构化与灵活性相结合** - 鉴于对页面和路径的嵌套，AEM 非常适合处理结构化信息。凭借内置的全文搜索功能，它在处理非结构化信息时也非常强大。标记兼具结构化和灵活性的强大优势。

在设计站点的内容结构和资产的元数据架构时，请考虑使用标记提供的轻量级可行方法。

## 应用标记 {#applying-tags}

在创作环境中，作者可以通过访问页面属性并在&#x200B;**标记/关键字**&#x200B;字段中输入一个或多个标记来应用标记。

To apply [pre-defined tags](/help/sites-administering/tags.md), in the **Page Properties** window use the **Tags** field and the **Select Tags** window. **标准标记**&#x200B;选项卡是默认的命名空间，这意味着分类前面没有 `namespace-string:` 前缀。

![选择“标记”窗口； 使用X按钮取消选择当前选定的标记](assets/chlimage_1-41.png)

### 发布标记 {#publishing-tags}

与页面一样，您可以对标记和命名空间执行以下操作：

**激活**

* 激活单个标记。

   与页面一样，新创建的标记需要先激活，然后才能在发布环境中使用。

>[!NOTE]
>
>激活页面时，会自动打开一个对话框，通过该对话框可以激活属于该页面的未激活标记。

**取消激活**

* 取消激活选定标记。
