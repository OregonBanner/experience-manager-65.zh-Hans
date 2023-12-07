---
title: Granite操作 — 用户和组管理
description: 了解Granite用户和组管理。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
exl-id: f3477d21-7e9a-4588-94e8-496bc42434a8
feature: Security
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '951'
ht-degree: 1%

---


# Granite操作 — 用户和组管理{#granite-operations-user-and-group-administration}

由于Granite采用了JCR API规范的CRX存储库实施，因此它拥有自己的用户和组管理。

该等账目乃本集团所有主要客户 [AEM帐户](/help/sites-administering/security.md) 并且，如果从访问帐户，则通过Granite管理所做的任何帐户更改都将得到反映。 [AEM用户控制台](/help/sites-administering/security.md#accessing-user-administration-with-the-security-console) (例如， `http://localhost:4502/useradmin`)。 从AEM Users控制台中，您还可以管理权限和其他AEM详细信息。

Granite用户和组管理控制台均可从 **[工具](/help/sites-administering/tools-consoles.md)** 触屏优化UI的控制台：

![工具控制台](assets/chlimage_1-72a.png)

选择 **用户** 或 **组** 从“工具”控制台中打开相应的控制台。 在这两种情况下，您可以通过以下方式执行操作：使用点击框，然后从工具栏执行操作，或通过下面的链接打开帐户详细信息 **名称**.

* [用户管理](#user-administration)

  ![chlimage_1-73](assets/chlimage_1-73a.png)

  此 **用户** 控制台列表：

   * 用户名
   * 用户登录名（帐户名）
   * 已指定帐户的任何标题

* [组管理](#group-administration)

  ![User Management 控制台](assets/chlimage_1-74a.png)

  此 **组** 控制台列表：

   * 组名称
   * 组描述
   * 组中的用户/组数

## 用户管理 {#user-administration}

### 添加新用户 {#adding-a-new-user}

1. 使用 **添加用户** 图标：

   ![“添加用户”图标](do-not-localize/chlimage_1-1.png)

1. 此 **创建用户** 表单打开：

   ![用户详细信息表单](assets/chlimage_1-75a.png)

   您可以在此输入帐户的用户详细信息（大部分是标准且无需解释）：

   * **ID**

     这是用户帐户的唯一标识。 它是必填项，不能包含空格。

   * **电子邮件地址**
   * **密码**

     必须输入密码。

   * **重新键入密码**

     这是强制性的，因为确认密码需要它。

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

      * **状态**
您可以将帐户标记为以下任一类型 **活动** 或 **不活动**.

   * **照片**

     您可以在此处上传照片以用作头像。

     接受的文件类型： `.jpg .png .tif .gif`

     首选大小： `240x240px`

   * **将用户添加到组**

     使用选择下拉列表选择用户应成为其成员的组。 选择后，使用 **X** ，在保存前取消选择。

   * **组**

     用户当前所属的组的列表。 使用 **X** ，在保存前取消选择。

1. 定义用户帐户后，使用：

   * **取消** 中止注册。
   * **保存** 以完成注册。 将通过一条消息确认创建用户帐户。

### 编辑现有用户 {#editing-an-existing-user}

1. 从用户控制台中用户名下的链接访问用户详细信息。

1. 您现在可以在中编辑详细信息 [添加新用户](#adding-a-new-user).

1. 从用户控制台中用户名下的链接访问用户详细信息。

1. 您现在可以在中编辑详细信息 [添加新用户](#adding-a-new-user).

### 更改现有用户的密码 {#changing-the-password-for-an-existing-user}

1. 从用户控制台中用户名下的链接访问用户详细信息。

1. 您现在可以在中编辑详细信息 [添加新用户](#adding-a-new-user). 下 **帐户设置** 有一个链接 **更改密码**.

   ![“帐户设置”对话框](assets/chlimage_1-76a.png)

1. 此 **更改密码** 对话框打开。 输入并重新键入新密码以及您的密码。 使用 **确定** 以确认更改。

   ![“更改密码”对话框](assets/chlimage_1-77a.png)

   将显示一条消息，确认密码已更改。

### 快速组分配 {#quick-group-assignment}

1. 使用点击框标记一个或多个用户。
1. 使用 **组** 图标：

   ![使用“组”图标](do-not-localize/chlimage_1-2.png)

   要打开组选择下拉列表，请执行以下操作：

   ![组选择器](assets/chlimage_1-78a.png)

1. 在选择框中，您可以选择或取消选择用户帐户所属的组。

1. 当已分配或未分配组时，根据需要使用：

   * **取消** 中止更改
   * **保存** 以确认更改

### 删除现有用户详细信息 {#deleting-existing-user-details}

1. 使用点击框标记一个或多个用户。
1. 使用 **删除** 图标以删除用户详细信息：

   ![删除现有用户详细信息](do-not-localize/chlimage_1-3.png)

1. 系统会要求您确认删除，然后会显示一条消息，确认已执行实际删除。

## 组管理 {#group-administration}

### 添加新组 {#adding-a-new-group}

1. 使用“添加群组”图标：

   ![添加新组](do-not-localize/chlimage_1-4.png)

1. 此 **创建组** 表单打开：

   ![组详细信息表单](assets/chlimage_1-79a.png)

   您可以在此输入组详细信息：

   * **ID**

     这是组的唯一标识符。 这是必填项，不能包含空格。

   * **名称**

     组的名称；它显示在“组”控制台中。

   * **描述**

     组的描述。

   * **将成员添加到组**

     使用选择下拉列表选择要添加到组中的用户。 选择后，使用 **X** ，在保存前取消选择。

   * **组成员**

     组中的用户列表。 使用 **X** ，在保存前取消选择。

1. 定义组后，使用：

   * **取消** 中止注册。
   * **保存** 以完成注册。 将通过一条消息确认组的创建。

### 编辑现有组 {#editing-an-existing-group}

1. 从组控制台中组名称下的链接访问组详细信息。

1. 您现在可以在中编辑并保存详细信息 [添加新组](#adding-a-new-group).

### 复制现有组 {#copying-an-existing-group}

1. 使用点击框标记组。
1. 使用 **复制** 图标以复制组详细信息：

   ![复制现有组](do-not-localize/chlimage_1-5.png)

1. 此 **编辑组设置** 窗体将被打开。

   组ID将与原始组相同，但带有前缀 `Copy of`. 编辑此ID，因为它不能包含空格。 所有其他细节与原始细节相同。

   您现在可以在中编辑并保存详细信息 [添加新组](#adding-a-new-group).

### 删除现有组 {#deleting-an-existing-group}

1. 使用点击框标记一个或多个组。
1. 使用 **删除** 图标以删除组详细信息：

   ![删除现有组](do-not-localize/chlimage_1-6.png)

1. 系统会要求您确认删除，然后会显示一条消息，确认已执行实际删除。
