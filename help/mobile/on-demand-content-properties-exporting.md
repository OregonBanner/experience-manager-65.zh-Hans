---
title: 使用内容属性导出内容
seo-title: Using Content Properties to Export Content
description: 以下页面显示了应用程序属性和节点。
seo-description: The following page shows App Properties and Nodes.
uuid: 73f1832f-e457-47d0-a0e1-80af90897d31
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
discoiquuid: a3006835-b1d2-47d6-959a-cdb692e34e1e
exl-id: db1c33c9-8539-436d-b4d0-3d5e6fd688ed
source-git-commit: 259f257964829b65bb71b5a46583997581a91a4e
workflow-type: tm+mt
source-wordcount: '331'
ht-degree: 4%

---

# 使用内容属性导出内容{#using-content-properties-to-export-content}

>[!NOTE]
>
>对于需要基于单页应用程序框架的客户端渲染（例如React）的项目，Adobe建议使用SPA编辑器。 [了解详情](/help/sites-developing/spa-overview.md).

应用程序表示为 *cq：Pages* 在AEM中。

它们共享在任意 *cq：Page* 以及下面显示的其他表示支持资产的集成。

## 应用程序属性 {#app-properties}

下表显示 **应用程序属性和节点**.

<table>
 <tbody>
  <tr>
   <td><strong>属性名称</strong></td>
   <td><strong>类型</strong></td>
   <td><strong>描述</strong></td>
  </tr>
  <tr>
   <td>dps-cloudConfig</td>
   <td>String：Path</td>
   <td><p>指向配置的Mobile On-DemandCloud Service的路径。 用于AEM Mobile到Mobile On-Demand操作（API调用）</p> <p>当作者选择要将应用程序关联到的Mobile On-DemandCloud Service时，可以通过“管理连接”拼贴配置此关联。</p> </td>
  </tr>
  <tr>
   <td>dps-exportTemplate</td>
   <td>String：Path</td>
   <td><p>应用程序导出配置的路径。 导出配置是一个包含2个子ContentSync导出配置模板的文件夹；</p> <p><i>dps-article</i>： ContentSync导出配置以导出文章内容</p> <p><i>dps-HTMLResources</i>：ContentSync导出配置以导出应用程序/文章共享资源</p> </td>
  </tr>
  <tr>
   <td>dps-projectId</td>
   <td>字符串</td>
   <td><p>此应用程序链接/绑定到的Mobile On-Demand项目的ID/URI。</p> <p>当作者从关联的Mobile On-DemandCloud Service的可用项目列表中选择项目时，可通过“管理连接”拼贴配置此关联。</p> </td>
  </tr>
  <tr>
   <td>dps-projectTitle</td>
   <td>字符串</td>
   <td>应用程序标题。</td>
  </tr>
  <tr>
   <td>dps-resourceType</td>
   <td>字符串</td>
   <td>内容类型.</td>
  </tr>
  <tr>
   <td>dps-sharedHTMLResources-lastUploaded</td>
   <td>日期</td>
   <td>将共享资源从AEM上次上传到AEM Mobile的日期。</td>
  </tr>
  <tr>
   <td>dps-sharedHTMLResources-lastUploadedBy</td>
   <td>String：userid</td>
   <td>上次执行将共享资源请求从AEM上传到AEM Mobile的用户的ID。</td>
  </tr>
  <tr>
   <td>pge-dashboard-config</td>
   <td>String：Path</td>
   <td>仪表板配置的路径。 可以根据需要将该路径重定向到自定义仪表板配置。</td>
  </tr>
  <tr>
   <td>sling:resourceType</td>
   <td>String：Path</td>
   <td><p>作为或扩展的cq：Component的路径 <i>mobileapps/core/components/instance.</i></p> <p>这会提供应用程序目录中的显示和渲染。</p> </td>
  </tr>
 </tbody>
</table>

您可以使用 ***内容属性*** 以创建内容。 请参阅以下资源以创建和导出文章和共享资源：

* [内容属性](/help/mobile/content-properties.md)
* [创建文章导出配置](/help/mobile/creating-article-export-configuration.md)
* [创建共享资源导出配置](/help/mobile/creating-shared-resources-export-configuration.md)
