---
title: 更改HTML5表单的默认样式
seo-title: 更改HTML5表单的默认样式
description: HTML5表单样式基于CSS。 您可以更改表单的默认样式。
seo-description: HTML5表单样式基于CSS。 您可以更改表单的默认样式。
uuid: 5e23237d-42d8-4d29-b79e-4dc276ef65ff
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 582b0fe8-a92b-4a1d-b859-57f13f53d0d8
docset: aem65
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317

---


# 更改HTML5表单的默认样式{#changing-default-styles-of-html-forms}

使用HTML5功能渲染HTML5表单，使用CSS完成渲染表单的样式设置。 HTML5表单的默认外观与其PDF再现类似。 开发人员可以使用自定义CSS更改HTML5表单的默认外观。

本文提供了更改HTML5表单样式的分步信息，而“样式简介”文章包含有关HTML5表单各种样式方面的 [详细信息](/help/forms/using/css-styles.md) 。 确保在执行本文中提到的步骤之前阅读样式文章的介绍。

以下两幅图像显示了默认样式和自定义样式之间的差异。

![图片-002-small](assets/pictures-002-small.png)

## 设置表单样式 {#style-your-forms}

1. **选择用户档案以添加自定义样式**

   访问URL上的CRX DE界面：https:// **&lt;server>:&lt;port>/crx/de** ，并创建用户档案或选择现有用户档案。 要了解如何创建用户档案，请参阅 [创建新用户档案](/help/forms/using/custom-profile.md)

1. **创建用于设置HTML5表单样式的CSS样式表**

   导览至创建用户档案渲染器的文件夹并创建CSS样式表文件。 要执行的步骤包括

   1. 右键单击文件夹，然后从菜 **单中选择** “ **创建文件** ”>“创建文件”

   1. 在创建文件对话框中，输入样式表的名称。 确保使用扩展名。css（例如stylesheet.css）
   1. 在导航窗格中，打开已创建的CSS文件。
   1. 定义要设置样式的组件的CSS类，并在这些类中添加样式。
   要了解要在HTML5表单中为特定组件创建哪些CSS类，请参 [阅样式介绍](/help/forms/using/css-styles.md)。

1. **在“用户档案渲染器”中包含样式表**

   在CRX DE中打开“用户档案渲染器”页（jsp文件），并将CSS文件包含在XFA客户端库正下方的页面中。 执行这些步骤以将CSS文件包含在用户档案中。

   1. 在渲染器页面中搜索以下行：

      &lt;cq:includeClientLib类别=&quot;xfaforms.用户档案&quot; />

   1. 在上面的行下方插入以下内容以包含样式表：

      &lt;link href=&quot;/path/to/stylesheet&quot; rel=&quot;stylesheet&quot; type=&quot;text/css&quot;/>

   1. 保存文件。
