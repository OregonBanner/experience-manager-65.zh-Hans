---
title: 注册为用户
seo-title: Registering as a User
description: 了解如何使用从Document Security用户那里收到的受策略保护的文档，即使您在该用户的组织之外也是如此。
seo-description: Learn how you can use policy-protected documents that you receive from an document security user, even if you are external to the user’s organization.
uuid: 4648b358-f545-434f-a3b2-2937e961dc64
products: SG_EXPERIENCEMANAGER/6.5/FORMS
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
discoiquuid: 26e11ef4-9f8f-4b0b-b035-a498fd7d65ef
feature: Document Security
exl-id: 320d8fa4-e200-4993-b018-a9718cddc5c1
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '700'
ht-degree: 6%

---

# 注册为用户 {#registering-as-a-user}

您可以使用从Document Security用户那里收到的受策略保护的文档，即使您在该用户的组织之外也是如此。 要使用受策略保护的文档，您必须向Document Security注册。 如果之前未邀请您注册，则Document Security会在发生以下事件时启动注册流程：

* 想要向您发送受策略保护文档的Document Security用户将您添加到策略中。
* Document Security管理员为您创建一个帐户。

   注册并激活帐户后，您可以使用策略授权您使用的受策略保护的文档。 如果Document Security管理员为受邀用户启用这些功能，则您可能有权执行这些任务：

* 使用Document Security策略创建Protect文档。
* 创建可应用于文档的用户策略。
* 通过将受策略保护的文档添加到策略，邀请其他外部用户使用这些文档。

   此外，在注册时，您无需再次注册即可使用其他受策略保护的文档。 您的帐户保持活动状态，直到策略管理员禁用或删除它。

>[!NOTE]
>
>如果您收到受策略保护的文档，但未收到注册电子邮件邀请，请联系向您发送文档的人以获取更多信息。

## 注册为受邀用户 {#register-as-an-invited-user}

如果您是受邀用户，并且收到来自document security的电子邮件注册消息，则可以使用消息中的URL进行注册，以打开在线注册页面。 在注册之后，您将收到有关激活帐户的第二个通知。

1. 打开document security注册电子邮件。 邮件包含的URL是指向Document Security中的“外部用户注册”页面的链接。
1. 单击 URL 或者复制并将其粘贴到浏览器中。此时将显示“外部用户注册”页面。
1. 在相应的框中键入您的姓名、电话号码、地址、组织和密码，然后在“确认密码”框中重新键入您的密码。 您的密码可以是任意八个字符的组合。
1. 单击“保存”。此时会显示一条感谢消息，通知您检查电子邮件中的激活电子邮件。 您现在必须激活帐户才能完成注册过程。

## 激活您的受邀用户帐户 {#activate-your-invited-user-account}

注册后，Document Security会向您发送一封激活电子邮件。 您必须使用邮件中的URL激活帐户。 然后，您可以登录到Document Security以使用您有权访问的受策略保护的文档。 根据管理员为外部用户启用的功能，您可能具有创建策略、将策略应用到文档以及将其他外部用户添加到策略的权限。

在管理员停用或删除您的帐户之前，该帐户保持活动状态。

1. 打开Document Security注册确认电子邮件。
1. 单击邮件中显示的 URL。此时将显示Document Security激活页面。
1. 单击“Here（此处）”以转到登录页面。
1. 在用户名框中，键入您在Document Security下注册的电子邮件地址。 此电子邮件地址是您的默认Document Security用户名。
1. 在“密码”框中，键入注册时创建的密码，然后单击“登录”。

## 重置密码 {#reset-your-password}

如果忘记了密码，策略管理员可以为您重置密码。 重置密码会生成一封电子邮件，邀请您使用临时密码登录。 然后，您可以创建新密码。

有关联系Document Security管理员以获取新密码的信息，请查看您的激活电子邮件通知或邀请您注册的组织的其他通知。

1. 通知策略管理员您需要新密码。
1. 当您收到Document Security密码电子邮件时，请打开它并获取新的临时密码。
1. 使用新的临时密码登录到Document Security。
1. 单击页面右上角的选项。 此时会显示“外部用户”页面。
1. 选择“更改密码”，然后在“旧密码”框中键入临时密码。
1. 在“新密码”框中，键入新密码，然后在“确认密码”框中重新键入。
