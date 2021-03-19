---
title: 通信管理 |处理用户数据
seo-title: 通信管理 |处理用户数据
description: 通信管理 |处理用户数据
uuid: d5bb190b-d668-4da3-95da-b7705ad302d9
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 764d8e0d-604d-4c7b-89cd-7686ce5f03ff
role: 管理员
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '546'
ht-degree: 0%

---


# 通信管理 |处理用户数据{#correspondence-management-handling-user-data}

AEM Forms Correspondence Management使您能够创建、管理和简化安全且个性化的客户通信。 它为商业用户提供了直观的用户界面，使用预先批准的内容块和媒体元素创建通信。 有关创建通信的详细信息，请参阅[创建通信](/help/forms/using/create-correspondence.md)。

当业务用户或代理将通信另存为草稿或提交时，信件实例将保存在AEM存储库中。 字母实例包括对应数据和元数据。

>[!NOTE]
>
>在AEM 6.5 Forms中，无法开箱即用地管理通信。 如果您是从以前的AEM Forms版本升级，请安装兼容性包并迁移您的通信管理资源，以便继续在AEM 6.5 Forms中使用它们。 有关详细信息，请参阅[兼容性包](/help/forms/using/compatibility-package.md)。

## 用户数据和数据存储{#data}

仅当发布实例配置为管理信函实例时，通信管理才会在AEM存储库中存储草稿和已提交信函的数据。 有关配置的详细信息，请参阅[Corresponce Management配置属性](/help/forms/using/cm-configuration-properties.md)。

根据为您的AEM部署配置的数据存储持久性，草稿和提交的通信数据存储在以下位置。

<table>
 <tbody>
  <tr>
   <td><p><strong>持久性类型</strong></p> </td>
   <td><p><strong>数据存储</strong></p> </td>
   <td><p><strong>位置</strong></p> </td>
  </tr>
  <tr>
   <td><p>默认</p> </td>
   <td><p>在反向复制配置中指定的AEM发布实例和作者实例存储库</p> </td>
   <td><p><code>/content/apps/cm/letterInstances/[yyyy]/[mm]/[dd]/[node-id]/[letter-instance-name]/</code> </p> </td>
  </tr>
  <tr>
   <td><p>远程</p> </td>
   <td><p>AEM远程处理作者实例存储库</p> </td>
   <td><p><code>/content/apps/cm/letterInstances/[yyyy]/[mm]/[dd]/[node-id]/[letter-instance-name]/</code></p> </td>
  </tr>
 </tbody>
</table>

在上述指定的AEM存储库位置中：

* `[yyyy]/[mm]/[dd]` 是基于创建字母实例的日期的节点结构
* `[node-id]` 是指派给包含该字母的文件夹的ID
* `[letter-instance-name]` 是保存或提交信函时指定的名称

在[letter-instance-name]节点下，将创建以下节点结构，并将每个字母实例的数据存储在AEM存储库中：

| 节点 | 描述 |
|---|---|
| `extendedProperties` | 存储字母实例的元数据属性。 |
| `dataXML` | 以二进制格式存储包含对应数据的可下载数据XML文件。 |
| `processedXDP` | 包括用于创建已提交信函的XDP模板的详细信息。 此节点仅为提交的通信创建。 |
| `submittedLetter` | 以可下载的二进制格式存储提交的字母数据。 此节点仅为提交的通信创建。 |

## 访问和删除用户数据{#access-and-delete-user-data}

您可以访问已配置数据存储中的草稿和已提交的通信数据，如有必要，请删除它。

### 访问用户数据{#access-user-data}

通信管理提供了API，您可以使用它查找和访问草稿和提交的信件实例。 使用API，您可以使用字母实例ID或保存或提交通信的用户查找和打开字母实例。 有关详细信息，请参阅[访问字母实例](/help/forms/using/cm-apis-to-access-letter-instances.md)的API。

或者，您也可以使用CRX DELite导航到AEM存储库中的字母实例。 有关存储的数据和存储库位置的信息，请参见[用户数据和数据存储](/help/forms/using/correspondence-management-handling-user-data.md#data)。

### 删除用户数据{#delete-user-data}

要查找包含特定用户数据的字母实例，您可以：

* 如果信件实例名称或保存草稿或提交信件的用户已知，请使用通信管理API
* 使用AEM存储库搜索功能，使用个人可识别信息（如电子邮件ID或名称）查找存储信息的节点

要从AEM系统中完全删除草稿和提交的通信中的用户数据，您必须从所有适用的AEM实例中手动删除字母实例节点。
