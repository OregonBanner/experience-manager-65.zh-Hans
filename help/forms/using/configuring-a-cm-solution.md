---
title: 配置通信管理解决方案
seo-title: 配置通信管理解决方案
description: 'null'
seo-description: 'null'
uuid: 76b25004-fe47-44d7-9bed-7c0fd963306b
topic-tags: correspondence-management
content-type: reference
products: SG_EXPERIENCEMANAGER/6.3/FORMS
discoiquuid: 186ca75c-638b-4057-826e-cd5d56aa0397
translation-type: tm+mt
source-git-commit: 5120bbdefea528ad6d07a9c99df565555b6a8444

---


# 配置通信管理解决方案 {#configuring-a-correspondence-management-solution}

## 为VersionRestoreManagerImpl定义作者实例URL {#defining-author-instance-url-for-versionrestoremanagerimpl}

使用以下步骤为创作实例版本恢复定义创作实例URL:

1. 转到 *https://:&lt;PublishHost>:&lt;PublishPort>/lc/system/console/configMgr*。 使用OSGi Management Console用户凭据登录。 默认凭据为admin/admin。
1. 查找并单 **[!UICONTROL 击]** com.adobe.livecycle.content.activate.impl.VersionRestoreManagerImpl.name设置旁边的“编辑”图标 **** 。
1. 在VersionRestoreManager的 **[!UICONTROL 作者URL字段中]** ，指定VersionRestoreManager的作者实例的URL。

   **URL字符串**:

   `https://<hostname>:<port>:/libs/fd/fdm/content/crud/lc.content.remote.activate.VersionRestoreManager`

   >[!NOTE]
   >
   >如果负载平衡器前面有多个作者实例（群集），请在 **[!UICONTROL VersionRestoreManager作者URL字段中指定负载平衡器的URL]** 。

1. 单击&#x200B;**[!UICONTROL 保存]**。

## 为ActivationManager定义发布实例URL实施（公共实例激活管理器） {#defining-the-publish-instance-url-for-activationmanagerimpl-public-instance-activation-manager}

按照以下步骤为公共实例激活管理器定义发布实例URL:

1. 转到 *https://:&lt;authorHost>:&lt;authorPort>/lc/system/console/configMgr*。 使用OSGi Management Console用户凭据登录。 默认凭据为admin/admin。
1. 查找并单 **[!UICONTROL 击]** com.adobe.livecycle.content.activate.impl.ActivationManagerImpl.name设置旁的“编辑”图标 **** 。
1. 在ActivationManager的 **[!UICONTROL 发布URL字段中]** ，指定用于访问发布实例ActivationManager的URL。 您可以提供以下URL。

   * **负载平衡器URL（建议）**:提供负载平衡器URL，如果在发布群（多个非群集发布实例）前有Web服务器充当负载平衡器。
   * **发布实例URL**:提供任何发布实例URL，如果您有单个发布实例或位于发布农场前端的Web服务器由于任何限制而无法从创作环境访问。 如果指定的发布实例关闭，则在作者端有一个要处理的回退机制。
   * **URL字符串**:

      `https://<hostname>:<port>:/libs/fd/fdm/content/crud/lc.content.remote.activate.activationManager`

1. 单击&#x200B;**[!UICONTROL 保存]**。

有关配置Correponse Management的详细信息，请参阅 [Correponsement Management Configuration Properties](https://helpx.adobe.com/aem-forms/6-2/cm-configuration-properties.html)。
