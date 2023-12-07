---
title: 为草稿和提交配置存储服务
description: 了解如何为草稿和提交配置存储
topic-tags: publish
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 51ca2844-91f0-453a-9b39-b876399ebecb
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '531'
ht-degree: 0%

---

# 为草稿和提交配置存储服务 {#configuring-storage-services-for-drafts-and-submissions}

## 概述 {#overview}

借助AEM Forms，您可以存储：

* **草稿**：最终用户正在填写并保存以供稍后使用并随后提交的表单。

* **提交内容**：包含用户提供数据的已提交表单。

AEM Forms Portal数据和元数据服务为草稿和提交提供支持。 默认情况下，数据存储在发布实例中，然后反向复制到配置的创作实例以供过滤到其他发布实例。

现有的开箱即用方法关心的是将所有数据存储在发布实例上，包括可以是个人身份信息(PII)的数据。

除了上述默认方法之外，还有另一种实施方法可用于直接将表单数据推送到处理，而不是保存在本地。 担心在发布实例上存储潜在敏感数据的客户可以选择将数据发送到处理服务器的替代实施。 由于处理发生在创作实例上，因此它通常位于安全区域中。

>[!NOTE]
>
>当您使用Forms Portal提交操作或启用自适应表单中的在表单门户中存储数据选项时，表单数据存储在AEM存储库中。 在生产环境中，建议不要将草稿或已提交的表单数据存储在AEM存储库中。 相反，您必须将草稿和提交组件与企业数据库等安全存储集成以存储草稿和提交的表单数据。
>
>有关更多信息，请参阅 [将草稿和提交组件与数据库集成的示例](/help/forms/using/integrate-draft-submission-database.md).

## 配置Forms Portal草稿和提交服务 {#configuring-forms-portal-drafts-and-submissions-services}

在AEM Web控制台配置中( `https://[host]:'port'/system/console/configMgr`)，单击以打开 **Forms Portal草稿和提交配置** 在编辑模式下。

根据您的要求指定属性的值，如下所示：

### 开箱即用的服务，用于在发布实例上存储数据 {#out-of-the-box-services-to-store-data-on-publish-instance}

将数据反向复制到配置的创作实例。

<table>
 <tbody>
  <tr>
   <th>属性</th>
   <th>价值</th>
  </tr>
  <tr>
   <td>Forms Portal草稿数据服务(草稿数据服务(<strong>draft.data.service</strong>))</td>
   <td>com.adobe.fd.fp.service.impl.DraftDataServiceImpl<br /> </td>
  </tr>
  <tr>
   <td>Forms Portal元数据服务草稿(元数据服务草稿的标识符(<strong>draft.metadata.service</strong>))</td>
   <td>com.adobe.fd.fp.service.impl.DraftMetadataServiceImpl<br /> </td>
  </tr>
  <tr>
   <td>Forms Portal提交数据服务(用于提交数据服务的标识符(<strong>submit.data.service</strong>))</td>
   <td>com.adobe.fd.fp.service.impl.SubmitDataServiceImpl<br /> </td>
  </tr>
  <tr>
   <td>Forms Portal提交元数据服务(用于提交元数据服务的标识符(<strong>提交元数据服务</strong>))</td>
   <td>com.adobe.fd.fp.service.impl.SubmitMetadataServiceImpl<br /> </td>
  </tr>
 </tbody>
</table>

### 开箱即用的服务，用于在远程处理实例上存储数据 {#out-of-the-box-services-to-store-data-on-remote-processing-instance}

数据直接推送到配置的远程实例

<table>
 <tbody>
  <tr>
   <th>属性</th>
   <th>价值</th>
  </tr>
  <tr>
   <td>Forms Portal草稿数据服务(草稿数据服务(<strong>draft.data.service</strong>))</td>
   <td>com.adobe.fd.fp.service.impl.DraftDataServiceRemoteImpl<br /> </td>
  </tr>
  <tr>
   <td>Forms Portal元数据服务草稿(元数据服务草稿的标识符(<strong>draft.metadata.service</strong>))</td>
   <td>com.adobe.fd.fp.service.impl.DraftMetadataServiceRemoteImpl<br /> </td>
  </tr>
  <tr>
   <td>Forms Portal提交数据服务(用于提交数据服务的标识符(<strong>submit.data.service</strong>))</td>
   <td>com.adobe.fd.fp.service.impl.SubmitDataServiceRemoteImpl<br /> </td>
  </tr>
  <tr>
   <td>Forms Portal提交元数据服务(用于提交元数据服务的标识符(<strong>提交元数据服务</strong>))</td>
   <td>com.adobe.fd.fp.service.impl.SubmitMetadataServiceRemoteImpl<br /> </td>
  </tr>
 </tbody>
</table>

除了上面指定的配置之外，还提供有关已配置的远程处理实例的信息。

在AEM Web控制台配置中( `https://[host]:'port'/system/console/configMgr`)，单击以打开 **AEM DS设置服务** 在编辑模式下。 在AEM DS设置服务对话框中，提供有关处理服务器URL、处理服务器用户名和密码的信息。

>[!NOTE]
>
>还提供了一种用于在数据库中存储用户数据的示例实现。 要了解如何配置数据和元数据服务以将用户数据存储在外部数据库中，请参阅 [将草稿和提交组件与数据库集成的示例](/help/forms/using/integrate-draft-submission-database.md).
