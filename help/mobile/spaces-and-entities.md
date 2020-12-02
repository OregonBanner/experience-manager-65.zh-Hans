---
title: 空格和实体
seo-title: 开发AEM Mobile内容服务
description: 本页为开发AEM Mobile内容服务提供登陆页。
seo-description: 本页为开发AEM Mobile内容服务提供登陆页。
uuid: eab5a61b-a9e8-4863-90a3-df1f18510cd8
contentOwner: Jyotika Syal
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
discoiquuid: ef568577-c74e-4fc2-b66e-eedac2948310
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '1209'
ht-degree: 1%

---


# 空格和实体{#spaces-and-entities}

>[!NOTE]
>
>Adobe建议对需要基于单页应用程序框架的客户端渲染（例如，React）的项目使用SPA编辑器。 [了解更多](/help/sites-developing/spa-overview.md).

空间是存储通过Content Services REST API公开的实体的便捷位置。 这特别有用，因为应用程序(或任何渠道)可以与许多实体关联。 强制实体位于空间内强制最佳实践是对应用程序的要求进行分组。 或者，您可以将AEM中的应用程序与少量空间关联。

>[!NOTE]
>
>要向来自内容服务的任何渠道提供内容，它需要位于某个空间下。

## 创建空格{#creating-a-space}

如果用户希望向移动应用程序展示大量内容和资产，则用户使用AEM Mobile仪表板创建空间。

对于尚未配置内容服务以使用空格的首次用户，AEM Mobile仪表板在选择&#x200B;**内容服务**&#x200B;后仅显示应用程序。

>[!CAUTION]
>
>**添加空间的先决条件**
>
>检查&#x200B;**启用AEM Content Services**&#x200B;以使用空格，并在您的AEM Mobile应用程序仪表板中启用它。
>
>有关详细信息，请参阅[管理内容服务](/help/mobile/developing-content-services.md)。

在仪表板中配置空格后，请按照以下步骤创建空格：

1. 从“内容服务”中选择&#x200B;**空格**。

   ![chlimage_1-83](assets/chlimage_1-83.png)

1. 选择&#x200B;**创建**&#x200B;以创建空格。 输入&#x200B;**标题**、**名称**&#x200B;和&#x200B;**说明**&#x200B;作为空格。

   单击&#x200B;**创建**。

   ![chlimage_1-84](assets/chlimage_1-84.png)

## 管理空间{#managing-a-space}

创建空间后，单击左侧以管理列表中的空间。

您可以视图空间的属性、删除空间或将空间及其内容发布到AEM发布实例。

![chlimage_1-85](assets/chlimage_1-85.png)

**查看和编辑空间的属性**

1. 从列表中选择空格
1. 从工具栏中选择&#x200B;**属性**
1. 完成后，单击&#x200B;**关闭**

**发布空** 间发布空间时，该空间中的所有文件夹和实体也会发布。

1. 在空间控制台列表中单击空间图标以选择空间
1. 选择&#x200B;**发布树**

>[!NOTE]
>
>可以&#x200B;**取消发布**&#x200B;空间，从发布实例中删除该空间。
>
>下图说明了在发布空间后可以执行的操作。

![chlimage_1-86](assets/chlimage_1-86.png)

## 处理空间{#working-with-folders-in-a-space}中的文件夹

空间可以包含文件夹，以帮助进一步组织空间的内容和资产。 用户可以在空间下创建自己的层次结构。

### 创建文件夹{#creating-a-folder}

1. 单击空间控制台列表中的空间，然后单击&#x200B;**创建文件夹**

   ![chlimage_1-87](assets/chlimage_1-87.png)

1. 输入文件夹的&#x200B;**标题**、**名称、**&#x200B;和&#x200B;**说明**

   ![chlimage_1-88](assets/chlimage_1-88.png)

1. 单击&#x200B;**创建**&#x200B;以在空格中创建文件夹

## 语言副本 {#language-copy}

>[!CAUTION]
>
>语言副本对此版本功能不全。 它只设置结构。

**语言副本**&#x200B;功能允许作者复制其主控语言副本，然后创建项目和工作流以自动翻译内容。 语言副本创建正确的结构。 在空间中添加文件夹后，即可向空间添加语言副本。

>[!NOTE]
>
>建议将任何可能已翻译的内容放在“语言副本”节点下。

### 添加语言副本{#adding-language-copy}

1. 创建空间后，单击该空间即可创建语言副本。

   单击&#x200B;**创建**&#x200B;并选择&#x200B;**语言副本**。

   ![chlimage_1-89](assets/chlimage_1-89.png)

   >[!NOTE]
   >
   >语言副本节点只能作为空间的直接子节点存在。

1. 选择&#x200B;**内容包语言&amp;ast;**，并在&#x200B;**创建语言副本**&#x200B;对话框中输入&#x200B;**标题&amp;ast;**。

   单击&#x200B;**创建**。

   ![chlimage_1-90](assets/chlimage_1-90.png)

1. 创建语言副本后，该副本会显示在&#x200B;**语言母版**&#x200B;的空白处。

   ![chlimage_1-91](assets/chlimage_1-91.png)

   >[!NOTE]
   >
   >选择&#x200B;**语言主页**&#x200B;以视图语言副本文件夹。

### 从空格{#removing-a-folder-from-the-space}中删除文件夹

1. 从空间内容列表中选择文件夹
1. 单击工具栏中的&#x200B;**删除**

   >[!NOTE]
   >
   >要导航到文件夹并查看其内容或添加子文件夹或实体，请在空间的内容列表中单击该文件夹的标题。

## 使用空格{#working-with-entities-in-a-space}中的实体

实体表示通过Web服务端点公开的内容。 实体存储在空格中，因此可以轻松找到实体，并与包含其相关内容的AEM存储库结构保持独立。

您可能希望在某个逻辑收集中将实体分组在一起。 为此，您可以创建任意数量的文件夹。

如果为数据建模而收集其他实体的实体子项，开发者用户可以根据现成的“实体组”模型类型创建特定的“组模型”。

>[!NOTE]
>
>实体始终与空间关联，因此大多数实体用户界面都通过空间控制台进行访问。

### 创建实体{#creating-an-entity}

1. 打开空间控制台，然后单击空间的标题。

   或者，您也可以通过单击该列表中文件夹的标题来导航到该文件夹。

   ![chlimage_1-92](assets/chlimage_1-92.png)

1. 为图元选择模型。 这是您要创建的实体类型。 单击下一步。

   ![chlimage_1-93](assets/chlimage_1-93.png)

   >[!NOTE]
   >
   >您可以选择&#x200B;**资产模型**、**页面模型**&#x200B;或您之前创建的实体类型模型。
   >
   >请参阅[创建模型](/help/mobile/administer-mobile-apps.md)以创建自定义实体。

1. 输入实体的&#x200B;**标题**、**名称**、**说明**&#x200B;和&#x200B;**标记**。 单击&#x200B;**创建**。

   ![chlimage_1-94](assets/chlimage_1-94.png)

   完成后，该实体将显示在空间的后代中。

### 编辑实体{#editing-an-entity}

1. 创建实体后，转到文件夹或空间，并从“空间”控制台中选择要编辑的实体。

   ![chlimage_1-95](assets/chlimage_1-95.png)

1. 选择要编辑的实体，然后单击&#x200B;**编辑**。

   ![chlimage_1-96](assets/chlimage_1-96.png)

   >[!CAUTION]
   >
   >根据您选择创建实体的模板，在编辑和查看实体属性时，两者的UI将有所不同。 有关更多详细信息，请参阅以下步骤。

   ***如果您选择用于创建实体的模板作为“资产模型***”，则 **** 单击“编辑”可添加资产，如下图所示：

   ![chlimage_1-97](assets/chlimage_1-97.png)

   或者，也可以单击&#x200B;**预览**&#x200B;视图json链接。

   ![chlimage_1-98](assets/chlimage_1-98.png)

   ***如果您选择用于创建实体的模板作为页面模型***，则单 **** 击编辑允许您添加资产，如下图所示：

   ![chlimage_1-99](assets/chlimage_1-99.png)

   单击&#x200B;**路径**&#x200B;中的图标以添加资产

   ![chlimage_1-100](assets/chlimage_1-100.png)

   >[!NOTE]
   >
   >添加实体后，必须保存该实体，预览链接才能正常工作。 要视图预览，请单击&#x200B;**保存**。 单击&#x200B;**预览**&#x200B;将显示已添加资产的json，如下图所示：

   ![chlimage_1-101](assets/chlimage_1-101.png)

   >[!NOTE]
   >
   >在将资产添加到实体后，您可以选择&#x200B;**保存**&#x200B;来保存更改，或者选择&#x200B;**保存并关闭**&#x200B;来保存并重定向到定义实体的空间控制台列表。

   此外，从空间控制台列表卡中选择一个实体，然后单击&#x200B;**属性**&#x200B;以视图和编辑已定义实体的属性。

   ![chlimage_1-102](assets/chlimage_1-102.png)

   您可以编辑标题、描述、标记，并将资产添加到您的实体。

   ![chlimage_1-103](assets/chlimage_1-103.png)

### 删除实体{#removing-an-entity}

1. 从空间内容列表中选择实体

   ![chlimage_1-104](assets/chlimage_1-104.png)

1. 单击工具栏中的&#x200B;**删除**&#x200B;以从空间中删除特定实体

### 发布实体{#publishing-an-entity}

您可以选择&#x200B;**发布树**&#x200B;或&#x200B;**快速发布**&#x200B;来发布您的实体。

1. 从空间控制台列表卡中选择一个实体，然后单击**发布树**以发布该实体及其子实体。

   ![chlimage_1-105](assets/chlimage_1-105.png)

   **或者**,

   单击&#x200B;**快速发布**&#x200B;以发布该特定实体。
