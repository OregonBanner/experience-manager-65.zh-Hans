---
title: 准备资产以进行翻译
description: 创建语言根文件夹以准备要翻译的资产以支持多语言资产。
contentOwner: AG
role: User, Admin
feature: 项目
exl-id: eee768e3-3eb4-46fa-b9ae-9ef8764a3a94
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '441'
ht-degree: 1%

---

# 准备资产以进行翻译 {#preparing-assets-for-translation}

多语言资产是指包含多种语言的二进制文件、元数据和标记的资产。 通常，资产的二进制文件、元数据和标记以一种语言存在，然后将这些语言翻译成其他语言，以用于多语言项目。

在[!DNL Adobe Experience Manager Assets]中，多语言资产包含在文件夹中，其中每个文件夹都包含使用不同语言的资产。

每个语言文件夹都称为语言副本。 语言副本的根文件夹（称为语言根）可标识语言副本中内容的语言。 例如，*/content/dam/it*&#x200B;是意大利语语言副本的意大利语根。 语言副本必须使用正确配置的语言根](preparing-assets-for-translation.md#creating-a-language-root)，以便在执行源资产的翻译时定位正确的语言。[

最初为其添加资产的语言副本是主要语言。 语言主语是翻译成其他语言的源。 示例文件夹层次结构包括多个语言根：

```shell
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

请执行以下步骤以准备资产以进行翻译：

1. 创建语言主目录的语言根目录。 例如，示例文件夹层次结构中英语语言副本的语言根目录为`/content/dam/en`。 确保根据[创建语言根](preparing-assets-for-translation.md#creating-a-language-root)中的信息正确配置语言根。

1. 将资产添加到主语言。
1. 创建您需要语言副本的每种目标语言的语言根目录。

## 创建语言根 {#creating-a-language-root}

要创建语言根目录，请创建一个文件夹并使用ISO语言代码作为Name属性的值。 创建语言根目录后，可以在语言根目录的任何级别创建语言副本。

例如，示例层次结构的意大利语语言副本的根页面具有`it`作为Name属性。 名称属性用作存储库中资产节点的名称，因此可确定资产的路径。(`https://[aem_server]:[port]/assets.html/content/dam/it/`)。

1. 从[!DNL Assets]控制台中，单击&#x200B;**[!UICONTROL 创建]**，然后从菜单中选择&#x200B;**[!UICONTROL 文件夹]**。

   ![创建文件夹](assets/Create-folder.png)

1. 在&#x200B;**[!UICONTROL 名称]**&#x200B;字段中，键入格式为`<language-code>`的国家/地区代码。

   ![在文件夹中添加语言代码](assets/Add-language-code-in-folder.png)

1. 单击&#x200B;**[!UICONTROL 创建]**。语言根目录在[!DNL Assets]控制台中创建。

## 查看语言根 {#viewing-language-roots}

[!DNL Experience Manager] 界面提供了一 **** 个“参考”面板，其中显示了在中创建的语言根列 [!DNL Assets]表。

1. 在[!DNL Assets]控制台中，选择要为其创建语言副本的语言主目录。
1. 从左边栏中，选择&#x200B;**[!UICONTROL 引用]**&#x200B;选项以打开[!UICONTROL 引用]窗格。

   ![chlimage_1-122](assets/chlimage_1-122.png)

1. 在引用窗格中，单击&#x200B;**[!UICONTROL 语言副本]**。 [!UICONTROL 语言副本]面板显示资产的语言副本。

   ![语言副本](assets/lang-copy2.png)
