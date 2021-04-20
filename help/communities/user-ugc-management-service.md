---
title: AEM Communities中的用户和UGC管理服务
seo-title: AEM Communities中的用户和UGC管理服务
description: 使用API批量删除和批量导出用户生成的内容，并禁用用户帐户。
seo-description: 使用API批量删除和批量导出用户生成的内容，并禁用用户帐户。
uuid: 91180659-617d-4f6c-9a07-e680770d0d8f
contentOwner: mgulati
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
discoiquuid: d305821d-1371-4e4a-8b28-8eee8fafa43b
docset: aem65
role: Administrator
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '617'
ht-degree: 0%

---


# AEM Communities中的用户和UGC管理服务{#user-and-ugc-management-service-in-aem-communities}

>[!IMPORTANT]
>
>以下各节将作为GDPR的示例，但涵盖的详细信息适用于所有数据保护和隐私法规；例如GDPR、CCPA等

AEM Communities提供现成的API，用于管理用户用户档案和批量管理用户生成的内容(UGC)。 启用后，**UserUgcManagement**&#x200B;服务允许特权用户（社区管理员和版主）禁用用户用户档案，并批量删除或批量导出特定用户的UGC。 这些API还使客户数据的控制者和处理者能够遵守欧洲合并的一般数据保护规定(GDPR)和其他受GDPR启发的隐私要求。

有关详细信息，请参阅Adobe隐私中心](https://www.adobe.com/privacy/general-data-protection-regulation.html)的[GDPR页。

>[!NOTE]
>
>如果您在AEM Communities](/help/communities/analytics.md)站点中配置了[Adobe Analytics，则捕获的用户数据将发送到Adobe Analytics服务器。 Adobe Analytics提供的API允许您访问、导出和删除用户数据并遵守GDPR。 有关详细信息，请参阅[提交访问和删除请求](https://docs.adobe.com/content/help/en/analytics/admin/data-governance/gdpr-submit-access-delete.html)。

要使用这些API，您需要通过激活UserUgcManagement服务来启用`/services/social/ugcmanagement`端点。 要激活此服务，请安装[GitHub.com](https://github.com/Adobe-Marketing-Cloud/aem-communities-ugc-migration/tree/main/bundles/communities-ugc-management-servlet)上提供的[示例servlet](https://github.com/Adobe-Marketing-Cloud/aem-communities-ugc-migration/tree/main/bundles/communities-ugc-management-servlet)。 然后，使用http请求，使用相应参数点击社区站点的发布实例上的端点，如下所示：

`https://localhost:port/services/social/ugcmanagement?user=<authorizable ID>&operation=<getUgc>`. 但是，您也可以构建UI（用户界面）来管理系统中的用户用户档案和用户生成的内容。

这些API支持执行以下功能。

## 检索用户{#retrieve-the-ugc-of-a-user}的UGC

**getUserUgc(ResourceResolver resourceResolver， String user， OutputStream outputStream)** 帮助从系统导出用户的所有UGC。

* **用户**:用户的可授权ID。
* **outputStream**:结果将作为输出流返回，该输出流是包含用户生成的内容（作为json文件）和附件（包括用户上传的图像或视频）的zip文件。

例如，要导出名为Weston McCall的用户的UGC(该用户使用weston.mccall@dodgit.com作为可授权的ID登录到社区站点)，可以发送类似于以下内容的httpGET请求：

`https://localhost:port/services/social/ugcmanagement?user=weston.mccall@dodgit.com&operation=getUgc`

## 删除用户{#delete-the-ugc-of-a-user}的UGC

**deleteUserUgc(ResourceResolver resourceResolver， String user)可** 帮助从系统中删除用户的所有UGC。

* **用户**:用户的可授权ID。

例如，要通过http-POST请求删除具有可授权ID weston.mccall@dodgit.com的用户的UGC，请使用以下参数：

* 用户 = `weston.mccall@dodgit.com`
* 操作 = `deleteUgc`

### 从Adobe Analytics {#delete-ugc-from-adobe-analytics}中删除UGC

要从Adobe Analytics中删除用户数据，请遵循[GDPR分析工作流程](https://docs.adobe.com/content/help/en/analytics/admin/data-governance/an-gdpr-workflow.html);因为API不会从Adobe Analytics中删除用户数据。

有关AEM Communities使用的Adobe Analytics变量映射，请参阅以下图像：

![AEM communities变量映射](assets/analytics-communities-mapping.png)

## 禁用用户帐户{#disable-a-user-account}

**deleteUserAccount(ResourceResolver resourceResolver， String user)帮** 助禁用用户帐户。

* **用户**:用户的可授权ID。

>[!NOTE]
>
>禁用用户将删除用户在服务器上拥有的所有用户生成的内容。

例如，要通过http-POST请求删除具有可授权ID `weston.mccall@dodgit.com`的用户的用户档案，请使用以下参数：

* 用户 = `weston.mccall@dodgit.com`
* 操作 = `deleteUser`

>[!NOTE]
>
>deleteUserAccount()API仅禁用系统中的用户用户档案并删除UGC。 但是，要从系统中删除用户用户档案，请导航到&#x200B;**CRXDE Lite**:[https://&lt;server>/crx/de](https://localhost:4502/crx/de)，找到用户节点并将其删除。
