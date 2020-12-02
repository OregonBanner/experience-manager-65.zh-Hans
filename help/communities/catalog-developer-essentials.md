---
title: Catalog Essentials
seo-title: Catalog Essentials
description: 目录概述
seo-description: 目录概述
uuid: 788512bb-fa38-48fb-a769-1eaae6bb95a1
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 542467ef-3793-4347-8424-c365c5a166f6
translation-type: tm+mt
source-git-commit: 41de9fff615b5b2f77d835740dfb1d33aa81e59b
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 2%

---


# Catalog Essentials {#catalog-essentials}

本页提供使用Enablement Community站点的目录功能的基本信息。

当包含在社区站点中时，目录功能允许社区成员浏览并选择目录中列出的支持资源。

[ `enablement catalog`组件](catalog.md)允许社区成员访问[启用资源](resources.md)的目录。 使用AEM标记是管理目录中启用资源外观的重要部分。

请参阅[标记Enablement Resources](tag-resources.md)。

## 客户端{#essentials-for-client-side}的必备工具

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
   <td> <a href="clientlibs.md"><strong>clientlibs</strong></a></td>
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
   <td>请参阅<a href="catalog.md">目录功能</a></td>
  </tr>
 </tbody>
</table>

## 服务器端{#essentials-for-server-side}的必备工具

### 目录功能 {#catalog-function}

包含[目录函数](functions.md#catalog-function)的社区站点结构包括已配置的`enablement catalog`组件。

### 预过滤器{#pre-filters}

将目录功能添加到社区站点后，可以通过指定预过滤器来限制显示在目录中的启用资源和学习路径。 这是通过为站点设置目录资源实例的属性来完成的。

使用[Enablement Tutorial](getting-started-enablement.md)的示例：

* 论作者
* 使用[CRXDE](../../help/sites-developing/developing-with-crxde-lite.md)

   * 例如[https://&lt;server>:&lt;port>/crx/de](http://localhost:4502/crx/de)

* 导航到目录页上的目录资源

   * 例如，`/content/sites/enable/en/catalog/jcr:content/content/primary/catalog`

* 添加子过滤器节点

   * 选择`catalog`节点
   * 选择&#x200B;**[!UICONTROL 创建节点]**

      * 名称: `filters`
      * 类型: `nt:unstructured`
      * 选择&#x200B;**[!UICONTROL 保存全部]**

* 将`se_resource-tags`属性添加到`filters`节点

   * 选择`filters`节点
   * 添加多属性

      * 名称: `se_resource-tags`
      * 类型：字符串
      * 值：*&lt;输入[TagID](#pre-filter-tagids)>*
         * 选择&#x200B;**[!UICONTROL 多]**
         * 选择&#x200B;**[!UICONTROL 添加]**

            * 在弹出对话框中，选择`+`以添加其他预过滤器TagID

* 重新发布社区站点

![configure-catalog](assets/configure-catalog.png)

#### 预过滤标记ID {#pre-filter-tagids}

预过滤器[TagID](../../help/sites-developing/framework.md#tagid)必须与应用到启用资源的标记完全匹配。 这些属性在站点的`resources`文件夹中显示为属性`se_resource-tags`的值。

![配置过滤器](assets/configure-catalog1.png)

### 参考API {#reference-apis}

* [Enablement API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/enablement/client/api/package-summary.html)

* [报告API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/enablement/client/reporting/api/package-summary.html)

* [报告分析API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/enablement/client/reporting/analytics/api/package-summary.html)

