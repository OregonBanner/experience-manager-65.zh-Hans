---
title: 准备要翻译的资产
description: 创建语言根文件夹以准备资产进行翻译以支持多语言资产。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 23d19d9656d61874cd00a9a2473092be0c53b8f8
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 0%

---


# 准备要翻译的资产 {#preparing-assets-for-translation}

多语言资产是指具有多语言二进制、元数据和标记的资产。 通常，资产的二进制文件、元数据和标记存在于一种语言中，然后将它们翻译为其他语言，以用于多语言项目。

在Adobe Experience Manager(AEM)资产中，多语言资产包含在文件夹中，其中每个文件夹都包含不同语言的资产。

每个语言文件夹都称为语言副本。 语言副本的根文件夹（称为语言根）标识语言副本中内容的语言。 例如， */content/dam/it* 是意大利语语言副本的意大利语根。 语言副本必须使用 [正确配置的语言根](preparing-assets-for-translation.md#creating-a-language-root) ，以在执行源资产翻译时锁定正确的语言。

您最初为其添加资产的语言副本是语言母版。 语言母版是翻译成其他语言的源。 示例文件夹层次结构包括几个语言根：

```
 /content
  /- dam
   |- en
   |- fr
   |- de
   |- es
   |- it
   |- ja
   |- zh
```

请执行以下步骤来准备要翻译的资产：

1. 创建语言母版的语言根。 例如，示例文件夹层次结构中英语副本的语言根目录为 `/content/dam/en`。 确保根据“创建语言根”中的信息正确 [配置语言根](preparing-assets-for-translation.md#creating-a-language-root)。

1. 将资源添加到语言母版。
1. 创建您需要语言副本的每种目标语言的语言根。

## 创建语言根 {#creating-a-language-root}

要创建语言根目录，请创建文件夹，并使用ISO语言代码作为“名称”属性的值。 创建语言根目录后，可以在语言根目录的任何级别创建语言副本。

例如，示例层次结构的意大利语语言副本的根页面 `it` 为“名称”属性。 名称属性用作存储库中资产节点的名称，因此会确定资产的路径。 (`https://[aem_server]:[port]/assets.html/content/dam/it/`)。

1. From the Assets console, click **[!UICONTROL Create]** and choose **[!UICONTROL Folder]** from the menu.

   ![创建文件夹](assets/Create-folder.png)

1. 在“名 **[!UICONTROL 称]** ”字段中，以格式键入国家／地区代码 `<language-code>`。

   ![在文件夹中添加语言代码](assets/Add-language-code-in-folder.png)

1. 单击&#x200B;**[!UICONTROL 创建]**。语言根目录在“资产”控制台中创建。

## 视图语根 {#viewing-language-roots}

AEM界面提供了 **[!UICONTROL 一个]** “引用”面板，其中显示在AEM资产中创建的语言根列表。

1. 在“资产”控制台中，选择要为其创建语言副本的语言母版。
1. 单击GlobalNav图标，然后选择“ **[!UICONTROL 引用]** ”以打开“ [!UICONTROL 引用] ”窗格。

   ![chlimage_1-122](assets/chlimage_1-122.png)

1. 在“引用”窗格中，单击“ **[!UICONTROL 语言副本”]**。 “语 [!UICONTROL 言副本] ”面板显示资产的语言副本。

   ![chlimage_1-123](assets/chlimage_1-123.png)
