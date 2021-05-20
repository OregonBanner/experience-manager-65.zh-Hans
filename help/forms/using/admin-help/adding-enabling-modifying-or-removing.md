---
title: 添加、启用、修改或删除端点
seo-title: 添加、启用、修改或删除端点
description: 了解如何添加、启用、修改和删除端点。
seo-description: 了解如何添加、启用、修改和删除端点。
uuid: c53f225b-3d55-42f6-8982-0cd7dde0c4f5
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_endpoints
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 7d0d4f96-fc72-4e2b-a2cc-5741b0a30f74
exl-id: b7461d5c-95d1-4da2-9d2a-f54c410a87f9
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 0%

---

# 添加、启用、修改或删除端点{#adding-enabling-modifying-or-removing-endpoints}

## 向服务{#add-an-endpoint-to-a-service}添加端点

只能将端点添加到服务。 端点不能单独存在；必须与服务关联。

>[!NOTE]
>
>建议您在添加端点时使用唯一的名称。

1. 在管理控制台中，单击服务>应用程序和服务>服务管理。
1. 在“服务管理”页面上，单击要配置的服务。
1. 在“端点”选项卡的列表中，选择要添加的端点类型，然后单击“添加”。
1. 根据端点类型，配置其他端点设置。

[监视文件夹端点设置](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#watched-folder-endpoint-settings)

[电子邮件端点设置](/help/forms/using/admin-help/configuring-email-endpoints.md#email-endpoint-settings)

[配置任务管理器端点](/help/forms/using/admin-help/configuring-task-manager-endpoints.md#configuring-task-manager-endpoints)

[远程处理端点设置](/help/forms/using/admin-help/configuring-remoting-endpoints.md#remoting-endpoint-settings)

1. 单击添加。

## 启用或禁用终结点{#enable-or-disable-an-endpoint}

默认情况下，会自动启用新端点。 但是，如果您禁用了某个端点，则需要启用该端点才能使其正常运行。

如果您遇到服务问题，请禁用关联的端点以更好地解决问题。 您可能还希望在常规系统维护期间或升级服务时禁用端点。

1. 在管理控制台中，单击“服务”>“应用程序和服务”>“端点管理”。
1. 在“端点管理”页上，选中要启用或禁用的端点的复选框，然后单击启用或禁用。

## 修改端点{#modify-an-endpoint}

>[!NOTE]
>
>使用管理控制台对端点配置所做的更改不会反映在应用程序的设计时副本中。 如果您重新部署应用程序，则您使用管理控制台对其端点所做的任何更改都将丢失。

1. 在管理控制台中，单击“服务”>“应用程序和服务”>“端点管理”。
1. 在“端点管理”页面上，单击要修改的端点。
1. 在“更新端点”页面上，修改端点名称、说明和设置。

   >[!NOTE]
   >
   >名称或描述中不要包含&lt;字符，因为它将截断工作区中显示的名称或描述。

1. 要保存更改，请单击“更新”。

您还可以从“服务管理”页面执行此任务，方法是选择服务，然后单击“端点”选项卡。

## 删除端点{#remove-an-endpoint}

1. 在管理控制台中，单击“服务”>“应用程序和服务”>“端点管理”。
1. 在“端点管理”页上，选中要删除的端点的复选框，然后单击删除。 不再显示端点。
