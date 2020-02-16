---
title: 空格和实体
seo-title: 开发AEM Mobile内容服务
description: 此页面用于开发AEM Mobile内容服务的登录页面。
seo-description: 此页面用于开发AEM Mobile内容服务的登录页面。
uuid: eab5a61b-a9e8-4863-90a3-df1f18510cd8
contentOwner: Jyotika Syal
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
discoiquuid: ef568577-c74e-4fc2-b66e-eedac2948310
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 空格和实体{#spaces-and-entities}

>[!NOTE]
>
>Adobe建议对需要基于单页应用程序框架的客户端渲染（例如，React）的项目使用SPA编辑器。 [了解更多](/help/sites-developing/spa-overview.md).

空间是存储通过Content Services REST API公开的实体的便捷位置。 这特别有用，因为应用程序（或任何渠道）可以与许多实体关联。 强制实体位于空间内强制最佳实践是将应用程序的要求分组。 或者，您也可以在AEM中将应用程序与少量空间关联。

>[!NOTE]
>
>要使内容服务中的任何渠道都可以使用某些内容，它需要位于某个空间内。

## 创建空间 {#creating-a-space}

如果用户希望向移动应用程序展示大量内容和资产，则用户会使用AEM Mobile控制面板创建空间。

对于首次将内容服务配置为使用空格的用户，AEM Mobile控制面板在选择内容服务后仅显示应用 **程序**。

>[!CAUTION]
>
>**添加空间的先决条件**
>
>选中“ **启用AEM Content Services** ”以使用Spaces，然后在AEM mobile应用程序功能板中启用它。
>
>有关更 [多详细信息，请参阅](/help/mobile/developing-content-services.md) “管理内容服务”。

在功能板中配置空格后，请按照以下步骤创建空格：

1. 从“内 **容服务** ”中选择“空格”。

   ![chlimage_1-83](assets/chlimage_1-83.png)

1. 选择 **创建** ，以创建空间。 输 **入空**&#x200B;格的标 **题**、名称 **和** 说明。

   单击&#x200B;**创建**。

   ![chlimage_1-84](assets/chlimage_1-84.png)

## 管理空间 {#managing-a-space}

创建空间后，单击左侧可管理列表中的空间。

您可以查看空间的属性、删除空间或将空间及其内容发布到AEM发布实例。

![chlimage_1-85](assets/chlimage_1-85.png)

**查看和编辑空间的属性**

1. 从列表中选择空格
1. Choose **Properties** from the toolbar
1. 完成 **后单击** “关闭”

**发布空间** ：发布空间时，该空间中的所有文件夹和实体也会发布。

1. 通过单击“空间控制台”列表中的空间图标来选择该空间
1. 选择 **发布树**

>[!NOTE]
>
>您可以 **取消发布** Space，从发布实例中删除该空间。
>
>下图说明了在发布空间后可以执行的操作。

![chlimage_1-86](assets/chlimage_1-86.png)

## 在空间中使用文件夹 {#working-with-folders-in-a-space}

空间可以包含文件夹以帮助进一步组织空间的内容和资产。 用户可以在空间下创建自己的层次结构。

### 创建文件夹 {#creating-a-folder}

1. 单击空间控制台中列表中的空间，然后单击“创建文 **件夹”**

   ![chlimage_1-87](assets/chlimage_1-87.png)

1. 输入文 **件夹的**“标 **题”、** “名称 **”和“** 说明”

   ![chlimage_1-88](assets/chlimage_1-88.png)

1. 单击 **创建** ，以在空间中创建文件夹

## 语言副本 {#language-copy}

>[!CAUTION]
>
>语言副本对于此版本功能不全。 它只设置结构。

“语 **言复制** ”功能允许作者复制其主语言副本，然后创建项目和工作流以自动翻译内容。 语言副本可创建正确的结构。 在空间中添加文件夹后，即可向空间添加语言副本。

>[!NOTE]
>
>建议将任何可能翻译的内容放在“语言副本”节点下。

### 添加语言副本 {#adding-language-copy}

1. 创建空间后，单击该空间即可创建语言副本。

   单击“ **创建** ”，然后选择“ **语言副本”**。

   ![chlimage_1-89](assets/chlimage_1-89.png)

   >[!NOTE]
   >
   >语言副本节点只能作为空间的直接子节点存在。

1. **** 选择 **内容包语言(&amp;A);并输入** Title&amp;ast;在“创 **建语言副本** ”对话框中。

   单击&#x200B;**创建**。

   ![chlimage_1-90](assets/chlimage_1-90.png)

1. 创建语言副本后，该副本会显示在“语言母版”的 **空间中**。

   ![chlimage_1-91](assets/chlimage_1-91.png)

   >[!NOTE]
   >
   >选择“ **语言主页** ”以查看语言副本文件夹。

### 从空间中删除文件夹 {#removing-a-folder-from-the-space}

1. 从空间内容列表中选择文件夹
1. 单击工 **具栏中** 的删除

   >[!NOTE]
   >
   >要导览至某个文件夹并查看其内容或添加子文件夹或实体，请单击该空间内容列表中该文件夹的标题。

## 使用空间中的图元 {#working-with-entities-in-a-space}

实体表示通过Web服务端点公开的内容。 实体存储在空格中，因此可以轻松找到并独立于保存其相关内容的AEM存储库结构。

您可能希望在某些逻辑收集中将实体分组在一起。 为此，您可以创建任意数量的文件夹。

如果为数据建模收集了其他实体的实体子项，则开发人员用户可以根据现成的“实体组”模型类型创建特定的“组模型”。

>[!NOTE]
>
>实体始终与空间关联，因此大部分实体用户界面都可通过空间控制台访问。

### 创建实体 {#creating-an-entity}

1. 打开空间控制台，然后单击空间的标题。

   或者，您也可以通过单击列表中文件夹的标题来导航到该文件夹。

   ![chlimage_1-92](assets/chlimage_1-92.png)

1. 为图元选择模型。 这是您要创建的实体类型。 单击下一步。

   ![chlimage_1-93](assets/chlimage_1-93.png)

   >[!NOTE]
   >
   >您可以选择资产模型、页 **面模型**, ****&#x200B;或您之前创建的实体类型模型。
   >
   >请参 [阅创建模型](/help/mobile/administer-mobile-apps.md)，以创建自定义实体。

1. 输入实 **体的标题**、名 **称**、说明 **、****** 标记和标记。 单击&#x200B;**创建**。

   ![chlimage_1-94](assets/chlimage_1-94.png)

   完成后，该实体将显示在空间的后代中。

### 编辑实体 {#editing-an-entity}

1. 创建实体后，转到您的文件夹或空间，然后从“空间”控制台中选择要编辑的实体。

   ![chlimage_1-95](assets/chlimage_1-95.png)

1. 选择要编辑的实体，然后单击“编 **辑”**。

   ![chlimage_1-96](assets/chlimage_1-96.png)

   >[!CAUTION]
   >
   >根据您选择创建实体的模板，编辑和查看实体属性时，两者的UI会有所不同。 有关更多详细信息，请参阅以下步骤。

   ***如果选择用于创建实体的模板作为“资产模型***”，则单击“编 **辑** ”可添加资产，如下图所示：

   ![chlimage_1-97](assets/chlimage_1-97.png)

   或者，也可以单击“ **预览** ”来查看json链接。

   ![chlimage_1-98](assets/chlimage_1-98.png)

   ***如果选择用于创建实体的模板作为页面模型***，则单击“编辑 **** ”可添加资产，如下图所示：

   ![chlimage_1-99](assets/chlimage_1-99.png)

   单击路径中的图 **标** ，添加资产

   ![chlimage_1-100](assets/chlimage_1-100.png)

   >[!NOTE]
   >
   >添加实体后，必须保存该实体才能使“预览”链接正常工作。 要查看预览，请单击“保 **存”**。 单击“预 **览** ”可显示添加的资产的json，如下图所示：

   ![chlimage_1-101](assets/chlimage_1-101.png)

   >[!NOTE]
   >
   >在将资产添加到实体后，您可以选择 **Save** （保存）以保存更改，或选择 **** Save &amp; Close（保存并关闭）以保存并重定向到定义实体的空间控制台列表。

   此外，从空间控制台列表中选择一个实体，然后单击“ **属性** ”(Properties)以查看和编辑已定义实体的属性。

   ![chlimage_1-102](assets/chlimage_1-102.png)

   您可以编辑标题、说明、标记，并将资产添加到您的实体。

   ![chlimage_1-103](assets/chlimage_1-103.png)

### 删除实体 {#removing-an-entity}

1. 从空间内容列表中选择实体

   ![chlimage_1-104](assets/chlimage_1-104.png)

1. 单击 **工具栏中的** “删除”(Delete)，以从空间中删除特定实体

### 发布实体 {#publishing-an-entity}

您可以选择“发布树” **或“快速发布****** ”来发布您的实体。

1. 从空间控制台列表中选择一个实体，然后单击**发布树**以发布该实体及其子实体。

   ![chlimage_1-105](assets/chlimage_1-105.png)

   **或者**,

   单击 **快速发布** ，以发布该特定实体。
