---
title: 配置通信管理解决方案
seo-title: 配置通信管理解决方案
description: 配置通信管理解决方案
uuid: 76b25004-fe47-44d7-9bed-7c0fd963306b
topic-tags: correspondence-management
content-type: reference
products: SG_EXPERIENCEMANAGER/6.3/FORMS
discoiquuid: 186ca75c-638b-4057-826e-cd5d56aa0397
feature: 通信管理
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '298'
ht-degree: 2%

---


# 配置Corresponce Management解决方案{#configuring-a-correspondence-management-solution}

## 定义VersionRestoreManagerImpl {#defining-author-instance-url-for-versionrestoremanagerimpl}的作者实例URL

使用以下步骤为创作实例版本还原定义创作实例URL:

1. 转至&#x200B;*https://:&lt;PublishHost>:&lt;PublishPort>/lc/system/console/configMgr*。 使用OSGi Management Console用户凭据登录。 默认凭据为admin/admin。
1. 查找并单击&#x200B;**[!UICONTROL com.adobe.livecycle.content.activate.impl.VersionRestoreManagerImpl.name]**&#x200B;设置旁的&#x200B;**[!UICONTROL 编辑]**&#x200B;图标。
1. 在&#x200B;**[!UICONTROL VersionRestoreManager作者URL]**&#x200B;字段中，指定VersionRestoreManager的作者实例的URL。

   **URL字符串**:

   `https://<hostname>:<port>:/libs/fd/fdm/content/crud/lc.content.remote.activate.VersionRestoreManager`

   >[!NOTE]
   >
   >如果有多个作者实例（群集）由负载平衡器前端，请在&#x200B;**[!UICONTROL VersionRestoreManager作者URL]**&#x200B;字段中指定指向负载平衡器的URL。

1. 单击&#x200B;**[!UICONTROL 保存]**。

## 定义ActivationManager的发布实例URLImpl(公共实例激活管理器){#defining-the-publish-instance-url-for-activationmanagerimpl-public-instance-activation-manager}

按照以下步骤定义公共实例激活管理器的发布实例URL:

1. 转至&#x200B;*https://:&lt;authorHost>:&lt;authorPort>/lc/system/console/configMgr*。 使用OSGi Management Console用户凭据登录。 默认凭据为admin/admin。
1. 查找并单击&#x200B;**[!UICONTROL com.adobe.livecycle.content.activate.impl.ActivationManagerImpl.name]**&#x200B;设置旁的&#x200B;**[!UICONTROL 编辑]**&#x200B;图标。
1. 在&#x200B;**[!UICONTROL ActivationManager发布URL]**&#x200B;字段中，指定用于访问发布实例ActivationManager的URL。 您可以提供以下URL。

   * **负载平衡器URL（推荐）**:提供负载平衡器URL，如果在发布场（多个非群集发布实例）之前有一台Web服务器充当负载平衡器。
   * **发布实例URL**:提供任何发布实例URL。如果您有单个发布实例，或者位于发布场前方的Web服务器由于任何限制而无法从作者环境访问。如果指定的发布实例关闭，则在作者端有一个要处理的回退机制。
   * **URL字符串**:

      `https://<hostname>:<port>:/libs/fd/fdm/content/crud/lc.content.remote.activate.activationManager`

1. 单击&#x200B;**[!UICONTROL 保存]**。

有关配置Corresponce Management的详细信息，请参阅[Corresponce Management Configuration Properties](https://helpx.adobe.com/aem-forms/6-2/cm-configuration-properties.html)。
