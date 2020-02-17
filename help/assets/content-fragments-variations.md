---
title: 变量——创作片段内容
seo-title: 变量——创作片段内容
description: 变量允许您为片段创作内容，然后根据用途创建该内容的变量（如果需要）。
seo-description: 变量允许您为片段创作内容，然后根据用途创建该内容的变量（如果需要）。
uuid: 0844f271-79bc-4f76-8031-d388b81d6feb
contentOwner: Alison Heimoz
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: content-fragments
content-type: reference
discoiquuid: 324df1da-78fa-460f-a744-3504259f1d4a
docset: aem65
translation-type: tm+mt
source-git-commit: 9d5fa8b85f6724097e34edd66745e0daf95d66cc

---


# 变量——创作片段内容{#variations-authoring-fragment-content}

[变体](/help/assets/content-fragments.md#constituent-parts-of-a-content-fragment) 是内容片段的重要功能，因为它们允许您创建和编辑主内容的副本以用于特定渠道和／或场景。

在“变 **量** ”选项卡中，您可以：

* [输入片段的内容](#authoring-your-content) ,
* [创建和管理主内容](#managing-variations) 的 **变体** 。

根据所编辑的数据类型执行一系列其他操作；例如：

* [将可视资产插入片段](#inserting-assets-into-your-fragment) （图像）
* 在富文 [本](#rich-text)、纯文 [本和标记之](#plain-text) 间进行选 [择](#markdown) ，以进行编辑

* [上传内容](#uploading-content)

* [查看主要统计](#viewing-key-statistics) （关于多行文本）
* [总结文本](#summarizing-text)

* [使变体与主内容同步](#synchronizing-with-master)

>[!CAUTION]
>
>在发布和／或引用片段后，当作者打开片段以再次进行编辑时，AEM将显示一条警告消息。 这将警告对片段所做的更改也会影响引用的页面。

## 创作内容 {#authoring-your-content}

打开内容片段进行编辑时，默认情 **况下** ,“变量”选项卡将打开。 您可以在此处为主视图或您拥有的任何变体创作内容。 您可以：

* 直接在“变量”(Variations)选项 **卡中进行编** 辑
* 打开全 [屏编辑器](#full-screen-editor) :

   * 选择格 [式](#formats)
   * 查看更多编辑选项(富 [文本格式](#rich-text) )

   * 访问一系列操 [作](#actions)

例如：

* 编辑简单片段

   一个简单的片段由一个多行文本字段组成（可以从全屏编辑器添加可视资产）。

   ![cfm-6420-21](assets/cfm-6420-21.png)

* 使用结构化内容编辑片段

   结构化片段包含在内容模型中定义的各种数据类型的字段。 对于任何多行字段， [全屏编辑器](#full-screen-editor) 均可用。

   ![cfm-6420-16](assets/cfm-6420-16.png)

### 全屏编辑器 {#full-screen-editor}

编辑多行文本字段时，可以打开全屏编辑器：

![cf-fullscreeneditor-icon](assets/cf-fullscreeneditor-icon.png)

全屏编辑器提供：

* 访问各种操 [作](#actions)
* 根据格式 [](#formats)，其他格式选项(富[文本](#rich-text))

### 操作 {#actions}

当全屏编辑器（即多行文本）打开时， [(对于所有格式](#formats))也可以执行以下操作：

* 选择格 [式](#formats) ([富文本](#rich-text)、纯文 [本、标](#plain-text) 记 [](#markdown))

* [显示文本统计信息](#viewing-key-statistics)

* [上传内容](#uploading-content)
* [与主页同步](#synchronizing-with-master) （编辑变量时）
* [总结文本](#summarizing-text)
* [在文本中添加注释](/help/assets/content-fragments-variations.md#annotating-a-content-fragment) ,

* [将可视资产插入片段](#inserting-assets-into-your-fragment) （图像）

### 格式 {#formats}

用于编辑多行文本的选项取决于所选的格式：

* [富文本](#rich-text)
* [纯文本](#plain-text)
* [Markdown](#markdown)

在全屏编辑器时，可以选择格式。

### 富文本 {#rich-text}

富文本编辑允许您设置格式：

* 粗体
* 斜体
* 下划线
* 对齐：左，中，右
* 项目符号列表
* 编号列表
* 缩进：增加，减少
* 创建／断开超链接
* 打开全屏编辑器，其中提供以下格式选项：

   * 粘贴文本／从Word
   * 插入表
   * 段落样式：段落，标题1/2/3
   * [插入可视资源](#inserting-assets-into-your-fragment)
   * 搜索
   * 查找/替换
   * 拼写检查器
   * [注释](/help/assets/content-fragments-variations.md#annotating-a-content-fragment)

操 [作也可](#actions) 从全屏编辑器访问。

### 纯文本 {#plain-text}

纯文本允许快速输入内容，而无需格式化或标记信息。 您还可以打开全屏编辑器以执行进一步 [操作](#actions)。

>[!CAUTION]
>
>如果选择 **纯文本** ，您可能会丢失已插入富文本或标记中的任何格式、标记和／或资 **源******。

### Markdown {#markdown}

>[!NOTE]
>
>有关完整信息，请参 [阅Markdown](/help/assets/content-fragments-markdown.md) 文档。

这允许您使用标记设置文本格式。 您可以定义：

* 标题
* 段落和换行
* 链接
* 图像
* 块引号
* 列表
* 重点
* 代码块
* 反斜杠转义

您还可以打开全屏编辑器以执行进一步 [操作](#actions)。

>[!CAUTION]
>
>如果在富文本和 **Markdown之间切换****** ，您可能会在块引号和代码块中遇到意外的效果，因为这两种格式在处理这些格式时可能会有所不同。

### 查看关键统计信息 {#viewing-key-statistics}

当全屏编辑器打开时，“文本统计 **信息** ”动作将显示有关文本的一系列信息。 例如：

![cfx-6420-22](assets/cfx-6420-22.png)

### 上传内容 {#uploading-content}

要简化内容片段的创作过程，您可以上传在外部编辑器中准备的文本，并将其直接添加到片段。

### 摘要文本 {#summarizing-text}

摘要文本旨在帮助用户将其文本的长度缩短为预定义的单词数，同时保留关键点和总体含义。

>[!NOTE]
>
>在技术层面上，系统根据具体算法保留其评分的句子，以提供 *信息密度和唯一性的最佳比率* 。

>[!CAUTION]
>
>内容片段必须具有有效的语言（ISO代码）文件夹作为祖代；这用于确定要使用的语言模型。
>
>例如， `en/` 如以下路径所示：
>
>`/content/dam/my-brand/en/path-down/my-content-fragment`

>[!CAUTION]
>
>现成提供英语。
>
>包共享中的语言模型包提供了其他语言：
>
>* [法语(fr)](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq630/product/smartcontent-model-fr)
>* [德语(de)](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq630/product/smartcontent-model-de)
>* [意大利语(it)](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq630/product/smartcontent-model-it)
>* [西班牙语(es)](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq630/product/smartcontent-model-es)
>



1. 选择“ **主** ”或所需的变体。
1. 打开全屏编辑器。

1. 从工 **具栏中选择** “摘要”文本。

   ![cf-17](assets/cf-17.png)

1. 指定目标单词数，然后选择“开 **始”**:
1. 原始文本与建议的摘要并排显示：

   * 任何要删除的句子都以红色突出显示，并带有删除。
   * 单击任何高亮显示的句子，将其保留在摘要内容中。
   * 单击任何未高亮显示的句子以将其删除。
   ![cfm-6420-23](assets/cfm-6420-23.png)

1. 选择 **摘要** ，以确认更改。

### 对内容片段添加注释 {#annotating-a-content-fragment}

要注释片段，请执行以下操作：

1. 选择“ **主** ”或所需的变体。
1. 打开全屏编辑器。
1. 选择一些文本。 “注 **释** ”(Annotate)图标变为可用。

   ![cfm-6420-24](assets/cfm-6420-24.png)

1. 此时将打开一个对话框。您可以在此输入注释。

1. 关闭全屏编辑器并 **保存** 片段。

### 查看、编辑和删除注释 {#viewing-editing-deleting-annotations}

注释:

* 在编辑器的全屏和正常模式下，文本上的高亮显示指示。 然后，可通过单击高亮显示的文本来查看、编辑和／或删除注释的完整详细信息，该文本将重新打开对话框。

   >[!NOTE]
   >
   >如果对一个文本应用了多个注释，则会提供下拉选择器。

* 当您删除应用了注释的整个文本时，注释也会被删除。

* 通过选择片段编辑器中的“注释”选项 **卡** ，可以列出和删除这些内容。

   ![cfm-6420-25](assets/cfm-6420-25.png)

* 可在选定片段的时间轴中查 [看](/help/assets/content-fragments-managing.md#timeline-for-content-fragments) 、删除这些片段。

### 将资产插入片段 {#inserting-assets-into-your-fragment}

要简化内容片段的创作过程，您可以直接 [将资产](/help/assets/managing-assets-touch-ui.md) （图像）添加到片段。

将它们添加到片段的段落序列中，而无需任何格式；在页面上使用／引 [用片段时，可以执行格式设置](/help/sites-authoring/content-fragments.md)。

>[!CAUTION]
>
>不能在引用页面上移动或删除这些资产，这必须在片段编辑器中完成。
>
>但是，必须在页面编辑器中完成资产的格式化(例如 [大小)](/help/sites-authoring/content-fragments.md)。 资产在片段编辑器中的表示形式仅用于创作内容流。

>[!NOTE]
>
>There are various methods of adding [images](/help/assets/content-fragments.md#fragments-with-visual-assets) to the fragment and/or page.

1. 将光标定位到要添加图像的位置。
1. 使用插入 **资产图标** ，打开搜索对话框。

   ![cf-insertasset-icon](assets/cf-insertasset-icon.png)

1. 在对话框中，您可以：

   * 在DAM中导航到所需的资产
   * 在DAM中搜索资产
   找到后，单击缩略图以选择所需的资产。

1. 使用 **选择** ，将资产添加到您的内容片段的当前位置的段落系统中。

   >[!CAUTION]
   >
   >如果在添加资产后，您将格式更改为：
   >
   >* **纯文本**:资产将从片段中完全丢失。
   >* **Markdown**:资产将不可见，但在您返回富文本时仍将 **存在**。


## 管理变量 {#managing-variations}

### 创建变量 {#creating-a-variation}

各种变量允许您获取主 **内容** ，并根据用途（如果需要）进行更改。

要创建新变体，请执行以下操作：

1. 打开片段，确保侧面板可见。
1. 从侧 **面板的图标栏中** ，选择“变量”。
1. 选择“ **创建变量**”。
1. 将打开一个对话框，为新变 **体指** 定 **标题和说** 明。
1. 选择 **添加**;片段 **主** (Master)将被复制到新变体中，该变体现在打开进行 [编辑](#editing-a-variation)。

   >[!NOTE]
   >
   >创建新变体时，始终是被复 **制的Master** ，而不是当前打开的变体。

### 编辑变量 {#editing-a-variation}

您可以在以下任一操作之后更改变体内容：

* [创建变体](#creating-a-variation)。
* 打开现有片段，然后从侧面板中选择所需的变体。

![cfm-6420-26](assets/cfm-6420-26.png)

### 重命名变量 {#renaming-a-variation}

重命名现有变量：

1. 打开片段，然后从侧 **面板中** 选择变量。
1. 选择所需的变体。
1. 从“ **操作** ”(Actions **)下拉框** 中选择“重命名”(Rename)。

1. 在生成的对 **话框中** ，输入新的 **标题和** /或说明。

1. 确认重 **命名** 。

>[!NOTE]
>
>这仅影响变体标 **题**。

### 删除变量 {#deleting-a-variation}

要删除现有变体，请执行以下操作：

1. 打开片段，然后从侧 **面板中** 选择变量。
1. 选择所需的变体。
1. 从“ **操作** ”下拉 **框中选择** “删除”。

1. 在对话 **框中确** 认删除操作。

>[!NOTE]
>
>无法删除主 **视图**。

### 与主同步 {#synchronizing-with-master}

**主** (Master)是内容片段的一个组成部分，根据定义，它包含内容的主副本，而变体包含该内容的个别更新和定制版本。 更新主视图时，这些更改可能也与变体相关，因此需要传播到它们。

编辑变量时，您有权访问将变量的当前元素与主元素同步的操作。 这允许您将对主视图所做的更改自动复制到所需的变体。

>[!CAUTION]
>
>同步仅可将更改从主 *版&#x200B;**本复制**到变体*。
>
>将仅同步变量的当前元素。
>
>同步仅适用于多 **行文本数据类型** 。
>
>将更改 *从变体传输到&#x200B;**主&#x200B;***(Master)不提供此选项。

1. 在片段编辑器中打开内容片段。 确保主 **页** 已编辑。
1. 从以下任一位置选择特定的变体，然后选择相应的同步操作：

   * 操 **作下拉选择器** -将当前元素 **与主元素同步**

   * 全屏编辑器的工具栏——与主 **页同步**

1. 主视图和变体将并排显示：

   * 绿色表示已添加（到变量）的内容
   * 红色表示内容已删除（从变量中）
   ![cfm-6420-27](assets/cfm-6420-27.png)

1. 选择 **同步**，变体将更新并显示。

