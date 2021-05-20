---
title: 为草稿和提交配置存储服务
seo-title: 为草稿和提交配置存储服务
description: 了解如何为草稿和提交配置存储
seo-description: 了解如何为草稿和提交配置存储
uuid: 2f4efc07-312c-4908-8c91-84f4e6c5ad25
topic-tags: publish
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 6ebb6420-68b6-4abc-b298-c252db038416
exl-id: 51ca2844-91f0-453a-9b39-b876399ebecb
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '547'
ht-degree: 0%

---

# 为草稿和提交配置存储服务{#configuring-storage-services-for-drafts-and-submissions}

## 概述 {#overview}

通过AEM Forms，您可以存储：

* **草稿**:正在进行中的表单，最终用户可填写并保存以后，然后提交。

* **提交**:已提交的包含用户提供数据的表单。

AEM Forms门户数据和元数据服务支持草稿和提交。 默认情况下，数据存储在发布实例中，然后将该实例反向复制到已配置的创作实例，以便渗滤到其他发布实例。

现有现成方法的问题在于，它存储了发布实例上的所有数据，包括可以是个人身份信息(PII)的数据。

除了上述默认方法之外，还提供了替代实施，用于直接将表单数据推送到处理，而不是将其保存在本地。 担心在发布实例上存储潜在敏感数据的客户可以选择将数据发送到处理服务器的替代实施。 由于处理在创作实例上进行，因此它通常保留在安全区域。

>[!NOTE]
>
>当您使用Forms Portal提交操作或在自适应表单中启用“在表单门户中存储数据”选项时，表单数据会存储在AEM存储库中。 在生产环境中，建议不要将草稿或提交的表单数据存储在AEM存储库中。 您而是必须将草稿和提交组件与安全存储（如企业数据库）集成，以存储草稿和提交的表单数据。
>
>有关更多信息，请参阅[将草稿和提交组件与数据库](/help/forms/using/integrate-draft-submission-database.md)集成的示例。

## 配置Forms Portal草稿和提交服务{#configuring-forms-portal-drafts-and-submissions-services}

在AEM Web控制台配置(`https://[host]:'port'/system/console/configMgr`)中，单击以在编辑模式下打开&#x200B;**Forms Portal草稿和提交配置**。

根据您的要求指定属性的值，如下所述：

### 用于在发布实例{#out-of-the-box-services-to-store-data-on-publish-instance}上存储数据的开箱即用服务

数据会反向复制到配置的创作实例。

<table>
 <tbody>
  <tr>
   <th>属性</th>
   <th>值</th>
  </tr>
  <tr>
   <td>Forms门户草稿数据服务(草稿数据服务的标识符(<strong>draft.data.service</strong>))</td>
   <td>com.adobe.fd.fp.service.impl.DraftDataServiceImpl<br /> </td>
  </tr>
  <tr>
   <td>Forms门户草稿元数据服务(草稿元数据服务的标识符(<strong>draft.metadata.service</strong>))</td>
   <td>com.adobe.fd.fp.service.impl.DraftMetadataServiceImpl<br /> </td>
  </tr>
  <tr>
   <td>Forms Portal提交数据服务(提交数据服务的标识符(<strong>submit.data.service</strong>))</td>
   <td>com.adobe.fd.fp.service.impl.SubmitDataServiceImpl<br /> </td>
  </tr>
  <tr>
   <td>Forms Portal提交元数据服务(提交元数据服务的标识符(<strong>submit.metadata.service</strong>))</td>
   <td>com.adobe.fd.fp.service.impl.SubmitMetadataServiceImpl<br /> </td>
  </tr>
 </tbody>
</table>

### 用于在远程处理实例{#out-of-the-box-services-to-store-data-on-remote-processing-instance}上存储数据的开箱即用服务

数据会直接推送到配置的远程实例

<table>
 <tbody>
  <tr>
   <th>属性</th>
   <th>值</th>
  </tr>
  <tr>
   <td>Forms门户草稿数据服务(草稿数据服务的标识符(<strong>draft.data.service</strong>))</td>
   <td>com.adobe.fd.fp.service.impl.DraftDataServiceRemoteImpl<br /> </td>
  </tr>
  <tr>
   <td>Forms门户草稿元数据服务(草稿元数据服务的标识符(<strong>draft.metadata.service</strong>))</td>
   <td>com.adobe.fd.fp.service.impl.DraftMetadataServiceRemoteImpl<br /> </td>
  </tr>
  <tr>
   <td>Forms Portal提交数据服务(提交数据服务的标识符(<strong>submit.data.service</strong>))</td>
   <td>com.adobe.fd.fp.service.impl.SubmitDataServiceRemoteImpl<br /> </td>
  </tr>
  <tr>
   <td>Forms Portal提交元数据服务(提交元数据服务的标识符(<strong>submit.metadata.service</strong>))</td>
   <td>com.adobe.fd.fp.service.impl.SubmitMetadataServiceRemoteImpl<br /> </td>
  </tr>
 </tbody>
</table>

除了上述指定的配置之外，还提供有关已配置远程处理实例的信息。

在AEM Web控制台配置(`https://[host]:'port'/system/console/configMgr`)中，单击以在编辑模式下打开&#x200B;**AEM DS设置服务**。 在AEM DS设置服务对话框中，提供有关处理服务器URL、处理服务器用户名和密码的信息。

>[!NOTE]
>
>还提供用于在数据库中存储用户数据的示例实现。 要了解如何配置数据和元数据服务以在外部数据库中存储用户数据，请参阅[将草稿和提交组件与数据库集成的示例](/help/forms/using/integrate-draft-submission-database.md)。
