---
title: 配置通信管理解决方案
seo-title: Configuring a Correspondence Management solution
description: 配置通信管理解决方案
uuid: 76b25004-fe47-44d7-9bed-7c0fd963306b
topic-tags: correspondence-management
content-type: reference
products: SG_EXPERIENCEMANAGER/6.3/FORMS
discoiquuid: 186ca75c-638b-4057-826e-cd5d56aa0397
feature: Correspondence Management
exl-id: f7f5eb0d-a283-45ea-84d3-d6375d2bb95b
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '291'
ht-degree: 1%

---

# 配置通信管理解决方案 {#configuring-a-correspondence-management-solution}

## 为VersionRestoreManagerImpl定义创作实例URL {#defining-author-instance-url-for-versionrestoremanagerimpl}

使用以下步骤为创作实例版本还原定义创作实例URL:

1. 转到 *https://网站：&lt;publishhost>:&lt;publishport>/lc/system/console/configMgr*. 使用OSGi管理控制台用户凭据登录。 默认凭据为管理员/管理员。
1. 查找并单击 **[!UICONTROL 编辑]** 图标 **[!UICONTROL com.adobe.livecycle.content.activate.impl.VersionRestoreManagerImpl.name]** 设置。
1. 在 **[!UICONTROL VersionRestoreManager创作URL]** 字段中，指定VersionRestoreManager的创作实例的URL。

   **URL字符串**:

   `https://<hostname>:<port>:/libs/fd/fdm/content/crud/lc.content.remote.activate.VersionRestoreManager`

   >[!NOTE]
   >
   >如果负载平衡器前面有多个创作实例（群集），请在 **[!UICONTROL VersionRestoreManager创作URL]** 字段。

1. 单击“**[!UICONTROL 保存]**”。

## 为ActivationManagerImpl（公共实例激活管理器）定义发布实例URL {#defining-the-publish-instance-url-for-activationmanagerimpl-public-instance-activation-manager}

按照以下步骤为公共实例激活管理器定义发布实例URL:

1. 转到 *https://网站：&lt;authorhost>:&lt;authorport>/lc/system/console/configMgr*. 使用OSGi管理控制台用户凭据登录。 默认凭据为管理员/管理员。
1. 查找并单击 **[!UICONTROL 编辑]** 图标 **[!UICONTROL com.adobe.livecycle.content.activate.impl.ActivationManagerImpl.name]** 设置。
1. 在 **[!UICONTROL ActivationManager发布URL]** 字段中，指定用于访问Publish实例激活管理器的URL。 您可以提供以下URL。

   * **负载平衡器URL（推荐）**:提供负载平衡器URL。如果您在发布场（多个非群集发布实例）之前有一个Web服务器充当负载平衡器。
   * **发布实例URL**:提供任何发布实例URL。如果您有单个发布实例，或者发布场的Web服务器由于任何限制而无法从创作环境访问。 如果指定的发布实例关闭，则在创作端有一个要处理的回退机制。
   * **URL字符串**:

      `https://<hostname>:<port>:/libs/fd/fdm/content/crud/lc.content.remote.activate.activationManager`

1. 单击“**[!UICONTROL 保存]**”。

有关配置通信管理的更多信息，请参阅 [通信管理配置属性](https://helpx.adobe.com/aem-forms/6-2/cm-configuration-properties.html).
