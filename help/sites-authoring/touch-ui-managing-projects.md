---
title: 管理项目
seo-title: 管理项目
description: 通过“项目”，您可以将资源分组到一个可以在“项目”控制台中访问和管理的实体中，从而组织项目
seo-description: 通过“项目”，您可以将资源分组到一个可以在“项目”控制台中访问和管理的实体中，从而组织项目
uuid: ac937582-181f-429b-9404-3c71d1241495
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: projects
content-type: reference
discoiquuid: fb354c72-debb-4fb6-9ccf-56ff5785c3ae
translation-type: tm+mt
source-git-commit: 58fa0f05bae7ab5ba51491be3171b5c6ffbe870d
workflow-type: tm+mt
source-wordcount: '1057'
ht-degree: 77%

---


# 管理项目{#managing-projects}

通过“项目”，您可以将资源分组到一个实体中来组织项目。

在&#x200B;**项目**&#x200B;控制台中，您可以访问项目并对其执行操作：

![chlimage_1-255](assets/chlimage_1-255.png)

在“项目”中，您可以创建项目、将资源与项目关联，还可以删除项目或资源链接。您可能想要打开一个拼贴来查看其内容，以及向拼贴中添加一些项。本主题介绍了这些过程。

>[!NOTE]
>
>6.2 引入了将项目组织到文件夹中的功能。在“项目”页面上，您可以创建项目或文件夹。
>
>如果已创建某个文件夹，则会使用户转到该文件夹，用户可以在其中创建其他文件夹或项目。这有助于根据产品营销活动、位置、翻译语言等类别将项目组织到文件夹中。
>
>您可以在列表视图中查看项目和文件夹，也可以搜索项目和文件夹。

>[!CAUTION]
>
>对于项目中的用户，要使用“项目”功能(如创建项目、创建任务/工作流、查看和管理团队)查看其他用户／组，这些用户需要具有对&#x200B;**/home/users**&#x200B;和&#x200B;**/home/groups**&#x200B;的读取权限。 实现此功能的最简单方法是向&#x200B;**projects-users**&#x200B;组授予对&#x200B;**/home/users**&#x200B;和&#x200B;**/home/groups**&#x200B;的读取权限。

## 创建项目 {#creating-a-project}

AEM 提供了以下现成的模板，供您在创建项目时进行选择：

* 简单项目
* 媒体项目
* 产品照片拍摄项目
* 翻译项目

从项目到项目，创建项目的过程相同。 项目类型之间的差异包括可用的用户角 [色](/help/sites-authoring/projects.md) 和工 [作流](/help/sites-authoring/projects-with-workflows.md)。  要创建新项目，请执行以下操作：

1. 在“ **项目**”中，点按／单 **击创建** ，以打开创 **建项目向导** :
1. 选择模板。开箱即用：简单项目、媒体项目、[翻译项目](/help/sites-administering/tc-manage.md)和[产品照片拍摄产品](/help/sites-authoring/managing-product-information.md)，然后单击&#x200B;**下一个**。

   ![chlimage_1-256](assets/chlimage_1-256.png)

1. 定义&#x200B;**标题**&#x200B;和&#x200B;**说明**，并根据需要添加&#x200B;**缩略图**&#x200B;图像。 您还可以添加或删除用户以及他们所属的组。此外，也可单击&#x200B;**高级**&#x200B;以添加 URL 中使用的名称。

   ![chlimage_1-257](assets/chlimage_1-257.png)

1. 点按/单击&#x200B;**创建**。确认对话框会询问您是要打开新项目还是要返回到控制台。

### 将资源与项目关联  {#associating-resources-with-your-project}

由于项目使您能够将资源分组到一个实体中，因此您需要将资源关联到项目。这些资源称为&#x200B;**拼贴**。有关可添加的资源类型的说明，请参阅[项目拼贴](/help/sites-authoring/projects.md#project-tiles)。

要将资源与项目关联，请执行以下操作：

1. 从&#x200B;**项目**&#x200B;控制台中打开您的项目。
1. 点按/单击&#x200B;**添加拼贴**，然后选择您要链接到项目的拼贴。您可以选择多种类型的拼贴。

   ![chlimage_1-258](assets/chlimage_1-258.png)

   >[!NOTE]
   >
   >有关可与项目关联的项目拼贴的详细说明，请参阅[项目拼贴](/help/sites-authoring/projects.md#project-tiles)。

1. 点按/单击&#x200B;**创建**。您的资源已链接到您的项目，从现在开始，您可以从您的项目访问它。

### 删除项目或资源链接 {#deleting-a-project-or-resource-link}

可使用同样的方法从控制台中删除项目或项目中的链接资源：

1. 导航到适当的位置：

   * 要删除项目，请转到&#x200B;**项目**&#x200B;控制台的顶层。
   * 要删除项目中的资源链接，请在&#x200B;**项目**&#x200B;控制台中打开相应的项目。

1. 单击&#x200B;**选择**&#x200B;并选择您的项目或资源链接，以进入选择模式。
1. 点按/单击&#x200B;**删除**。

1. 您需要在对话框中确认删除。确认后，将会删除项目或资源链接。点按/单击&#x200B;**取消选择**&#x200B;可退出选择模式。

>[!NOTE]
>
>在创建项目并将用户添加各种角色时，将自动创建与项目关联的组以管理关联的权限。例如，名为 Myproject 的项目将有三个组，分别为 **Myproject 所有者**、**Myproject 编辑者**、**Myproject 观察者**。但是，如果删除了项目，这些组不会自动删除。管理员需要在&#x200B;**工具** > **安全** > **组**&#x200B;中手动删除这些组。

### 向拼贴中添加一些项 {#adding-items-to-a-tile}

在某些拼贴中，您可能想要添加多个项。例如，您可能会一次运行多个工作流或多个体验。

要向拼贴中添加一些项，请执行以下操作：

1. 在&#x200B;**项目**&#x200B;中，导航到项目并单击要向其添加项目的拼贴上的添加+图标。

   ![chlimage_1-259](assets/chlimage_1-259.png)

1. 像创建新拼贴时一样，向拼贴中添加项。项目拼贴在[此处](/help/sites-authoring/projects.md#project-tiles)进行了介绍。在此示例中，添加了其他工作流。

   ![chlimage_1-260](assets/chlimage_1-260.png)

### 打开拼贴 {#opening-a-tile}

您可能想要查看当前拼贴中包含的各个项，或者修改或删除拼贴中的一些项。

要打开拼贴，以便查看其中的各个项或修改一些项，请执行以下操作：

1. 在“项目”控制台中，点按/单击省略号 (...)。

   ![chlimage_1-261](assets/chlimage_1-261.png)

1. AEM 列出了该拼贴中的各个项。您可以进入选择模式来修改或删除一些项。

   ![chlimage_1-262](assets/chlimage_1-262.png)

## 查看项目统计信息 {#viewing-project-statistics}

要查看项目统计信息，请在&#x200B;**项目**&#x200B;控制台中单击&#x200B;**显示统计信息视图**。随即会显示每个项目的完成程度。再次单击&#x200B;**显示统计视图**&#x200B;以转到&#x200B;**项目**&#x200B;控制台。

![chlimage_1-263](assets/chlimage_1-263.png)

### 查看项目时间轴 {#viewing-a-project-timeline}

项目时间轴提供了项目中的资产上次使用时间的相关信息。要视图项目时间轴，请单击／点按&#x200B;**时间轴**，然后进入选择模式并选择项目。 资产会显示在左侧窗格中。单击／点按&#x200B;**时间轴**&#x200B;以返回至&#x200B;**项目**&#x200B;控制台。

![chlimage_1-264](assets/chlimage_1-264.png)

### 查看活动/不活动的项目 {#viewing-active-inactive-projects}

要在活动项目和非活动项目之间切换，请在&#x200B;**项目**&#x200B;控制台中，单击&#x200B;**切换活动项目**。 如果该图标旁边显示有复选标记，则显示的是活动的项目。

![chlimage_1-265](assets/chlimage_1-265.png)

如果该图标旁边显示有一个 x，则显示的是不活动的项目。

![chlimage_1-266](assets/chlimage_1-266.png)

## 将项目设为不活动或活动 {#making-projects-inactive-or-active}

如果您已完成项目，但仍希望保留有关该项目的信息，您可能需要将项目设为不活动。

要将项目设为不活动（或活动），请执行以下操作：

1. 在&#x200B;**项目**&#x200B;控制台中，打开您的项目，然后找到&#x200B;**项目信息**&#x200B;拼贴。

   >[!NOTE]
   如果该拼贴不在您的项目中，您可能需要添加它。请参阅[添加拼贴](#adding-items-to-a-tile)。

1. 点按／单击&#x200B;**编辑**。
1. 将选择器从&#x200B;**活动**&#x200B;更改为&#x200B;**不活动**（反之亦然）。

   ![chlimage_1-267](assets/chlimage_1-267.png)

1. 点按/单击&#x200B;**完成**&#x200B;以保存更改。

