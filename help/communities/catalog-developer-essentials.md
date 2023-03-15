---
title: 目录要点
seo-title: Catalog Essentials
description: 目录概述
seo-description: Catalog overview
uuid: 788512bb-fa38-48fb-a769-1eaae6bb95a1
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 542467ef-3793-4347-8424-c365c5a166f6
exl-id: 4ca76b50-d56d-4f4d-be92-bf8929c5d754
source-git-commit: 1d334c42088342954feb34f6179dc5b134f81bb8
workflow-type: tm+mt
source-wordcount: '358'
ht-degree: 2%

---

# 目录要点 {#catalog-essentials}

本页提供了有关使用启用社区站点的目录功能的基本信息。

当包含在社区站点中时，目录功能允许社区成员浏览和选择目录中列出的启用资源。

此 [ `enablement catalog` 组件](catalog.md) 允许社区成员访问目录 [启用资源](resources.md). 使用AEM标记是管理目录中启用资源外观的重要组成部分。

参见 [标记启用资源](tag-resources.md).

## 适用于客户端的Essentials {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/enablement/components/hbs/catalog</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>可包含</strong></a></td>
   <td>否</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md"><strong>clientllibs</strong></a></td>
   <td>cq.social.enablement.hbs.breadcrumbs<br /> cq.social.enablement.hbs.catalog<br /> cq.social.enablement.hbs.resource<br /> cq.social.enablement.hbs.learningpath</td>
  </tr>
  <tr>
   <td> <strong>模板</strong></td>
   <td> /libs/social/enablement/components/hbs/catalog/catalog.hbs<br /> </td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/enablement/components/hbs/catalog/clientlibs/catalog.css</td>
  </tr>
  <tr>
   <td><strong> 属性</strong></td>
   <td>参见 <a href="catalog.md">目录功能</a></td>
  </tr>
 </tbody>
</table>

## 服务器端Essentials {#essentials-for-server-side}

### 目录功能 {#catalog-function}

社区站点结构包括 [目录功能](functions.md#catalog-function)，包括已配置的 `enablement catalog` 组件。

### 预过滤器 {#pre-filters}

将“目录”功能添加到社区站点后，可以通过指定预过滤器来限制出现在目录中的启用资源和学习路径。 这是通过在站点的目录资源实例上设置属性来完成的。

以为例 [启用教程](getting-started-enablement.md)：

* 在作者上
* 使用 [CRXDE](../../help/sites-developing/developing-with-crxde-lite.md)

   * 例如 [https://&lt;server>：&lt;port>/crx/de](http://localhost:4502/crx/de)

* 导航到目录页上的目录资源

   * 例如，`/content/sites/enable/en/catalog/jcr:content/content/primary/catalog`

* 添加子过滤器节点

   * 选择 `catalog`节点
   * 选择 **[!UICONTROL 创建节点]**

      * 名称: `filters`
      * 类型: `nt:unstructured`
      * 选择 **[!UICONTROL 全部保存]**

* 添加 `se_resource-tags` 属性到 `filters` 节点

   * 选择 `filters` 节点
   * 添加多属性

      * 名称: `se_resource-tags`
      * 类型：字符串
      * 值： *&lt;enter a=&quot;&quot; span=&quot;&quot; id=&quot;1&quot; translate=&quot;no&quot; />标记ID](#pre-filter-tagids)>*[
         * 选择 **[!UICONTROL 多个]**
         * 选择 **[!UICONTROL 添加]**

            * 在弹出对话框中，选择 `+` 添加其他预筛选标记ID

* 重新发布社区站点

![configure-catalog](assets/configure-catalog.png)

#### 预筛选标记ID {#pre-filter-tagids}

预过滤器 [标记ID](../../help/sites-developing/framework.md#tagid) 必须与应用于启用资源的标记完全匹配。 这些组件在 `resources` 站点的文件夹，作为属性的值 `se_resource-tags`.

![configure-filters](assets/configure-catalog1.png)

### 参考API {#reference-apis}

* [启用API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/enablement/reporting/model/api/package-summary.html)

* [报表API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/reporting/dv/api/package-summary.html)

* [Reporting Analytics API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/reporting/dv/model/api/package-summary.html)
