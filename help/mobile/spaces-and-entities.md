---
title: 空间和实体
description: 此页用作开发AEM Mobile Content Services的登陆页。
contentOwner: Jyotika Syal
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
exl-id: 44591900-b01b-4a33-9910-839564477e7d
source-git-commit: 10b370fd8f855f71c6d7d791c272137bb5e04d97
workflow-type: tm+mt
source-wordcount: '1206'
ht-degree: 1%

---

# 空间和实体{#spaces-and-entities}

>[!NOTE]
>
>Adobe建议对需要基于单页应用程序框架的客户端渲染（例如React）的项目使用SPA编辑器。 [了解详情](/help/sites-developing/spa-overview.md)。

空间是存储通过Content Services REST API公开的实体的方便位置。 此功能特别有用，因为应用程序（或任何渠道）可以与许多实体关联。 强制实体位于空间内会强制采用将应用程序要求分组的最佳实践。 或者，您可以将AEM中的应用程序与少量空间关联。

>[!NOTE]
>
>要使内容服务中的内容可供任何渠道使用，内容需要放在空间下。

## 创建空间 {#creating-a-space}

如果用户希望向移动设备应用程序展示大量内容和资产，则可以使用AEM Mobile仪表板创建空间。

首次有用户未将Content Services配置为使用空间，而AEM Mobile功能板在选中后仅显示应用程序 **内容服务**.

>[!CAUTION]
>
>**添加空间的先决条件**
>
>查看 **启用AEM内容服务** 使用空间并在AEM Mobile应用程序功能板中启用它。
>
>请参阅 [管理内容服务](/help/mobile/developing-content-services.md) 以了解更多详细信息。

在功能板中配置空间后，请按照以下步骤创建空间：

1. 选择 **空间** 来自Content Services。

   ![chlimage_1-83](assets/chlimage_1-83.png)

1. 选择 **创建** 创建空间。 输入 **标题**， **名称**、和 **描述** 为空间而战。

   单击&#x200B;**创建**。

   ![chlimage_1-84](assets/chlimage_1-84.png)

## 管理空间 {#managing-a-space}

创建空间后，单击左侧以管理列表中的空间。

您可以查看空间的属性，删除空间，或将空间及其内容发布到AEM发布实例。

![chlimage_1-85](assets/chlimage_1-85.png)

**查看和编辑空间的属性**

1. 从列表中选择空间
1. 选择 **属性** 工具栏中的
1. 单击 **关闭** 完成时

**发布空间** 发布空间时，也会发布该空间中的所有文件夹和实体。

1. 在“空间控制台”列表中单击空间的图标以选择空间
1. 选择 **发布树**

>[!NOTE]
>
>您可以 **取消发布** 空间，用于从发布实例中删除空间。
>
>下图说明了发布空间后可以执行的操作。

![chlimage_1-86](assets/chlimage_1-86.png)

## 使用空间中的文件夹 {#working-with-folders-in-a-space}

空间可以包含文件夹，以帮助进一步组织空间的内容和资源。 用户可以在空间下创建自己的层次结构。

### 创建文件夹 {#creating-a-folder}

1. 在空间控制台的列表中单击空间，然后单击 **创建文件夹**

   ![chlimage_1-87](assets/chlimage_1-87.png)

1. 输入 **标题**， **名称，** 和 **描述** 文件夹的

   ![chlimage_1-88](assets/chlimage_1-88.png)

1. 单击 **创建** 在空间中创建文件夹

## 语言复制 {#language-copy}

>[!CAUTION]
>
>语言副本无法完全用于此版本。 它只设置结构。

此 **语言复制** 该功能允许作者复制其主语言副本，然后创建项目和工作流程以自动翻译内容。 语言副本创建正确的结构。 在共享空间中添加文件夹后，即可向共享空间中添加语言副本。

>[!NOTE]
>
>建议将任何可能翻译的内容放在语言副本节点下。

### 添加语言副本 {#adding-language-copy}

1. 创建空间后，单击该空间以创建语言副本。

   单击 **创建** 并选择 **语言复制**.

   ![chlimage_1-89](assets/chlimage_1-89.png)

   >[!NOTE]
   >
   >语言副本节点只能作为空间的直接子级存在。

1. 选择 **内容包语言&amp;ast；** 并输入 **标题&amp;ast；** 在 **创建语言副本** 对话框。

   单击&#x200B;**创建**。

   ![chlimage_1-90](assets/chlimage_1-90.png)

1. 创建语言副本后，该副本会显示在您共享空间中的 **语言母版**.

   ![chlimage_1-91](assets/chlimage_1-91.png)

   >[!NOTE]
   >
   >选择 **语言母版** 查看语言副本文件夹。

### 从空间中删除文件夹 {#removing-a-folder-from-the-space}

1. 从空间内容列表中选择文件夹
1. 单击 **删除** 工具栏中的

   >[!NOTE]
   >
   >要导航到文件夹中并查看其内容或添加子文件夹或实体，请单击空间内容列表中的文件夹标题。

## 使用空间中的实体 {#working-with-entities-in-a-space}

实体表示通过Web服务端点公开的内容。 实体存储在空间中，以便可以轻松地找到并独立于保存其相关内容的AEM存储库结构进行保存。

您可能希望在某些逻辑集合中将实体分组在一起。 为此，您可以创建任意数量的文件夹。

如果为数据建模而收集了图元子项（即其他图元），则开发人员用户可以从“图元组”模型类型创建特定的“组模型”（现成可用）。

>[!NOTE]
>
>实体始终与空间相关联，因此大多数实体用户界面都可通过空间控制台访问。

### 创建实体 {#creating-an-entity}

1. 打开空间控制台，然后单击空间的标题。

   （可选）您可以通过单击列表中的文件夹标题来导航到该文件夹。

   ![chlimage_1-92](assets/chlimage_1-92.png)

1. 选择图元的模型。 这是要创建的实体类型。 单击“下一步”。

   ![chlimage_1-93](assets/chlimage_1-93.png)

   >[!NOTE]
   >
   >您可以选择以下选项 **资产模型**， **页面模型**&#x200B;或您之前创建的图元类型的模型。
   >
   >请参阅 [创建模型](/help/mobile/administer-mobile-apps.md)，以创建自定义实体。

1. 输入 **标题**， **名称**， **描述**、和 **标记** 实体的。 单击&#x200B;**创建**。

   ![chlimage_1-94](assets/chlimage_1-94.png)

   完成后，实体会显示在您共享空间的子项中。

### 编辑实体 {#editing-an-entity}

1. 创建实体后，转到文件夹或共享空间，然后从共享空间控制台中选择要编辑的实体。

   ![chlimage_1-95](assets/chlimage_1-95.png)

1. 选择要编辑的实体，然后单击 **编辑**.

   ![chlimage_1-96](assets/chlimage_1-96.png)

   >[!CAUTION]
   >
   >根据您选择创建实体的模板，用于编辑和查看实体属性的UI将有所不同。 有关更多详细信息，请参阅以下步骤。

   ***如果选择用于创建实体作为资产模型的模板***，单击 **编辑** 允许您添加资源，如下图所示：

   ![chlimage_1-97](assets/chlimage_1-97.png)

   或者，您可以单击 **预览** 以查看json链接。

   ![chlimage_1-98](assets/chlimage_1-98.png)

   ***如果选择用于创建实体作为页面模型的模板***，单击 **编辑** 允许您添加资源，如下图所示：

   ![chlimage_1-99](assets/chlimage_1-99.png)

   单击 **路径** 添加资产

   ![chlimage_1-100](assets/chlimage_1-100.png)

   >[!NOTE]
   >
   >添加实体后，必须保存该实体才能使“预览”链接正常工作。 要查看预览，请单击 **保存**. 单击 **预览** 显示了所添加资产的json，如下图所示：

   ![chlimage_1-101](assets/chlimage_1-101.png)

   >[!NOTE]
   >
   >完成向实体添加资产后，您可以选择 **保存** 保存更改或选择 **保存并关闭** 保存并重定向到在其中定义实体的空间控制台列表。

   此外，从空间控制台列表中选择一个实体，然后单击 **属性** 查看和编辑已定义实体的属性。

   ![chlimage_1-102](assets/chlimage_1-102.png)

   您可以编辑标题、描述和标记，并将资产添加到实体。

   ![chlimage_1-103](assets/chlimage_1-103.png)

### 删除实体 {#removing-an-entity}

1. 从空间内容列表中选择实体

   ![chlimage_1-104](assets/chlimage_1-104.png)

1. 单击 **删除** 从工具栏中移除特定实体

### 发布实体 {#publishing-an-entity}

您可以选择以下选项 **发布树** 或 **快速发布** 以发布您的实体。

1. 从空间控制台列表中选择一个实体，然后单击**发布树**以发布该实体及其子项。

   ![chlimage_1-105](assets/chlimage_1-105.png)

   **或**，

   单击 **快速发布** 以发布该特定实体。
