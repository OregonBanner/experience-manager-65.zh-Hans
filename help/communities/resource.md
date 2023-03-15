---
title: 创建和分配启用资源
seo-title: Create and Assign Enablement Resources
description: 添加启用资源
seo-description: Add enablement resources
uuid: da940242-0c9b-4ad8-8880-61fd41461c3b
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: introduction
content-type: reference
discoiquuid: 8fe97181-600e-42ac-af25-d5d4db248740
exl-id: 78908a9c-a260-44ff-ad1e-baa6d78ae399
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '711'
ht-degree: 6%

---

# 创建和分配启用资源 {#create-and-assign-enablement-resources}

## 添加启用资源 {#add-an-enablement-resource}

要将启用资源添加到新社区站点，请执行以下操作：

* 以系统管理员身份登录创作实例：
   * 例如， [http://localhost:4502/](http://localhost:4503/)
* 在全局导航中，选择 **[!UICONTROL Communities]** > **[!UICONTROL 资源]**

   ![资源](assets/resources.png)

   ![enablement-resource](assets/enablement-resource.png)
* 选择要向其中添加启用资源的社区站点：
   * 选择 **[!UICONTROL 启用教程]**.
* 从菜单中，选择 **[!UICONTROL 创建]**.
* 选择 **[!UICONTROL 资源]**.

![create-resource](assets/create-enablement-resource.png)

### 基本信息 {#basic-info}

填写资源的基本信息：

* **[!UICONTROL 网站名称]**

   设置为所选社区站点的名称：启用教程

* **[!UICONTROL 资源名称(&amp;A)；]**

   滑雪课程1

* **[!UICONTROL 标记]**

   教程：体育/滑雪

* **[!UICONTROL 在目录中显示]**

   将其设置为 **日期**.

* **[!UICONTROL 描述]**

   在雪上滑行，给初学者看。

* **[!UICONTROL 添加]**

   在成员的“工作总揽”视图中添加图像以表示该资源。

   ![basic-info](assets/basic-info.png)

* 选择 **[!UICONTROL 下一个]**

### 添加内容 {#add-content}

虽然看起来好像可以选择多个资源，但仅允许选择一个。

选择 `'+' icon`，开始通过标识源来选择资源的过程。

![add-content](assets/add-content.png)

![upload-resource](assets/upload-resource.png)

上传资源。 如果是视频资源，请在视频开始播放之前上传要显示的自定义图像，或者允许从视频生成缩略图（可能需要几分钟，无需等待）。

![upload-video](assets/upload-video.png)

* 选择&#x200B;**[!UICONTROL 下一步]**。

### 设置 {#settings}

* **[!UICONTROL 社交设置]**

   保留默认设置以体验学习者对启用资源进行评论和评级。

* **[!UICONTROL 到期日期]**

   *（可选）* 可选取应完成分配的日期。

* **[!UICONTROL 资源作者]**

   *（可选）* 留空。

* **[!UICONTROL 资源联系人(&amp;A)；]**

   *（必需）* 使用下拉菜单选择成员 `Quinn Harper`.

* **[!UICONTROL 资源专家]**

   *（可选）* 留空。

   **注释**：如果用户或组不可见，请检查它们是否已添加到 `Community Enable Members` 组和 *已保存* 在发布实例上。

   ![enablement-settings](assets/enablement-settings.png)

* 选择 **[!UICONTROL 下一个]**

### 指定任务 {#assignments}

* **[!UICONTROL 添加被分派人]**

   保留为未设置，因为此启用资源将添加到学习路径中。 如果将学习者分配给单个启用资源以及一个包含启用资源的学习路径，则会将学习者分配给启用资源两次。

   ![add-assigments](assets/add-assignments.png)

* 选择 **[!UICONTROL 创建]**

   ![create-resource](assets/create-resource.png)

成功创建资源后，将返回到资源控制台，并选中新创建的资源。 通过此控制台，您可以发布、添加学习者并更改其他设置。

要上传新版本的启用资源，建议创建一个新资源，然后从旧版本中取消注册成员并在新版本中注册这些成员。

### 发布资源 {#publish-the-resource}

必须先发布分配的资源，然后登记者才能查看这些资源：

* 选择世界 `Publish` 图标

确认激活并显示一条成功消息：

![publish-resource](assets/publish-resource.png)

## 添加第二个启用资源 {#add-a-second-enablement-resource}

重复上述步骤以创建并发布另一个相关的支持资源，从中创建学习路径。

![添加资源](assets/add-resource.png)

**Publish** 第二个资源。

返回到其资源的启用教程列表。

*提示：如果两个资源均不可见，请刷新页面。*

![refresh — 资源](assets/refresh-resource.png)

## 添加学习路径 {#add-a-learning-path}

学习路径是对构成课程的支持资源的逻辑分组。

* 从“资源”控制台中，选择 `+ Create`
* 选择 **[!UICONTROL 学习路径]**

![add-learning-path](assets/add-learning-path.png)

添加 **[!UICONTROL 基本信息]**：

* **[!UICONTROL 学习路径名称]**

   滑雪课程

* **[!UICONTROL 标记]**

   教程：滑雪

* **[!UICONTROL 在目录中显示]**

   保持未选中状态

* **[!UICONTROL 上传图像]**

   在“资源”控制台中表示学习路径。

   ![学习路径 — 基本](assets/learningpath-basic.png)

* 选择&#x200B;**[!UICONTROL 下一步]**。

跳过下一个面板，因为没有要添加的前提条件学习路径。

* 选择 **[!UICONTROL 下一个]**

在“添加资源”面板上：

* 选择 `+ Add Resources` 以选择要添加到学习路径的2个滑雪缆绳资源。

   注意：仅限 **已发布** 资源将可供选择。

>[!NOTE]
>
>您只能选择与学习路径处于同一级别的可用资源。 例如，对于在组中创建的学习路径，只有组级别的资源可用；对于在社区站点中创建的学习路径，该站点中的资源可用于添加到该学习路径中。

* 选择&#x200B;**[!UICONTROL 提交]**。

   ![学习路径](assets/learningpath-add.png)

   ![create-learningpath](assets/create-learningpath.png)

* 选择 **[!UICONTROL 下一个]**

   ![learningpath-settings](assets/learningpath-settings.png)

* **[!UICONTROL 添加被分派人]**

   使用下拉菜单选择 `Community Ski Class` 组，其中应包含成员 `Riley Taylor` 和 `Sidney Croft.`

* **[!UICONTROL 学习路径联系人&amp;ast；]**

   *（必需）* 使用下拉菜单选择成员 `Quinn Harper`.

* 选择&#x200B;**[!UICONTROL 创建]**。

   ![learningpath-info](assets/learningpath-info.png)

成功创建学习路径后，学习路径将返回到“资源”控制台，并选中新创建的学习路径。 通过此控制台，您可以发布、添加学习者并更改其他设置。

**Publish** 学习路径。
