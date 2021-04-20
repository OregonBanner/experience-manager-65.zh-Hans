---
title: 配置AEM DS设置
seo-title: 配置AEM DS设置
description: 在提交表单之前，您需要指定处理服务器URL。
seo-description: 在提交表单之前，您需要指定处理服务器URL。
uuid: 55a6d434-7352-48a8-8387-8a5c1a48fafc
contentOwner: amgoyal
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
discoiquuid: a7387bd3-8b31-4bd0-a861-daa8f7cb2d05
docset: aem65
role: Administrator
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '259'
ht-degree: 0%

---


# 配置AEM DS设置{#configuring-aem-ds-settings}

本文介绍如何配置&#x200B;**AEM DS设置服务**。 此设置可用于多种情况，例如：

* 在通信管理中

   * 用于配置AEM Forms工作流
   * 使用表单门户远程保存草稿/提交时

* 在自适应表单中，当从发布实例提交自适应表单时

以下是配置&#x200B;**[!UICONTROL AEM DS设置]**&#x200B;的步骤：

1. 使用以下URL在发布实例上打开Configuration Manager:\
   *https://localhost:port/system/console/configMgr*。

   ![AEM Web控制台配置](assets/web_configuration_console_new.png)

1. 在&#x200B;**[!UICONTROL Adobe Experience Manager Web控制台配置]**&#x200B;窗口中，找到并单击&#x200B;**[!UICONTROL AEM DS设置]**&#x200B;选项。

   ![DS设置](assets/ds_settings_new.png)

1. **[!UICONTROL AEM DS设置服务]**&#x200B;窗口显示AEM DS组件的常用配置设置。

   ![DS设置服务](assets/ds_settings_service_new.png)

1. 在相应的字段中添加以下信息：

   **[!UICONTROL 处理服务器URL]**:处理服务器是需要触发Forms或AEM工作流的服务器。这可以与AEM作者实例的URL或其他服务器URL(即https://localhost:port/)相同。

   **[!UICONTROL 处理服务器用户名]**:工作流用户的用 [户名（基于使用的服务器URL）]

   **[!UICONTROL 处理服务器密码]**:工作流用户的口令

   >[!NOTE]
   >
   >
   >    
   >    
   >    * 在使用Forms或AEM工作流时，在从发布服务器提交任何内容之前，必须配置DS设置服务。 否则，提交表格将失败。


