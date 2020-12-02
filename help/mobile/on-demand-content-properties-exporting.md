---
title: 使用内容属性导出内容
seo-title: 使用内容属性导出内容
description: 下页显示了应用程序属性和节点。
seo-description: 下页显示了应用程序属性和节点。
uuid: 73f1832f-e457-47d0-a0e1-80af90897d31
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
discoiquuid: a3006835-b1d2-47d6-959a-cdb692e34e1e
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '344'
ht-degree: 4%

---


# 使用内容属性导出内容{#using-content-properties-to-export-content}

>[!NOTE]
>
>Adobe建议对需要基于单页应用程序框架的客户端渲染（例如，React）的项目使用SPA编辑器。 [了解更多](/help/sites-developing/spa-overview.md).

应用程序在AEM中表示为&#x200B;*cq:Pages*。

除了下面显示的表示集成支持属性的其他属性外，这些属性还共享任何&#x200B;*cq:Page*&#x200B;中的相同公共属性。

## 应用程序属性 {#app-properties}

下表显示了&#x200B;**App Properties和Nodes**。

<table>
 <tbody>
  <tr>
   <td><strong>属性名称</strong></td>
   <td><strong>类型</strong></td>
   <td><strong>描述</strong></td>
  </tr>
  <tr>
   <td>dps-cloudConfig</td>
   <td>字符串：路径</td>
   <td><p>指向已配置的移动点播Cloud Service的路径。 用于AEM Mobile到移动点播操作（API调用）</p> <p>当作者选择将应用程序关联到的Mobile On-DemandCloud Service时，可通过管理连接拼贴配置此关联。</p> </td>
  </tr>
  <tr>
   <td>dps-exportTemplate</td>
   <td>字符串：路径</td>
   <td><p>应用程序导出配置的路径。 导出配置是一个包含2个子ContentSync导出配置模板的文件夹；</p> <p><i>dps-article</i>:用于导出文章内容的ContentSync导出配置</p> <p><i>dps-HTMLResources</i>:用于导出应用程序／文章共享资源的内容同步导出配置</p> </td>
  </tr>
  <tr>
   <td>dps-projectId</td>
   <td>字符串</td>
   <td><p>此应用程序链接／绑定到的移动点播项目的ID/URI。</p> <p>当作者从可用项目列表中为关联的Mobile On-DemandCloud Service选择项目时，可通过管理连接拼贴配置此关联。</p> </td>
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
   <td>上次将共享资源从AEM上传到AEM Mobile的日期。</td>
  </tr>
  <tr>
   <td>dps-sharedHTMLResources-lastUploadedBy</td>
   <td>字符串：userid</td>
   <td>执行上次从AEM上传共享资源请求到AEM Mobile的用户的ID。</td>
  </tr>
  <tr>
   <td>pge-仪表板-config</td>
   <td>字符串：路径</td>
   <td>仪表板配置的路径。 可以根据需要将路径重定向到自定义仪表板配置。</td>
  </tr>
  <tr>
   <td>sling:resourceType</td>
   <td>字符串：路径</td>
   <td><p>cq的路径：是或扩展<i>mobileapps/core/components/instance的组件。</i></p> <p>它提供应用程序目录中的状态和呈现。</p> </td>
  </tr>
 </tbody>
</table>

可以使用&#x200B;***内容属性***&#x200B;创建内容。 请参阅以下创建和导出文章和共享资源的资源：

* [内容属性](/help/mobile/content-properties.md)
* [创建文章导出配置](/help/mobile/creating-article-export-configuration.md)
* [创建共享资源导出配置](/help/mobile/creating-shared-resources-export-configuration.md)
