---
title: 配置共享队列
seo-title: Configure shared queues
description: 了解如何在OSGi上为AEM Forms上的以Forms为中心的工作流使用共享队列。
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

# 共享和请求访问用户的收件箱项目 {#share-and-request-access}

队列是用户的AEM收件箱中的项目列表。 这些项目可以是分配给用户的项目，也可以是分配给用户所属的组的项目。 您可以访问收件箱以查看收件箱项目并对其执行操作。 例如，与其他用户共享项目。

您还可以与其他用户共享收件箱项目。 一旦另一用户有权访问您的收件箱项目，该用户可以声明共享项目并对其采取适当措施。 同样，您也可以向其他用户请求对收件箱项目的访问权限。

## 先决条件 {#pre-requisites}

登录用户必须是 `workflow-users` 组。 用户只能从对具有读取权限的用户或从启用了公共配置文件的用户共享项目或请求访问项目。

## 与其他用户共享收件箱中的单个或所有项目

AEM收件箱允许您与其他用户共享收件箱中的单个或所有项目。

### 共享所有收件箱项目

执行以下步骤，与其他用户共享收件箱中的所有项目：

1. 登录到您的AEM实例。 点按 ![收件箱](assets/bell.svg) 图标并点按 **[!UICONTROL 查看全部]**. 此时将显示收件箱项目的列表。
1. 点按 ![视图选择器](assets/viewlist.svg) 或 ![视图选择器](assets/calendar.svg) 图标 **[!UICONTROL 创建]** 按钮并点按 **[!UICONTROL 设置]**. 将显示“设置”对话框。
1. 打开 **[!UICONTROL 共享]** 选项卡。
1. 在中输入用户名 **[!UICONTROL 授予对收件箱项目的访问权限]** 文本框并点按 **[!UICONTROL 授权]**. 重复该步骤以添加更多用户。 所有有权访问您的项目的用户都会显示在 **用户名** 部分。
1. 点按&#x200B;**[!UICONTROL 保存]**。

>[!NOTE]
>
>(仅适用于以Forms为中心的工作流项目)启用 **[允许被分派人通过收件箱共享进行共享](aem-forms-workflow-step-reference.md)** 的选项 **分配任务** 步骤。 只有启用了上述选项的项目才会显示给其他用户。

### 共享单个项目

执行以下步骤以与其他用户共享收件箱项目：

1. 登录到您的AEM实例。 点按 ![收件箱](assets/bell.svg) 图标并点按 **[!UICONTROL 查看全部]**. 此时将显示收件箱项目的列表。
1. 选择项目并点按 **[!UICONTROL 共享]**. 将显示一个对话框。
1. 在添加要共享此项目的用户文本框中输入用户的名称，然后点按 **[!UICONTROL 添加]**. 重复该步骤以添加更多用户。 所有有权访问您的项目的用户都会显示在 **[!UICONTROL 用户名]** 部分。
1. 点按&#x200B;**[!UICONTROL 保存]**。


>[!NOTE]
>
>(仅适用于以Forms为中心的工作流项目)启用 **[允许被分派人在收件箱中明确共享](aem-forms-workflow-step-reference.md)** 的选项 **分配任务** 步骤。 只有启用了上述选项的项目才会显示给其他用户。

## 请求访问收件箱项目 {#request-access}

您可以请求对其他用户的收件箱项目的访问权限。 授予访问权限后，您可以查看、声明共享项目并对共享项目采取适当措施。 执行以下步骤，请求访问其他用户的收件箱项目：

1. 登录到您的AEM实例。 点按 ![视图选择器](assets/bell.svg) 图标并点按 **[!UICONTROL 查看全部]**.
1. 点按 ![视图选择器](assets/viewlist.svg) 或 ![视图选择器](assets/calendar.svg) 图标 **[!UICONTROL 创建]** 按钮并点按 **[!UICONTROL 设置]**. 将显示“设置”对话框。
1. 在中输入用户名 **[!UICONTROL 请求访问用户的收件箱项目]** 文本框并点按 **[!UICONTROL 请求]**. 请求将发送给用户，并根据用户名称显示请求状态。 重复该步骤以添加更多用户。
1. 点按&#x200B;**[!UICONTROL 保存]**。该请求将作为收件箱项目发送给用户。 用户可以选择项目并点按批准或拒绝，以授予或拒绝访问权限。


## 其他用户共享的声明项 {#claim-items}

只有在声明共享项目后，才能开始处理该项目。 它阻止多个用户处理单个项目。 执行以下步骤来声明项目：

1. 登录到您的AEM实例。 点按收件箱 ![收件箱](assets/bell.svg) 图标并点按 **[!UICONTROL 查看全部]**.
1. 点按 ![仅内容](assets/railleft.svg) 图标以打开过滤器选择器。
1. 点按 **[!UICONTROL 选择被分派人]** 下拉列表，以查看并选择已与您共享其收件箱项目的用户。
1. 选择项目并点按 **[!UICONTROL 声明]**. 该项目即添加到您的收件箱。

## 释放声明的项 {#release-items}

只有在声明共享项目后，才能对其进行处理。 其他用户看不到或无法处理您声明的项目。 如果无法继续处理某个项目，可以将其释放回池。   发放项目后，其他人可以申请并处理项目：

执行以下步骤以发放物料：

1. 登录到您的AEM实例。 点按收件箱 ![收件箱](assets/bell.svg) 图标并点按 **[!UICONTROL 查看全部]**. 此时将显示收件箱项目的列表。
1. 选择要释放的项目并点按 **[!UICONTROL 取消声明]**. 该项目将添加回池。 其他人现在可以申请此项目。

## 限制 {#limitations}

* 不支持与组共享项目。
* 不支持共享项目任务。
