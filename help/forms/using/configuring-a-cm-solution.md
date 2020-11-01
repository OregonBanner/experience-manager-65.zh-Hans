---
title: 配置通信管理解决方案
seo-title: 配置通信管理解决方案
description: 配置通信管理解决方案
uuid: 76b25004-fe47-44d7-9bed-7c0fd963306b
topic-tags: correspondence-management
content-type: reference
products: SG_EXPERIENCEMANAGER/6.3/FORMS
discoiquuid: 186ca75c-638b-4057-826e-cd5d56aa0397
translation-type: tm+mt
source-git-commit: a873cf3e7efd3bc9cd4744bf09078d9040efcdda
workflow-type: tm+mt
source-wordcount: '296'
ht-degree: 1%

---


# 配置通信管理解决方案 {#configuring-a-correspondence-management-solution}

## 为VersionRestoreManagerImpl定义作者实例URL {#defining-author-instance-url-for-versionrestoremanagerimpl}

使用以下步骤为创作实例版本还原定义作者实例URL:

1. 转 *至https://:&lt;PublishHost>:&lt;PublishPort>/lc/system/console/configMgr*。 使用OSGi Management Console用户凭据登录。 默认凭据为admin/admin。
1. 查找并单 **[!UICONTROL 击]** com.adobe. **[!UICONTROL livecycle.content.activate.impl.VersionRestoreManagerImpl.name设置旁的“编辑”图标]** 。
1. 在VersionRestoreManager **[!UICONTROL 作者URL字段]** ，指定VersionRestoreManager的作者实例的URL。

   **URL字符串**:

   `https://<hostname>:<port>:/libs/fd/fdm/content/crud/lc.content.remote.activate.VersionRestoreManager`

   >[!NOTE]
   >
   >如果负载平衡器前面有多个作者实例（群集），请在VersionRestoreManager作者URL字段中指定负载平衡 **[!UICONTROL 器的URL]** 。

1. 单击&#x200B;**[!UICONTROL 保存]**。

## 为ActivationManagerImpl定义发布实例URL(公共实例激活管理器) {#defining-the-publish-instance-url-for-activationmanagerimpl-public-instance-activation-manager}

按照以下步骤定义公共实例激活管理器的发布实例URL:

1. 转 *至https://:&lt;authorHost>:&lt;authorPort>/lc/system/console/configMgr*。 使用OSGi Management Console用户凭据登录。 默认凭据为admin/admin。
1. 查找并单 **[!UICONTROL 击]** com.adobe. **[!UICONTROL livecycle.content.activate.impl.ActivationManagerImpl.name设置旁的“编辑”图标]** 。
1. 在ActivationManager **[!UICONTROL 发布URL]** 字段中，指定用于访问发布实例ActivationManager的URL。 您可以提供以下URL。

   * **负载平衡器URL（推荐）**:提供负载平衡器URL，如果在发布场前有一台Web服务器充当负载平衡器（多个非群集发布实例）。
   * **发布实例URL**:提供任何发布实例URL。如果您有单个发布实例或位于发布场前方的Web服务器由于任何限制而无法从作者环境访问。 如果指定的发布实例关闭，则在作者端有一个要处理的回退机制。
   * **URL字符串**:

      `https://<hostname>:<port>:/libs/fd/fdm/content/crud/lc.content.remote.activate.activationManager`

1. 单击&#x200B;**[!UICONTROL 保存]**。

有关配置Corresponce Management的更多信息，请参 [阅Corresponce Management Configuration Properties](https://helpx.adobe.com/aem-forms/6-2/cm-configuration-properties.html)。
