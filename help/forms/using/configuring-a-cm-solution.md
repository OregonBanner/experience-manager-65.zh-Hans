---
title: 配置通信管理解决方案
description: 了解如何在AEM Forms环境中配置通信管理解决方案。
topic-tags: correspondence-management
content-type: reference
products: SG_EXPERIENCEMANAGER/6.3/FORMS
feature: Correspondence Management
exl-id: f7f5eb0d-a283-45ea-84d3-d6375d2bb95b
source-git-commit: 000c22028259eb05a61625d43526a2e8314a1d60
workflow-type: tm+mt
source-wordcount: '301'
ht-degree: 1%

---

# 配置通信管理解决方案 {#configuring-a-correspondence-management-solution}

## 为VersionRestoreManagerImpl定义创作实例URL {#defining-author-instance-url-for-versionrestoremanagerimpl}

使用以下步骤可为创作实例版本还原定义创作实例URL：

1. 转到 *https://网站：&lt;publishhost>：&lt;publishport>/lc/system/console/configMgr*. 使用OSGi Management Console用户凭据登录。 默认凭据为admin/admin。
1. 查找并单击 **[!UICONTROL 编辑]** 图标(位于 **[!UICONTROL com.adobe.livecycle.content.activate.impl.VersionRestoreManagerImpl.name]** 设置。
1. 在 **[!UICONTROL VersionRestoreManager作者URL]** 字段，指定VersionRestoreManager的创作实例的URL。

   **URL字符串**：

   `https://<hostname>:<port>:/libs/fd/fdm/content/crud/lc.content.remote.activate.VersionRestoreManager`

   >[!NOTE]
   >
   >如果有多个作者实例（聚类）由负载平衡器前导，请在中指定指向负载平衡器的URL **[!UICONTROL VersionRestoreManager作者URL]** 字段。

1. 单击&#x200B;**[!UICONTROL 保存]**。

## 定义ActivationManagerImpl（公共实例激活管理器）的发布实例URL {#defining-the-publish-instance-url-for-activationmanagerimpl-public-instance-activation-manager}

请按照以下步骤操作，以便您能够为公共实例激活管理器定义发布实例URL：

1. 转到 *https://网站：&lt;authorhost>：&lt;authorport>/lc/system/console/configMgr*. 使用OSGi Management Console用户凭据登录。 默认凭据为admin/admin。
1. 查找并单击 **[!UICONTROL 编辑]** 图标(位于 **[!UICONTROL com.adobe.livecycle.content.activate.impl.ActivationManagerImpl.name]** 设置。
1. 在 **[!UICONTROL ActivationManager发布URL]** 字段，指定用于访问发布实例ActivationManager的URL。 您可以提供以下URL。

   * **负载平衡器URL（推荐）**：如果将Web服务器用作发布场前面的负载平衡器（多个非集群发布实例），则提供负载平衡器URL。
   * **发布实例URL**：提供任意发布实例URL，如果您有一个发布实例，或者由于任何限制而无法从创作环境访问作为发布场前端的Web服务器。 如果指定的发布实例出现故障，创作端会有一个回退机制来处理。
   * **URL字符串**：

     `https://<hostname>:<port>:/libs/fd/fdm/content/crud/lc.content.remote.activate.activationManager`

1. 单击&#x200B;**[!UICONTROL 保存]**。

有关配置通信管理的详细信息，请参阅 [通信管理配置属性](https://helpx.adobe.com/aem-forms/6-2/cm-configuration-properties.html).
