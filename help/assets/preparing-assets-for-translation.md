---
title: 准备要翻译的资产
description: 创建语言根文件夹以准备要翻译的资产以支持多语言资产。
contentOwner: AG
translation-type: tm+mt
source-git-commit: a39ee0f435dc43d2c2830b2947e91ffdcf11c7f6

---


# 准备要翻译的资产 {#preparing-assets-for-translation}

多语言资源是指具有多语言二进制文件、元数据和标记的资源。 通常，资产的二进制文件、元数据和标记以一种语言存在，然后将它们翻译为其他语言，以便在多语言项目中使用。

在Adobe Experience Manager(AEM)资产中，多语言资产包含在文件夹中，其中每个文件夹都包含不同语言的资产。

每个语言文件夹都称为语言副本。 语言副本的根文件夹（称为语言根）标识语言副本中内容的语言。 例如， */content/dam/it是意大利语副本的意大利语根语言* 。 语言副本必须使用 [正确配置的语言根目录](preparing-assets-for-translation.md#creating-a-language-root) ，以便在执行源资产翻译时瞄准正确的语言。

您最初为其添加资产的语言副本是语言母版。 语言母版是翻译成其他语言的源。 示例文件夹层次结构包括多个语言根：

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

执行以下步骤以准备要翻译的资产：

1. 创建语言母版的语言根。 例如，示例文件夹层次结构中英语副本的语言根目录为 `/content/dam/en`。 确保根据“创建语言根”中的信息正确配置 [了语言根](preparing-assets-for-translation.md#creating-a-language-root)。

1. 将资源添加到您的语言母版。
1. 创建您需要语言副本的每个目标语言的语言根。

## 创建语言根 {#creating-a-language-root}

要创建语言根目录，请创建一个文件夹，并使用ISO语言代码作为“名称”属性的值。 创建语言根目录后，可以在语言根目录的任何级别创建语言副本。

例如，示例层次结构的意大利语语言副本的根页面 `it` 作为“名称”属性。 名称属性将用作存储库中资产节点的名称，因此会确定资产的路径。(`https://[aem_server]:[port]/assets.html/content/dam/it/`)。

1. 在资产控制台中，单击／点按创 **[!UICONTROL 建]** ，然后从 **[!UICONTROL 菜单中选]** 择文件夹。

   ![创建文件夹](assets/Create-folder.png)

1. 在“名 **[!UICONTROL 称]** ”字段中，键入格式为的国家／地区代码 `<language-code>`。

   ![在文件夹中添加语言代码](assets/Add-language-code-in-folder.png)

1. 单击或点按&#x200B;**[!UICONTROL 创建]**。将在“资产”控制台中创建语言根目录。

## 查看语言根 {#viewing-language-roots}

AEM界面提供了一 **[!UICONTROL 个“引用]** ”面板，其中显示在AEM资产中创建的语言根列表。

1. 在“资产”控制台中，选择要为其创建语言副本的语言母版。
1. 单击或点按GlobalNav图标，然后选择“引 **[!UICONTROL 用]** ”以打开“引 [!UICONTROL 用] ”窗格。

   ![chlimage_1-122](assets/chlimage_1-122.png)

1. 在“引用”窗格中，单击或点按 **[!UICONTROL 语言副本]**。 “语 [!UICONTROL 言副本] ”面板显示资产的语言副本。

   ![chlimage_1-123](assets/chlimage_1-123.png)
