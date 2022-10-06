---
title: 配置共享队列
seo-title: Configure shared queues
description: 了解如何在OSGi上的AEM Forms上将共享队列用于以Forms为中心的工作流。
seo-description: Learn how to use shared queues for Forms-centric workflows on AEM Forms on OSGi.
topic-tags: process
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
exl-id: 72cd0594-8b5e-4d14-bc6f-bca26bae50f2
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '841'
ht-degree: 1%

---

# 共享和请求对用户收件箱项目的访问权限 {#share-and-request-access}

队列是用户AEM收件箱中的项目列表。 这些项目可以是分配给用户的项目，也可以是分配给用户所属的组的项目。 您可以访问收件箱以查看收件箱项目并对其执行操作。 例如，与其他用户共享项目。

您还可以与其他用户共享您的收件箱项目。 当其他用户有权访问您的收件箱项目时，用户可以声明共享项目并对其采取适当的操作。 同样，您也可以请求其他用户访问收件箱项目。

## 先决条件 {#pre-requisites}

登录用户必须是 `workflow-users` 群组。 用户只能从登录用户具有读取权限的用户或仅从启用了公共配置文件的用户共享项目或请求对项目的访问权限。

## 与其他用户共享您收件箱的单个或所有项目

AEM收件箱允许您与其他用户共享收件箱中的单个或所有项目。

### 共享所有收件箱项目

执行以下步骤，将收件箱中的所有项目与其他用户共享：

1. 登录到您的AEM实例。 点按 ![收件箱](assets/bell.svg) 图标，点按 **[!UICONTROL 查看全部]**. 此时会显示收件箱项目的列表。
1. 点按 ![视图选择器](assets/viewlist.svg) 或 ![视图选择器](assets/calendar.svg) 图标 **[!UICONTROL 创建]** 按钮和点按 **[!UICONTROL 设置]**. 此时会出现“设置”对话框。
1. 打开 **[!UICONTROL 共享]** 选项卡。
1. 在 **[!UICONTROL 授予对收件箱项目的访问权限]** 文本框和点按 **[!UICONTROL 授予]**. 重复此步骤以添加更多用户。 所有有权访问您项目的用户都显示在 **用户名** 中。
1. 点按&#x200B;**[!UICONTROL 保存]**。

>[!NOTE]
>
>(仅限以Forms为中心的工作流项目)启用 **[允许被分派人通过收件箱共享进行共享](aem-forms-workflow-step-reference.md)** 的 **分配任务** 中的步骤。 只有启用了上述选项的项目才会显示给其他用户。

### 共享单个项目

执行以下步骤以与其他用户共享收件箱项目：

1. 登录到您的AEM实例。 点按 ![收件箱](assets/bell.svg) 图标，点按 **[!UICONTROL 查看全部]**. 此时会显示收件箱项目的列表。
1. 选择项目并点按 **[!UICONTROL 共享]**. 将显示一个对话框。
1. 在“添加用户以共享此项目”文本框中输入用户的名称，然后点按 **[!UICONTROL 添加]**. 重复此步骤以添加更多用户。 所有有权访问您项目的用户都显示在 **[!UICONTROL 用户名]** 中。
1. 点按&#x200B;**[!UICONTROL 保存]**。


>[!NOTE]
>
>(仅限以Forms为中心的工作流项目)启用 **[允许被分派人在收件箱中明确共享](aem-forms-workflow-step-reference.md)** 的 **分配任务** 中的步骤。 只有启用了上述选项的项目才会显示给其他用户。

## 请求访问收件箱项目 {#request-access}

您可以请求访问其他用户的收件箱项目。 授予访问权限后，您可以查看、声明和对共享项目采取适当的操作。 请执行以下步骤以请求访问其他用户的收件箱项目：

1. 登录到您的AEM实例。 点按 ![视图选择器](assets/bell.svg) 图标，点按 **[!UICONTROL 查看全部]**.
1. 点按 ![视图选择器](assets/viewlist.svg) 或 ![视图选择器](assets/calendar.svg) 图标 **[!UICONTROL 创建]** 按钮和点按 **[!UICONTROL 设置]**. 此时会出现“设置”对话框。
1. 在 **[!UICONTROL 请求对用户收件箱项目的访问权限]** 文本框和点按 **[!UICONTROL 请求]**. 向用户发送请求，并根据用户的名称显示请求的状态。 重复此步骤以添加更多用户。
1. 点按&#x200B;**[!UICONTROL 保存]**。该请求将作为收件箱项目发送给用户。 用户可以选择项目并点按批准或拒绝以授予或拒绝访问权限。


## 其他用户共享的声明项目 {#claim-items}

只有在声明共享项目后，才能开始处理该项目。 它可阻止多个用户处理单个项目。 执行以下步骤以声明项目：

1. 登录到您的AEM实例。 点按收件箱 ![收件箱](assets/bell.svg) 图标，点按 **[!UICONTROL 查看全部]**.
1. 点按 ![仅限内容](assets/railleft.svg) 图标以打开过滤器选择器。
1. 点按 **[!UICONTROL 选择被分派人]** 下拉列表可查看和选择与您共享其收件箱项目的用户。
1. 选择项目并点按 **[!UICONTROL 索赔]**. 该项目会添加到您的收件箱中。

## 释放索赔项目 {#release-items}

只有在您声明共享项目后，才能处理该项目。 其他用户无法查看或处理您声明的项目。 如果无法继续处理某个项目，则可将其释放回池。   在您发布项目后，其他人可以声明并处理该项目：

执行以下步骤以释放项目：

1. 登录到您的AEM实例。 点按收件箱 ![收件箱](assets/bell.svg) 图标，点按 **[!UICONTROL 查看全部]**. 此时会显示收件箱项目的列表。
1. 选择要释放的项目并点按 **[!UICONTROL UnClaim]**. 该项目会添加回池中。 其他人现在可以声明该项目。

## 限制 {#limitations}

* 不支持与组共享项目。
* 不支持共享项目任务。
