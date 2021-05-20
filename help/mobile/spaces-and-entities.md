---
title: 空间和实体
seo-title: 开发AEM Mobile内容服务
description: 本页提供用于开发AEM Mobile内容服务的登陆页。
seo-description: 本页提供用于开发AEM Mobile内容服务的登陆页。
uuid: eab5a61b-a9e8-4863-90a3-df1f18510cd8
contentOwner: Jyotika Syal
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
discoiquuid: ef568577-c74e-4fc2-b66e-eedac2948310
exl-id: 44591900-b01b-4a33-9910-839564477e7d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1209'
ht-degree: 1%

---

# 空格和实体{#spaces-and-entities}

>[!NOTE]
>
>Adobe建议对需要基于单页应用程序框架的客户端渲染（例如React）的项目使用SPA编辑器。 [了解更多](/help/sites-developing/spa-overview.md)。

空间是存储通过内容服务REST API公开的实体的便捷位置。 这特别有用，因为应用程序（或任何渠道）可以与多个实体关联。 强制将实体置于空间内强制对应用程序要求进行分组的最佳实践。 或者，您也可以将AEM中的应用程序与少量空格关联。

>[!NOTE]
>
>要使内容服务中的任何渠道都可以使用某些内容，它需要位于空格下。

## 创建空格{#creating-a-space}

如果用户希望向移动设备应用程序显示大量内容和资产，则用户会使用AEM Mobile功能板创建空间。

对于首次将内容服务配置为使用空格的用户，AEM Mobile功能板仅在选择&#x200B;**Content Services**&#x200B;后显示应用程序。

>[!CAUTION]
>
>**添加空格的先决条件**
>
>选中&#x200B;**启用AEM Content Services**&#x200B;以使用空格，并在AEM Mobile应用程序功能板中启用它。
>
>有关更多详细信息，请参阅[管理内容服务](/help/mobile/developing-content-services.md)。

在功能板中配置空格后，请按照以下步骤创建空格：

1. 从“内容服务”中选择&#x200B;**空格**。

   ![chlimage_1-83](assets/chlimage_1-83.png)

1. 选择&#x200B;**创建**&#x200B;以创建空格。 输入空格的&#x200B;**标题**、**名称**&#x200B;和&#x200B;**描述**。

   单击&#x200B;**创建**。

   ![chlimage_1-84](assets/chlimage_1-84.png)

## 管理空间{#managing-a-space}

创建空间后，单击左侧以管理列表中的空间。

您可以查看空间的属性、删除空间，或将空间及其内容发布到AEM发布实例。

![chlimage_1-85](assets/chlimage_1-85.png)

**查看和编辑空间的属性**

1. 从列表中选择空格
1. 从工具栏中选择&#x200B;**属性**
1. 完成后，单击&#x200B;**关闭**

**发布空** 间发布空间时，该空间中的所有文件夹和实体也会发布。

1. 单击空间控制台列表中的空间图标以选择该空间
1. 选择&#x200B;**发布树**

>[!NOTE]
>
>您可以&#x200B;**取消发布**&#x200B;空间，这将从发布实例中删除该空间。
>
>下图说明了在发布空间后可以执行的操作。

![chlimage_1-86](assets/chlimage_1-86.png)

## 在空间{#working-with-folders-in-a-space}中使用文件夹

空间可以包含文件夹，以帮助进一步组织空间的内容和资产。 用户可以在空间下创建自己的层次结构。

### 创建文件夹{#creating-a-folder}

1. 单击空间控制台中列表中的空间，然后单击&#x200B;**创建文件夹**

   ![chlimage_1-87](assets/chlimage_1-87.png)

1. 输入文件夹的&#x200B;**标题**、**名称、**&#x200B;和&#x200B;**描述**

   ![chlimage_1-88](assets/chlimage_1-88.png)

1. 单击&#x200B;**创建**&#x200B;以在空间中创建文件夹

## 语言副本 {#language-copy}

>[!CAUTION]
>
>语言副本在此版本中功能不全。 它只设置结构。

**语言副本**&#x200B;功能允许作者复制其主控语言副本，然后创建项目和工作流以自动翻译内容。 语言副本创建正确的结构。 在空间中添加文件夹后，即可在空间中添加语言副本。

>[!NOTE]
>
>建议将任何可能已翻译的内容放在语言副本节点下。

### 添加语言副本{#adding-language-copy}

1. 创建空间后，单击该空间以创建语言副本。

   单击&#x200B;**创建**，然后选择&#x200B;**语言副本**。

   ![chlimage_1-89](assets/chlimage_1-89.png)

   >[!NOTE]
   >
   >语言副本节点只能作为空间的直接子节点存在。

1. 选择&#x200B;**内容包语言&amp;ast;**&#x200B;并在&#x200B;**创建语言副本**&#x200B;对话框中输入&#x200B;**标题&amp;ast;**。

   单击&#x200B;**创建**。

   ![chlimage_1-90](assets/chlimage_1-90.png)

1. 创建语言副本后，该副本会显示在&#x200B;**语言母版**&#x200B;的空间中。

   ![chlimage_1-91](assets/chlimage_1-91.png)

   >[!NOTE]
   >
   >选择&#x200B;**语言母版**&#x200B;以查看语言副本文件夹。

### 从空间{#removing-a-folder-from-the-space}中删除文件夹

1. 从空间内容列表中选择文件夹
1. 单击工具栏中的&#x200B;**删除**

   >[!NOTE]
   >
   >要导航到文件夹并查看其内容或添加子文件夹或实体，请在空间的内容列表中单击该文件夹的标题。

## 使用空格{#working-with-entities-in-a-space}中的实体

实体表示通过Web服务端点公开的内容。 实体存储在空格中，以便能够轻松找到并保持与包含其相关内容的AEM存储库结构无关。

您可能希望在某些逻辑收集中将实体分组在一起。 为此，您可以创建任意数量的文件夹。

如果为数据建模收集实体子项（即其他实体），则开发人员用户可以从提供的现成“实体组”模型类型创建特定的“组模型”。

>[!NOTE]
>
>实体始终与空间关联，因此大多数实体用户界面都通过空间控制台进行访问。

### 创建实体{#creating-an-entity}

1. 打开空间控制台，然后单击空间的标题。

   或者，您也可以通过单击列表中文件夹的标题来导航到该文件夹。

   ![chlimage_1-92](assets/chlimage_1-92.png)

1. 选择实体的模型。 这是要创建的实体类型。 单击下一步。

   ![chlimage_1-93](assets/chlimage_1-93.png)

   >[!NOTE]
   >
   >您可以选择&#x200B;**资产模型**、**页面模型**，或您之前创建的实体类型模型。
   >
   >请参阅[创建模型](/help/mobile/administer-mobile-apps.md)以创建自定义实体。

1. 为实体输入&#x200B;**标题**、**名称**、**描述**&#x200B;和&#x200B;**标记**。 单击&#x200B;**创建**。

   ![chlimage_1-94](assets/chlimage_1-94.png)

   完成后，实体将显示在空间的子体中。

### 编辑实体{#editing-an-entity}

1. 创建实体后，转到文件夹或空间，然后从空间控制台中选择要编辑的实体。

   ![chlimage_1-95](assets/chlimage_1-95.png)

1. 选择要编辑的实体，然后单击&#x200B;**编辑**。

   ![chlimage_1-96](assets/chlimage_1-96.png)

   >[!CAUTION]
   >
   >根据您选择创建实体的模板，用于编辑和查看实体属性的UI将因此而异。 有关更多详细信息，请参阅以下步骤。

   ***如果您选择用于将实体创建为资产模型的模板***，则单击编 **** 辑可添加资产，如下图所示：

   ![chlimage_1-97](assets/chlimage_1-97.png)

   或者，您也可以单击&#x200B;**预览**&#x200B;以查看json链接。

   ![chlimage_1-98](assets/chlimage_1-98.png)

   ***如果选择用于将实体创建为页面模型的模板***，则单击 **** 编辑可添加资产，如下图所示：

   ![chlimage_1-99](assets/chlimage_1-99.png)

   单击&#x200B;**路径**&#x200B;中的图标可添加资产

   ![chlimage_1-100](assets/chlimage_1-100.png)

   >[!NOTE]
   >
   >添加实体后，必须保存该实体，预览链接才能正常工作。 要查看预览，请单击&#x200B;**Save**。 单击&#x200B;**Preview**&#x200B;会显示已添加资产的json，如下图所示：

   ![chlimage_1-101](assets/chlimage_1-101.png)

   >[!NOTE]
   >
   >将资产添加到实体后，您可以选择&#x200B;**保存**&#x200B;以保存更改，或选择&#x200B;**保存并关闭**&#x200B;以保存并重定向到定义实体的空间控制台列表。

   此外，从空间控制台列表中选择一个实体，然后单击&#x200B;**属性**&#x200B;以查看和编辑已定义实体的属性。

   ![chlimage_1-102](assets/chlimage_1-102.png)

   您可以编辑标题、描述、标记，并将资产添加到实体中。

   ![chlimage_1-103](assets/chlimage_1-103.png)

### 删除实体{#removing-an-entity}

1. 从空间内容列表中选择实体

   ![chlimage_1-104](assets/chlimage_1-104.png)

1. 单击工具栏中的&#x200B;**Delete**&#x200B;以从空间中删除特定实体

### 发布实体{#publishing-an-entity}

您可以选择&#x200B;**发布树**&#x200B;或&#x200B;**快速发布**&#x200B;来发布您的实体。

1. 从空间控制台列表中选择一个实体，然后单击**发布树**以发布该实体及其子实体。

   ![chlimage_1-105](assets/chlimage_1-105.png)

   **或者**,

   单击&#x200B;**快速发布**&#x200B;以发布该特定实体。
