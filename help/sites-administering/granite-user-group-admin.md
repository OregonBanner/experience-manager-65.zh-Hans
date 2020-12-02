---
title: Granite Operations —— 用户和组管理
seo-title: Granite Operations —— 用户和组管理
description: 了解Granite用户和组管理。
seo-description: 了解Granite用户和组管理。
uuid: 7b6b7767-712c-4cc8-8d90-36f26280d6e3
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 95ab2e54-0f8d-49e0-ad20-774875f6f80a
translation-type: tm+mt
source-git-commit: 0eda6ee61acf737abc91d1e5df731e719663b3f2
workflow-type: tm+mt
source-wordcount: '936'
ht-degree: 4%

---


# Granite Operations —— 用户和组管理{#granite-operations-user-and-group-administration}

随着Granite采用JCR API规范的CRX存储库实施，它拥有自己的用户和组管理。

这些帐户是[AEM帐户](/help/sites-administering/security.md)的基础，如果／当从[AEM用户控制台](/help/sites-administering/security.md#accessing-user-administration-with-the-security-console)访问帐户时，将反映使用Granite管理所做的任何帐户更改(例如，`http://localhost:4502/useradmin`)。 从AEM用户控制台中，您还可以管理权限和其他AEM特定信息。

Granite用户和组管理控制台均可从触屏优化UI的&#x200B;**[工具](/help/sites-administering/tools-consoles.md)**&#x200B;控制台中访问：

![chlimage_1-72](assets/chlimage_1-72a.png)

从工具控制台中选择&#x200B;**用户**&#x200B;或&#x200B;**组**&#x200B;将打开相应的控制台。 在这两种情况下，您都可以先使用单击框，然后从工具栏中执行操作，或者通过&#x200B;**名称**&#x200B;下的链接打开帐户详细信息。

* [用户管理](#user-administration)

   ![chlimage_1-73](assets/chlimage_1-73a.png)

   **Users**&#x200B;控制台列表:

   * 用户名
   * 用户登录名（帐户名）
   * 已授予帐户的任何标题

* [组管理](#group-administration)

   ![chlimage_1-74](assets/chlimage_1-74a.png)

   **组**&#x200B;控制台列表符：

   * 用户组名称
   * 组描述
   * 组中的用户／组数

## 用户管理{#user-administration}

### 添加新用户{#adding-a-new-user}

1. 使用&#x200B;**添加用户**&#x200B;图标：

   ![](do-not-localize/chlimage_1-1.png)

1. 将打开&#x200B;**创建用户**&#x200B;表单：

   ![chlimage_1-75](assets/chlimage_1-75a.png)

   您可以在此输入帐户的用户详细信息（大多数是标准的和自解释的）:

   * **ID**

      这是用户帐户的唯一标识。 它是强制的，不能包含空格。

   * **电子邮件地址**
   * **密码**

      密码是必填项。

   * **重新键入密码**

      这是必填项，因为确认密码时需要它。

   * **名字**
   * **姓氏**
   * **电话号码**
   * **职务**
   * **街道**
   * **移动设备**
   * **城市**
   * **邮政编码**
   * **国家/地区**
   * **状态**
   * **标题**
   * **性别**
   * **关于**
   * **帐户设置**

      * **状**
态您可以将帐户标记为 
**活动** 或不 **活动**。
   * **照片**

      您可以在此上传照片以用作头像。

      接受的文件类型: `.jpg .png .tif .gif`

      首选大小：`240x240px`

   * **将用户添加到组**

      使用选择下拉列表选择用户应为其成员的组。 选择后，在保存前使用名称中的&#x200B;**X**&#x200B;取消选择。

   * **组**

      用户当前为其成员的组列表。 保存前，请使用名称中的&#x200B;**X**&#x200B;取消选择。


1. 定义用户帐户使用时：

   * **取消** 以中止注册。
   * **Saveto** 完成注册。用户帐户的创建将会收到一条消息。

### 编辑现有用户{#editing-an-existing-user}

1. 从“用户”控制台中用户名下的链接访问用户详细信息。

1. 现在，您可以编辑详细信息，如[添加新用户](#adding-a-new-user)中所示。

1. 从“用户”控制台中用户名下的链接访问用户详细信息。

1. 现在，您可以编辑详细信息，如[添加新用户](#adding-a-new-user)中所示。

### 更改现有用户{#changing-the-password-for-an-existing-user}的口令

1. 从“用户”控制台中用户名下的链接访问用户详细信息。

1. 现在，您可以编辑详细信息，如[添加新用户](#adding-a-new-user)中所示。 在&#x200B;**帐户设置**&#x200B;下，有一个链接用于&#x200B;**更改密码**。

   ![chlimage_1-76](assets/chlimage_1-76a.png)

1. 将打开&#x200B;**更改密码**&#x200B;对话框。 输入并重新键入新密码以及密码。 使用&#x200B;**OK**&#x200B;确认更改。

   ![chlimage_1-77](assets/chlimage_1-77a.png)

   将显示一条消息，确认密码已更改。

### 快速组分配{#quick-group-assignment}

1. 使用该复选框标记一个或多个用户。
1. 使用&#x200B;**组**&#x200B;图标：

   ![](do-not-localize/chlimage_1-2.png)

   要打开组选择下拉列表，请执行以下操作：

   ![chlimage_1-78](assets/chlimage_1-78a.png)

1. 在选择框中，可以选择或取消选择用户帐户应属于的组。

1. 在您已分配或未分配用户组时，请根据需要使用：

   * **取消** 以中止更改
   * **萨** 韦托确认更改

### 删除现有用户详细信息{#deleting-existing-user-details}

1. 使用该复选框标记一个或多个用户。
1. 使用&#x200B;**删除**&#x200B;图标删除用户详细信息：

   ![](do-not-localize/chlimage_1-3.png)

1. 系统会要求您确认删除，然后会显示一条消息，确认已实际删除。

## 组管理{#group-administration}

### 添加新组{#adding-a-new-group}

1. 使用“添加组”图标：

   ![](do-not-localize/chlimage_1-4.png)

1. 将打开&#x200B;**创建组**&#x200B;表单：

   ![chlimage_1-79](assets/chlimage_1-79a.png)

   您可以在此输入组详细信息：

   * **ID**

      这是组的唯一标识符。 这是必填项，不能包含空格。

   * **名称**

      组的名称；它将显示在“组”控制台中。

   * **描述**

      组的描述。

   * **将成员添加到组**

      使用选择下拉列表选择要添加到组的用户。 选择后，在保存前使用名称中的&#x200B;**X**&#x200B;取消选择。

   * **组成员**

      组中用户的列表。 保存前，请使用名称中的&#x200B;**X**&#x200B;取消选择。

1. 定义组后，请使用：

   * **取消** 以中止注册。
   * **Saveto** 完成注册。用户组的创建将通过消息进行确认。

### 编辑现有组{#editing-an-existing-group}

1. 从“组”控制台中组名称下的链接访问组详细信息。

1. 现在，您可以编辑并保存详细信息，如[添加新组](#adding-a-new-group)中所示。

### 复制现有组{#copying-an-existing-group}

1. 使用单击框标记组。
1. 使用&#x200B;**复制**&#x200B;图标复制组详细信息：

   ![](do-not-localize/chlimage_1-5.png)

1. 将打开&#x200B;**编辑组设置**&#x200B;表单。

   组ID将与原始ID相同，但前缀为`Copy of`。 您必须编辑此项，因为ID不能包含空格。 所有其他详细信息将与原始信息相同。

   现在，您可以编辑并保存详细信息，如[添加新组](#adding-a-new-group)中所示。

### 删除现有组{#deleting-an-existing-group}

1. 使用单击框标记一个或多个组。
1. 使用&#x200B;**删除**&#x200B;图标删除组详细信息：

   ![](do-not-localize/chlimage_1-6.png)

1. 系统会要求您确认删除，然后会显示一条消息，确认已实际删除。

