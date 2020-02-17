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

---


# 使用内容属性导出内容{#using-content-properties-to-export-content}

>[!NOTE]
>
>Adobe建议对需要基于单页应用程序框架的客户端渲染（例如，React）的项目使用SPA编辑器。 [了解更多](/help/sites-developing/spa-overview.md).

应用程序在AEM中 *表示为cq* :Pages。

除了下面显示的表示集成支持属性的其他属性外，这些属性还共享在 ** 任何cq:Page中找到的相同公共属性。

## 应用程序属性 {#app-properties}

下表显示了应用 **程序属性和节点**。

<table>
 <tbody>
  <tr>
   <td><strong>PropertyName</strong></td>
   <td><strong>类型</strong></td>
   <td><strong>描述</strong></td>
  </tr>
  <tr>
   <td>dps-cloudConfig</td>
   <td>字符串：路径</td>
   <td><p>配置的Mobile On-Demand cloud服务的路径。 用于AEM mobile到Mobile点播操作（API调用）</p> <p>当作者选择将应用程序关联到的Mobile On-Demand cloud服务时，可通过管理连接拼贴配置此关联。</p> </td>
  </tr>
  <tr>
   <td>dps-exportTemplate</td>
   <td>字符串：路径</td>
   <td><p>应用程序的导出配置路径。 导出配置是一个包含2个子ContentSync导出配置模板的文件夹；</p> <p><i>dps-article</i>:用于导出文章内容的内容同步导出配置</p> <p><i>dps-HTMLResources</i>:内容用于导出应用程序／文章共享资源的同步导出配置</p> </td>
  </tr>
  <tr>
   <td>dps-projectId</td>
   <td>字符串</td>
   <td><p>此应用程序链接到／绑定到的移动点播项目的ID/URI。</p> <p>当作者从关联的Mobile On-Demand cloud服务的可用项目列表中选择项目时，可通过“管理连接”拼贴配置此关联。</p> </td>
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
   <td>从AEM上次上传共享资源到AEM mobile的日期。</td>
  </tr>
  <tr>
   <td>dps-sharedHTMLResources-lastUploadedBy</td>
   <td>字符串：userid</td>
   <td>执行从AEM到AEM mobile的共享资源请求的上次上传的用户ID。</td>
  </tr>
  <tr>
   <td>pge-dashboard-config</td>
   <td>字符串：路径</td>
   <td>功能板配置的路径。 该路径可以根据需要重定向到自定义功能板配置。</td>
  </tr>
  <tr>
   <td>sling:resourceType</td>
   <td>字符串：路径</td>
   <td><p>cq的路径：是或扩展 <i>mobileapps/core/components/instance的组件。</i></p> <p>这将提供应用程序目录中的状态和呈现。</p> </td>
  </tr>
 </tbody>
</table>

您可以使用 ***内容属性*** ，创建内容。 有关创建和导出文章和共享资源的信息，请参阅以下资源：

* [内容属性](/help/mobile/content-properties.md)
* [创建文章导出配置](/help/mobile/creating-article-export-configuration.md)
* [创建共享资源导出配置](/help/mobile/creating-shared-resources-export-configuration.md)
