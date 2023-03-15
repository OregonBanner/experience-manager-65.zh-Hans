---
title: 管理受邀的用户帐户和本地用户帐户
seo-title: Managing invited and local user accounts
description: 使用Document Security，您可以搜索、查看、编辑、锁定、解锁和删除受邀和本地用户帐户。
seo-description: Using document security, you can search for, view, edit, lock, unlock, and delete invited and local user accounts.
uuid: 0d0c717a-6e6e-4e42-96eb-3a7166e215ab
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 65720eed-ab06-463f-9567-2fdc468b6219
feature: Document Security
exl-id: 23f71b34-a0cb-4664-bb8b-a60f33dc70d8
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1196'
ht-degree: 0%

---

# 管理受邀的用户帐户和本地用户帐户 {#managing-invited-and-local-user-accounts}

使用“受邀用户和本地用户”页可以管理受邀用户和本地用户。 仅当满足以下要求时，才会显示此页：

* 您是已分配Document Security管理受邀用户和本地用户角色和管理控制台用户角色的管理员。 (请参阅 [创建和配置角色](/help/forms/using/admin-help/creating-configuring-roles.md#creating-and-configuring-roles).)
* 已启用受邀用户注册。 (请参阅 [配置受邀用户注册](/help/forms/using/admin-help/configuring-client-server-options.md#configuring-invited-user-registration).)

“受邀用户和本地用户”页包含两个选项卡，您可以使用这两个选项卡搜索、查看、编辑、锁定、解锁和删除受邀用户和本地用户帐户。

您还可以手动向受邀用户发送注册电子邮件。 例如，如果电子邮件授权的注册期结束，并且用户无法使用URL进行注册，则可能需要执行此操作。 在这种情况下，您可以向受邀用户重新发送注册电子邮件。 当受邀用户注册并激活帐户时，该用户将成为本地用户。

>[!NOTE]
>
>也可以直接通过文档安全引用的LDAP目录添加受邀用户，或者在用户或管理员创建或编辑策略时邀请新用户，从而启动注册邀请电子邮件时。 如果在“受邀用户注册”页面上启用了“启用受邀用户注册”选项，则用户可以将新的受邀用户添加到策略中。

## 添加受邀用户 {#add-an-invited-user}

您可以一次添加一个或多个受邀用户帐户到Document Security。 要添加受邀用户帐户，您需要该用户的电子邮件地址。 添加用户时，document security会发送一封注册电子邮件，邀请用户注册。

1. 在管理控制台中，单击“服务”>“Document Security”>“受邀用户和本地用户”，然后单击“邀请新用户”。
1. 键入要邀请的用户的电子邮件地址。 在一行中输入多个地址，用逗号分隔。

   您在启用受邀用户注册时创建的消息将发送给用户。 (请参阅 [配置受邀用户注册](/help/forms/using/admin-help/configuring-client-server-options.md#configuring-invited-user-registration).)

1. 单击确定。

## 查看有关本地用户的信息 {#view-information-about-a-local-user}

您可以查看有关本地用户的信息，包括名称、电子邮件地址、组织、注册状态和域。

1. 在管理控制台中，单击“服务”>“Document Security”>“受邀用户和本地用户”，然后单击“邀请新用户”。
1. 单击“本地用户”选项卡，然后在“管理本地用户”页面上，单击要查看的用户的电子邮件地址。

   将显示用户详细信息，您可以重置用户的密码并停用帐户。

## 向未注册的外部用户发送电子邮件 {#send-an-email-to-an-unregistered-external-user}

添加受邀用户时，Document Security会自动向用户发送注册电子邮件请求。 您还可以手动生成注册电子邮件，以发送给尚未注册的受邀用户。 例如，如果受邀用户的注册电子邮件过期，则可能需要执行上述操作，以发送新的邀请。

1. 在管理控制台中，单击“服务”>“Document Security”>“受邀用户和本地用户”。
1. 在用户列表中，选中每个要向其发送注册电子邮件的用户的复选框，然后单击“重新发送邀请电子邮件”。
1. 查看所选用户的列表，然后单击“确定”。

## 重置本地用户密码 {#reset-a-local-user-password}

您可以为已注册Document Security但忘记密码的激活的受邀用户重置密码。 重置密码时，会生成一封电子邮件，其中包含用户的新临时密码。

启用受邀用户注册过程后，您创建了一条电子邮件消息，该消息将发送给用户，提示他们重置密码。 (请参阅 [配置受邀用户注册](/help/forms/using/admin-help/configuring-client-server-options.md#configuring-invited-user-registration).)

1. 在管理控制台中，单击“服务”>“Document Security”>“受邀用户和本地用户”，然后单击“本地用户”选项卡。
1. 在用户列表中，选择适当的用户。
1. 在“管理本地用户”页上，单击“重置密码”，然后单击“确定”。 包含新密码的重置密码电子邮件将发送给用户。

## 启用或禁用用户帐户 {#enable-or-disable-a-user-account}

您可以禁用本地用户帐户，以暂时限制用户登录Document Security。 禁用帐户后，用户无法使用受策略保护的文档，也无法创建或应用策略。

您可以启用当前禁用的本地用户帐户。 无法启用列为已注册的受邀请用户帐户。 注册状态表示受邀用户已注册，但尚未使用激活电子邮件中的链接激活帐户。

**限制用户帐户**

1. 在Administration Console中，单击“服务”>“Document Security”>“受邀用户和本地用户”，然后单击“本地用户”选项卡。
1. 在用户列表中，选择适当的用户。
1. 在“本地用户详细信息”页面上，单击“帐户禁用”。

**恢复用户帐户**

1. 单击受邀用户和本地用户，然后单击本地用户选项卡。
1. 在用户列表中，选择适当的用户。
1. 在“本地用户详细信息”页面上，单击“帐户启用”。

## 删除受邀请的用户帐户 {#remove-an-invited-user-account}

您可以从Document Security删除受邀用户帐户。 例如，当用户更改其个人电子邮件帐户信息时，您可能希望删除帐户。

如果删除用户帐户，则只有您或其他管理员可以通过选择“受邀用户”页面上的“添加受邀用户”选项来恢复帐户。 用户无法将已删除的用户帐户添加到策略中，并且无法通过该方法启动任何邀请过程。

>[!NOTE]
>
>对于通过AEM Forms User Management界面删除的受邀用户，只有在再次通过以下过程删除之后，才能将其重新激活。

1. 在管理控制台中，单击“服务”>“Document Security”>“受邀用户和本地用户”，然后单击“受邀用户”选项卡。
1. 选中一个或多个用户旁边的复选框，单击删除，然后单击确定。

## 搜索受邀的用户帐户 {#search-for-an-invited-user-account}

您可以使用电子邮件地址搜索受邀的用户帐户。

1. 在管理控制台中，单击“服务”>“Document Security”>“受邀用户和本地用户”。
1. 在查找电子邮件框中，键入用户的电子邮件地址，然后单击查找。

## 搜索本地用户帐户 {#search-for-a-local-user-account}

您可以使用用户的电子邮件地址或名称和域搜索本地用户。

1. 在管理控制台中，单击“服务”>“Document Security”>“受邀用户和本地用户”，然后单击“本地用户”选项卡。
1. 在“查找”框中键入搜索条件，选择“名称”或“电子邮件”，然后单击“查找”。

## 删除本地用户帐户 {#remove-a-local-user-account}

您可以从Document Security中删除本地用户帐户。 例如，当用户更改其个人电子邮件帐户信息时，您可能希望删除帐户。

1. 在管理控制台中，单击“服务”>“Document Security”>“受邀用户和本地用户”，然后单击“本地用户”选项卡。
1. 选中一个或多个用户旁边的复选框，单击删除，然后单击确定。

## 对用户列表进行排序 {#sort-the-user-list}

通过按列标题对用户列表进行排序，可以更轻松地查找用户。 列标题旁边的三角形图标指示当前使用哪一列进行排序：

* 向上指的三角形表示升序。
* 向下指的三角形表示降序。

   1. 在管理控制台中，单击“服务”>“Document Security”>“受邀用户和本地用户”。
   1. 要对受邀用户进行排序，请单击受邀用户选项卡，然后单击相应的列标题。
   1. 要对本地用户进行排序，请单击“本地用户”选项卡，然后单击相应的列标题。
