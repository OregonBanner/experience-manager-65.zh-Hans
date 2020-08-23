---
title: 项目
seo-title: 项目
description: 通过“项目”，您可以将资源分组到一个实体中，该实体的通用共享环境使您能够轻松管理项目
seo-description: 项目 您可以将资源分组到一个实体中，该实体的通用共享环境可轻松管理项目
uuid: 4b5b9d78-d515-46af-abe2-882da0a1c8ae
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: projects
content-type: reference
discoiquuid: dee7ac7c-ca86-48e9-8d95-7826fa926c68
docset: aem65
translation-type: tm+mt
source-git-commit: 80b8571bf745b9e7d22d7d858cff9c62e9f8ed1e
workflow-type: tm+mt
source-wordcount: '1395'
ht-degree: 75%

---


# 项目{#projects}

通过“项目”，您可以将资源分组到一个实体中。通用共享环境使您能够轻松管理项目。可以与项目关联的资源类型在 AEM 中称为“拼贴”。Tiles may include project and team information, assets, workflows, and other types of information, as described in detail in [Project Tiles.](#project-tiles)

>[!CAUTION]
>
>For users in projects to see other users/groups while using Projects functionality like creating projects, creating tasks/workflows, seeing and managing the team, those users need to have read access on **/home/users** and **/home/groups**. The easiest way to implement this is to give the **projects-users** group read access to **/home/users** and**/home/groups**.

作为用户，您可以执行以下操作：

* 创建项目
* 将内容和资产文件夹关联到项目
* 删除项目
* 从项目中删除内容链接

请参阅以下其他主题：

* [管理项目](/help/sites-authoring/touch-ui-managing-projects.md)
* [处理任务](/help/sites-authoring/task-content.md)
* [使用项目工作流](/help/sites-authoring/projects-with-workflows.md)
* [创意项目和 PIM 集成](/help/sites-authoring/managing-product-information.md)

## “项目”控制台{#projects-console}

在“项目”控制台中，您可以访问和管理 AEM 中的项目。

![screen-shot_2019-03-05at125110](assets/screen-shot_2019-03-05at125110.png)

* 选择&#x200B;**时间轴**，然后选择一个项目可查看其时间轴。
* 单击/点按&#x200B;**选择**&#x200B;可进入选择模式。
* 单击&#x200B;**创建**&#x200B;可添加项目。
* **切换活动的项目**&#x200B;允许您在所有项目和仅处于活动状态的项目之间切换。
* **显示统计信息视图**&#x200B;允许您查看与任务完成程度相关的项目统计信息。

## 项目拼贴 {#project-tiles}

通过项目，您可以将不同类型的信息与项目关联。这些信息称为&#x200B;**拼贴**。本节介绍了各个拼贴以及它们包含的信息类型。

您可以将以下拼贴与项目关联。以下各部分介绍了每个拼贴：

* 资产和资产收藏集
* 体验
* 链接
* 项目信息
* 团队
* 登陆页面
* 电子邮件
* 工作流
* 启动项
* 任务

### 资产 {#assets}

在&#x200B;**资产**&#x200B;拼贴中，您可以收集用于特定项目的所有资产。

![chlimage_1-70](assets/chlimage_1-70.png)

您可以直接在该拼贴中上传资产。另外，如果您拥有 Dynamic Media 加载项，则可以创建图像集、旋转集或混合媒体集。

![chlimage_1-71](assets/chlimage_1-71.png)

### 资产收藏集 {#asset-collections}

与资产类似，您可以直接将[资产收藏集](/help/assets/managing-collections-touch-ui.md)添加到项目中。您可以在资产中定义收藏集。

![chlimage_1-72](assets/chlimage_1-72.png)

单击&#x200B;**添加收藏集**&#x200B;并从列表中选择相应的收藏集，可添加收藏集。

### 体验 {#experiences}

**体验**&#x200B;拼贴允许您将移动设备应用程序、网站或出版物添加到项目中。

![chlimage_1-73](assets/chlimage_1-73.png)

这些图标指示表示的体验类型：网站、移动应用程序或出版物。 单击+符号或单击添加体验 **并选择体验类型** ，以添加体验。

![chlimage_1-74](assets/chlimage_1-74.png)

选择缩略图的路径，并在适用的情况下更改体验的缩略图。Experiences are grouped together in the **Experiences** tile.

### 链接 {#links}

“链接”拼贴允许您将外部链接与项目关联。

![chlimage_1-75](assets/chlimage_1-75.png)

您可以使用易于识别的名称来命名链接并更改其缩略图。

![chlimage_1-76](assets/chlimage_1-76.png)

### 项目信息 {#project-info}

“项目信息”拼贴提供了项目的一般信息，包括描述、项目状态（非活动或活动）、到期日期和成员。此外，您还可以添加项目缩略图，该缩略图会显示在“项目”主页上。

![chlimage_1-77](assets/chlimage_1-77.png)

您可以从该拼贴和“团队”拼贴中分配和删除团队成员（或者更改其角色）。

![chlimage_1-78](assets/chlimage_1-78.png)

### 翻译作业 {#translation-job}

在“翻译作业”拼贴中，您可以开始翻译，也可以查看翻译状态。要设置翻译，请参阅[创建翻译项目](/help/assets/translation-projects.md)。

![chlimage_1-79](assets/chlimage_1-79.png)

Click the ellipsis at the bottom of the **Translation Job** card to view the assets in the translation workflow. 转换作业列表还显示资产元数据和标记的条目。 这些条目指示资产的元数据和标记也会被翻译。

![chlimage_1-80](assets/chlimage_1-80.png)

### 团队 {#team}

在此拼贴中，您可以指定项目团队的成员。编辑时，您可以输入团队成员的姓名并分配用户角色。

![chlimage_1-81](assets/chlimage_1-81.png)

您可以在团队中添加和删除团队成员。In addition, you can edit the [user role](#userroles) assigned to the team member.

![chlimage_1-82](assets/chlimage_1-82.png)

### 登陆页面 {#landing-pages}

**登陆页面**&#x200B;拼贴允许您请求新的登陆页面。

![chlimage_1-83](assets/chlimage_1-83.png)

此工作流在[创建登陆页面工作流](/help/sites-authoring/projects-with-workflows.md#request-landing-page-workflow)中进行了介绍。

### 电子邮件 {#emails}

**电子邮件**&#x200B;拼贴可帮助您管理电子邮件请求。它会启动请求电子邮件工作流。

![chlimage_1-84](assets/chlimage_1-84.png)

有关更多信息，请参阅[请求电子邮件工作流](/help/sites-authoring/projects-with-workflows.md#request-email-workflow)。

### 工作流 {#workflows}

您可以指定项目遵循特定的工作流。当有任何工作流正在运行时，其状态会显示在“项目”的&#x200B;**工作流**&#x200B;拼贴中。

![chlimage_1-85](assets/chlimage_1-85.png)

您可以指定项目遵循特定的工作流。根据您选择的项目，您可以使用不同的工作流。

这些工作流在[使用项目工作流](/help/sites-authoring/projects-with-workflows.md)中进行了介绍。

### 启动项 {#launches}

“启动项”拼贴显示使用[请求启动项工作流](/help/sites-authoring/projects-with-workflows.md)请求的任何启动项。

![chlimage_1-86](assets/chlimage_1-86.png)

### 任务 {#tasks}

“任务”拼贴允许您监测任何项目相关任务（包括工作流）的状态。Tasks are covered in detail at [Working with Tasks](/help/sites-authoring/task-content.md).

![chlimage_1-87](assets/chlimage_1-87.png)

## 项目模板 {#project-templates}

AEM随附三个不同的现成模板：

* 简单项目——任何不适合其他类别的项目的参考范例（全部捕获）。 它包括三个基本角色（所有者、编辑者和观察者）和四个工作流（项目批准、请求启动项、请求登陆页面和请求电子邮件）。
* 媒体项目——与媒体相关的活动的参考示例项目。 它包括几个与媒体相关的项目角色（摄影师、编辑者、撰稿人、设计师、所有者和观察者）。它还包括两个与媒体内容相关的工作流-请求复制（用于请求和查看文本）和产品照片拍摄（用于管理与产品相关的照片）
* [产品照片拍摄项目](/help/sites-authoring/managing-product-information.md) -用于管理与电子商务相关的产品照片的参考范例。 它包括摄影师、编辑、修图师、所有者、创意总监、社交媒体营销人员、营销经理、审阅者和观察者的角色。
* [翻译项目](/help/sites-administering/translation.md) - 用于管理翻译相关活动的参考示例。它包括三个基本角色（所有者、编辑者和观察者）。它包括两个工作流，它们可在工作流用户界面中访问。

根据您选择的模板，您可以使用不同的选项，特别是与用户角色和工作流有关的选项。

## 项目中的用户角色 {#user-roles-in-a-project}

项目模板中设置了不同的用户角色，之所以使用这些用户角色，主要是出于以下两个原因：

1. 权限. 用户角色属于下列三个类别之一：观察者、编辑者、所有者。例如，摄影师或文案人将具有与编辑相同的权限。 权限决定了用户可以对项目中的内容执行的操作。
1. 工作流. 工作流可确定向谁分配了项目中的任务。任务可以与项目角色关联。 例如，可以将某个任务分配给摄影师，这样所有具有摄影师角色的团队成员都将会获取该任务。

所有项目都支持以下默认角色，以便您可以管理安全性和控制权限：

<table>
 <tbody>
  <tr>
   <td><p><strong>角色</strong></p> </td>
   <td><p><strong>描述</strong></p> </td>
   <td><p><strong>权限</strong></p> </td>
   <td><p><strong>组成员资格</strong></p> </td>
  </tr>
  <tr>
   <td><p>观察者</p> </td>
   <td><p>具有此角色的用户可以查看项目详细信息，包括项目状态。</p> </td>
   <td><p>项目的只读权限</p> </td>
   <td><p>工作流用户组</p> </td>
  </tr>
  <tr>
   <td><p>编辑者</p> </td>
   <td><p>具有此角色的用户可以上传和编辑项目的内容。</p> <p> </p> </td>
   <td>
    <ul>
     <li>项目、关联元数据和相关资产的读取和写入权限</li>
     <li>上传拍摄列表、照片拍摄以及审核和批准资产的权限</li>
     <li>/etc/commerce 的写入权限</li>
     <li>拥有特定项目的修改权限</li>
    </ul> </td>
   <td><p>工作流用户组</p> </td>
  </tr>
  <tr>
   <td><p>所有者</p> </td>
   <td><p>具有此角色的用户可以启动项目。所有者可以创建项目、在项目中启动工作以及将已批准的资产移至“生产”文件夹。 所有者还可以查看和执行项目中的所有其他任务。</p> </td>
   <td>
    <ul>
     <li>/etc/commerce 的写入权限</li>
    </ul> </td>
   <td>
    <ul>
     <li>DAM用户组（能够创建项目）</li>
     <li>项目管理员组（可移动资产）</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

对于创意项目，还提供了其他角色，例如摄影师。您可以使用这些角色来为特定项目派生自定义角色。

>[!NOTE]
>
>在创建项目并将用户添加各种角色时，将自动创建与项目关联的组以管理关联的权限。例如，名为 Myproject 的项目将有三个组，分别为 **Myproject 所有者**、**Myproject 编辑者**、**Myproject 观察者**。但是，如果删除了项目，这些组不会自动删除。管理员需要在&#x200B;**工具** > **安全** > **组**&#x200B;中手动删除这些组。
