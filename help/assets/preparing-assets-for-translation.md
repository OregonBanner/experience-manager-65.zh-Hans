---
title: 准备要翻译的资产
description: 创建语言根文件夹以准备要翻译的资产，从而支持多语言资产。
contentOwner: AG
role: User, Admin
feature: Projects
exl-id: eee768e3-3eb4-46fa-b9ae-9ef8764a3a94
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '440'
ht-degree: 1%

---

# 准备要翻译的资产 {#preparing-assets-for-translation}

多语言资源是指使用多种语言的二进制文件、元数据和标记的资源。 通常，资产的二进制文件、元数据和标记以一种语言存在，然后会翻译成其他语言以用于多语言项目。

In [!DNL Adobe Experience Manager Assets]，多语言资产包含在文件夹中，其中每个文件夹都包含不同语言的资产。

每个语言文件夹都称为语言副本。 语言副本的根文件夹（称为语言根）标识了语言副本中内容的语言。 例如， */content/dam/it* 是意大利语副本的意大利语根。 语言副本必须使用 [正确配置的语言根](preparing-assets-for-translation.md#creating-a-language-root) 以便在翻译源资产时定位正确的语言。

最初为其添加资产的语言副本是主要语言。 主要语言是翻译成其他语言的源。 示例文件夹层次结构包含多个语言根：

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

执行以下步骤来准备要翻译的资产：

1. 创建主要语言的语言根。 例如，示例文件夹层次结构中英语副本的语言根为 `/content/dam/en`. 确保根据中的信息正确配置了语言根 [创建语言根](preparing-assets-for-translation.md#creating-a-language-root).

1. 将资源添加到您的主要语言。
1. 为需要语言副本的每个目标语言创建语言根。

## 创建语言根 {#creating-a-language-root}

要创建语言根，您需要创建一个文件夹，并使用ISO语言代码作为Name属性的值。 创建语言根后，您可以在语言根的任何级别创建语言副本。

例如，示例层次结构的意大利语副本的根页面具有 `it` 作为Name属性。 Name属性用作存储库中资源节点的名称，从而确定资源的路径。(`https://[aem_server]:[port]/assets.html/content/dam/it/`)。

1. 从 [!DNL Assets] 控制台，单击 **[!UICONTROL 创建]** 并选择 **[!UICONTROL 文件夹]** 从菜单中。

   ![创建文件夹](assets/Create-folder.png)

1. 在 **[!UICONTROL 名称]** 字段输入国家/地区代码，格式为 `<language-code>`.

   ![在文件夹中添加语言代码](assets/Add-language-code-in-folder.png)

1. 单击&#x200B;**[!UICONTROL 创建]**。语言根创建于 [!DNL Assets] 控制台。

## 查看语言根 {#viewing-language-roots}

[!DNL Experience Manager] 界面提供 **[!UICONTROL 引用]** 显示已在其中创建的语言根列表的面板 [!DNL Assets].

1. 在 [!DNL Assets] 控制台中，选择要为其创建语言副本的主要语言。
1. 从左边栏中，选择 **[!UICONTROL 引用]** 用于打开 [!UICONTROL 引用] 窗格。

   ![chlimage_1-122](assets/chlimage_1-122.png)

1. 在“引用”窗格中，单击 **[!UICONTROL 语言副本]**. 此 [!UICONTROL 语言副本] 面板显示资产的语言副本。

   ![语言副本](assets/lang-copy2.png)
