---
title: AEM桌面应用程序(AEM Forms)
seo-title: AEM桌面应用程序(AEM Forms)
description: AEM桌面应用程序(AEM Forms)
uuid: 99e0f2fb-8623-45bb-8e2e-5c5d6f482366
contentOwner: khsingh
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: manage
discoiquuid: c30332b6-e012-442d-8e84-28832c116c7b
noindex: true
translation-type: tm+mt
source-git-commit: a873cf3e7efd3bc9cd4744bf09078d9040efcdda
workflow-type: tm+mt
source-wordcount: '425'
ht-degree: 0%

---


# AEM桌面应用程序(AEM Forms) {#aem-desktop-app-for-aem-forms}

AEM桌面应用程序允许您将Adobe Experience Manager(AEM)资产存储库和AEM Forms二进制文件映射到系统上的网络目录。 您可以在文件资源管理器中视图同步的资源和二进制文件，并根据需要使用各种应用程序编辑文件。 除了查看文件外，您还可以创建、上传和删除二进制文件。 您还可以直接从软件打开、编辑和保存文件。 例如，您可以直接从Designer打开和编辑XDP文件。 您对本地资产所做的更改会反映在AEM Assets存储库和AEM FormsUI中。

您可以从AEM实例下载应用程序。 有关下载应用程序的详细信息，请参 [阅AEM桌面应用程序发行说明](https://helpx.adobe.com/experience-manager/desktop-app/release-notes.html)。

## AEM Forms桌面应用程序支持的AEM资源 {#aem-forms-assets-supported-in-aem-desktop-app}

您可以使用该应用程序同步以下类型的AEM Forms二进制文件：表单模板(.xdp)、PDF表单(.pdf)、文档(.pdf)、图像、XML模式(.xsd)、样式表(.xfs)。 应用程序将所有其他文件（不支持的文件）列表为0字节文件。 将不支持的文件列为0字节文件可确保用户知道AEM Forms服务器上存在其他可用资源。

>[!NOTE]
>
>文件名只能包含字母数字字符、连字符或下划线。

## 启用AEM FormsAEM桌面应用程序 {#enable-aem-forms-for-aem-desktop-app}

AEM桌面应用程序在Microsoft Windows上使用WebDAV协议，在Mac OS X上使用SMB1连接到AEM Forms服务器。 开箱即用，AEM Forms服务器无法与WebDAV或SMB客户端同步二进制文件和其他资产。 执行以下步骤以启用AEM FormsAEM桌面应用程序：

1. 以管理员身份登录AEM Forms。
1. 在创作实例中，单击 ![adobeexperiencemanager](assets/adobeexperiencemanager.png) **[!UICONTROL >工具]** >锤 ![头](assets/hammer.png) >部 **[!UICONTROL 署]**>操作> Web ConsoleAdobe Experience Manager。 Web控制台将在新窗口中打开。
1. 在Web控制台窗口中，找到并打开 **[!UICONTROL FormsManager AddOn配置选项]** 。
1. 在FormsManager的AddOn配置对话框中，取消选中 **[!UICONTROL 异步同步资源]** 复选框，然后单 **[!UICONTROL 击保存]**。
1. 重新启动AEM Forms服务器。 重新启动后，AEM Forms服务器可接受内容并与AEM桌面应用程序共享内容。
1. 打开应用程序并连接到AEM Forms服务器。

   成功连接后，应用程序将填充 `content/dam` 和文 `content/dam/formsanddocuments` 件夹。 除了将文件从上方文件夹移动到本地文件夹，反之亦然，您还可以使用应用程序在自动填充的文件夹之间移动内容。

