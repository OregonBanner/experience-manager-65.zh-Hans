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

---


# Granite Operations —— 用户和组管理{#granite-operations-user-and-group-administration}

随着Granite整合了JCR API规范的CRX存储库实施，它拥有自己的用户和组管理。

这些帐户是 [AEM帐户的基础](/help/sites-administering/security.md) ，如果通过 [](/help/sites-administering/security.md#accessing-user-administration-with-the-security-console) AEM用户控制台访问帐户，则使用Granite管理所做的任何帐户更改都将反映出来(例如， `http://localhost:4502/useradmin`)。 从AEM用户控制台中，您还可以管理权限和其他AEM特定信息。

Granite用户和组管理控制台都可从触屏优化UI的 **[“工具](/help/sites-administering/tools-consoles.md)**”控制台中使用：

![chlimage_1-72](assets/chlimage_1-72a.png)

从“工 **具** ”控制台 **中选择“用户** ”或“用户组”将打开相应的控制台。 在这两种情况下，您都可以通过单击框，然后从工具栏中执行操作，或通过“名称”下的链接打开帐户详细 **信息**。

* [用户管理](#user-administration)

   ![chlimage_1-73](assets/chlimage_1-73a.png)

   “用 **户** ”控制台列出：

   * 用户名
   * 用户登录名（帐户名）
   * 给予帐户的任何标题

* [组管理](#group-administration)

   ![chlimage_1-74](assets/chlimage_1-74a.png)

   “组 **”控制台** 列出：

   * 用户组名称
   * 用户组说明
   * 用户组中的用户／用户组数

## 用户管理 {#user-administration}

### 添加新用户 {#adding-a-new-user}

1. 使用“添 **加用户** ”图标：

   ![](do-not-localize/chlimage_1-1.png)

1. 此时将 **打开“创建用户** ”表单：

   ![chlimage_1-75](assets/chlimage_1-75a.png)

   您可以在此输入帐户的用户详细信息（大多数是标准和自解释的）:

   * **ID**

      这是用户帐户的唯一标识。 它是必填项，不能包含空格。

   * **电子邮件地址**
   * **密码**

      密码为必填项。

   * **重新键入密码**

      这是必填项，因为确认密码时需要这样做。

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

      * **状态**&#x200B;您可以将帐户标记为活动 **或不活** 动 ****。
   * **照片**

      您可以在此处上传照片以用作头像。

      接受的文件类型: `.jpg .png .tif .gif`

      首选大小： `240x240px`

   * **将用户添加到组**

      使用选择下拉列表选择用户应为其成员的组。 选择后，在保存前 **使用** X（按名称）取消选择。

   * **组**

      用户当前为其成员的组列表。 在保存 **之前** ，使用名称旁的X取消选择。


1. 定义用户帐户使用时：

   * **取消** ，以中止注册。
   * **保存** ，以完成注册。 用户帐户的创建将确认并显示一条消息。

### 编辑现有用户 {#editing-an-existing-user}

1. 从“用户”控制台中用户名下的链接访问用户详细信息。

1. 您现在可以像添加新用户中 [那样编辑详细信息](#adding-a-new-user)。

1. 从“用户”控制台中用户名下的链接访问用户详细信息。

1. 您现在可以像添加新用户中 [那样编辑详细信息](#adding-a-new-user)。

### 更改现有用户的密码 {#changing-the-password-for-an-existing-user}

1. 从“用户”控制台中用户名下的链接访问用户详细信息。

1. 您现在可以像添加新用户中 [那样编辑详细信息](#adding-a-new-user)。 在“ **帐户设置** ”下，有一个“更改密 **码”链接**。

   ![chlimage_1-76](assets/chlimage_1-76a.png)

1. 将打 **开“更改密码** ”对话框。 输入新密码并重新键入新密码。 使用 **确定** ，以确认更改。

   ![chlimage_1-77](assets/chlimage_1-77a.png)

   系统会显示一条消息，确认密码已更改。

### 快速组分配 {#quick-group-assignment}

1. 使用单击框标记一个或多个用户。
1. Use the **Groups** icon:

   ![](do-not-localize/chlimage_1-2.png)

   要打开用户组选择下拉列表，请执行以下操作：

   ![chlimage_1-78](assets/chlimage_1-78a.png)

1. 在选择框中，您可以选择或取消选择用户帐户应属于的组。

1. 在您已分配或未分配用户组时，请根据需要使用：

   * **取消** ，以中止更改
   * **保存** ，以确认更改

### 删除现有用户详细信息 {#deleting-existing-user-details}

1. 使用单击框标记一个或多个用户。
1. 使用“删 **除** ”图标删除用户详细信息：

   ![](do-not-localize/chlimage_1-3.png)

1. 系统会要求您确认删除，然后会显示一条消息，确认实际删除操作已经完成。

## 组管理 {#group-administration}

### 添加新组 {#adding-a-new-group}

1. 使用“添加组”图标：

   ![](do-not-localize/chlimage_1-4.png)

1. 此时将 **打开创建** “组”表单：

   ![chlimage_1-79](assets/chlimage_1-79a.png)

   您可以在此输入用户组详细信息：

   * **ID**

      这是组的唯一标识符。 这是必填项，不能包含空格。

   * **名称**

      用户组的名称；它将显示在“组”控制台中。

   * **描述**

      用户组的说明。

   * **将成员添加到组**

      使用选择下拉列表选择要添加到用户组的用户。 选择后，在保存前 **使用** X（按名称）取消选择。

   * **组成员**

      用户组中的用户列表。 在保存 **之前** ，使用名称旁的X取消选择。

1. 定义用户组后，请使用：

   * **取消** ，以中止注册。
   * **保存** ，以完成注册。 用户组的创建将通过消息确认。

### 编辑现有组 {#editing-an-existing-group}

1. 从“组”控制台中组名称下的链接访问组详细信息。

1. 您现在可以像添加新组中那样编辑 [和保存详细信息](#adding-a-new-group)。

### 复制现有组 {#copying-an-existing-group}

1. 使用单击框标记组。
1. 使用复 **制图标** ，可复制组详细信息：

   ![](do-not-localize/chlimage_1-5.png)

1. 将 **打开“编辑组设置** ”表单。

   组ID将与原始ID相同，但前缀为 `Copy of`。 您必须编辑它，因为ID不能包含空格。 所有其他详细信息将与原始信息相同。

   您现在可以像添加新组中那样编辑 [和保存详细信息](#adding-a-new-group)。

### 删除现有组 {#deleting-an-existing-group}

1. 使用单击框标记一个或多个组。
1. 使用删 **除图标** ，可删除用户组详细信息：

   ![](do-not-localize/chlimage_1-6.png)

1. 系统会要求您确认删除，然后会显示一条消息，确认实际删除操作已经完成。

