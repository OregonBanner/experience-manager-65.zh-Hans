---
title: 云服务配置
seo-title: 云服务配置
description: 您可以扩展现有实例以创建您自己的配置
seo-description: 您可以扩展现有实例以创建您自己的配置
uuid: 9d20c3a4-2a12-4d3c-80c3-fcac3137a675
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: d25c03bf-6eaa-45f4-ab60-298865935a62
exl-id: 20a19ee5-7113-4aca-934a-a42c415a8d93
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '580'
ht-degree: 3%

---

# 云服务配置{#cloud-service-configurations}

配置旨在提供用于存储服务配置的逻辑和结构。

您可以扩展现有实例以创建您自己的配置。

## 概念  {#concepts}

在开发配置时使用的原则基于以下概念：

* 服务/适配器用于检索配置。
* 配置（如属性/段落）从父级继承。
* 按路径从分析节点引用。
* 易于扩展。
* 灵活地满足更复杂的配置需求，例如[Adobe Analytics](/help/sites-administering/marketing-cloud.md#integrating-with-adobe-analytics)。
* 支持依赖项(例如[Adobe Analytics](/help/sites-administering/marketing-cloud.md#integrating-with-adobe-analytics)插件需要[Adobe Analytics](/help/sites-administering/marketing-cloud.md#integrating-with-adobe-analytics)配置)。

## 结构 {#structure}

配置的基本路径是：

`/etc/cloudservices`。

对于每种类型的配置，都将提供一个模板和一个组件。这样，配置模板就可以在自定义后满足大多数需求。

要为新服务提供配置，您需要：

* 创建服务页

   `/etc/cloudservices`

* 下：

   * 配置模板
   * 配置组件

模板和组件必须从基本模板继承`sling:resourceSuperType`:

`cq/cloudserviceconfigs/templates/configpage`

或基元

`cq/cloudserviceconfigs/components/configpage`

服务提供商还应提供服务页面：

`/etc/cloudservices/<service-name>`

### 模板 {#template}

您的模板将扩展基本模板：

`cq/cloudserviceconfigs/templates/configpage`

并定义指向自定义组件的`resourceType`。

```xml
/libs/cq/analytics/templates/sitecatalyst
sling:resourceSuperType = cq/cloudserviceconfigs/templates/configpage
allowedChildren = /libs/cq/analytics/templates/sitecatalyst
allowedPaths = /etc/cloudservices/analytics/*, /etc/cloudservices/analytics/.*
componentReference = cq/analytics/components/sitecatalyst
jcr:content/
cq:designPath = /etc/designs/cloudservices
sling:resourceType = cq/analytics/components/sitecatalystpage

/libs/cq/analytics/templates/generictracker
sling:resourceSuperType = cq/cloudservices/templates/configpage
allowedChildren = /libs/cq/analytics/templates/generictracker
allowedPaths = /etc/cloudservices/analytics/*, /etc/cloudservices/analytics/.*
jcr:content/
cq:designPath = /etc/designs/cloudservices
sling:resourceType = cq/analytics/components/generictrackerpage
```

### 组件 {#components}

您的组件应扩展基本组件：

`cq/cloudserviceconfigs/templates/configpage`

```xml
/libs/cq/analytics/components/sitecatalystpage

/libs/cq/analytics/components/generictrackerpage
```

设置模板和组件后，您可以通过在下添加子页面来添加配置：

`/etc/cloudservices/<service-name>`

### 内容模型{#content-model}

内容模型将存储为`cq:Page`，位于：

`/etc/cloudservices/<service-name>(/*)`

```xml
/etc/cloudservices
/etc/cloudservices/service-name
/etc/cloudservices/service-name/config
/etc/cloudservices/service-name/config/inherited-config
```

配置存储在子节点`jcr:content`下。

* 修复了对话框中定义的属性应直接存储在`jcr:node`上。
* 动态元素（使用`parsys`或`iparsys`）使用子节点存储组件数据。

```xml
/etc/cloudservices/service/config/jcr:content as nt:unstructured
propertyname
*
par/component/ as cq:Component
propertyname
*
```

### API {#api}

有关API的参考文档，请参阅[com.day.cq.wcm.webservicesupport](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/webservicesupport/package-summary.html)。

### AEM集成{#aem-integration}

**页面属性**&#x200B;对话框的&#x200B;**Cloud Services**&#x200B;选项卡（任何从`foundation/components/page`或`wcm/mobile/components/page`继承的页面）中列出了可用服务。

选项卡还提供：

* 可在其中启用服务的位置的链接
* 从路径字段中选择配置（服务的子节点）

#### 密码加密{#password-encryption}

存储服务的用户凭据时，应加密所有密码。

您可以通过添加隐藏的表单字段来实现此目的。 该字段的属性名称中应包含注释`@Encrypted`;例如，对于`password`字段，名称将写为：

`password@Encrypted`

然后，该属性将由`EncryptionPostProcessor`自动加密（使用`CryptoSupport`服务）。

>[!NOTE]
>
>这类似于标准` [SlingPostServlet](https://sling.apache.org/site/manipulating-content-the-slingpostservlet-servletspost.html)`注释。

>[!NOTE]
>
>默认情况下，`EcryptionPostProcessor`仅加密对`/etc/cloudservices`发出的`POST`请求。

#### 服务页jcr:content节点{#additional-properties-for-service-page-jcr-content-nodes}的其他属性

<table>
 <tbody>
  <tr>
   <td><strong>属性</strong></td>
   <td><strong>描述</strong></td>
  </tr>
  <tr>
   <td>componentReference</td>
   <td>要自动包含在页面中的组件的引用路径。<br /> 此插件可用于其他功能和JS包含项。<br /> 这包括包含的页面上的组<br /> <code> cq/cloudserviceconfigs/components/servicecomponents</code><br /> 件(通常在标记之 <code>body</code> 前)。<br /> 对于Analytics和Target，我们使用此功能包含其他功能，例如用于跟踪访客行为的JavaScript调用。</td>
  </tr>
  <tr>
   <td>描述</td>
   <td>服务的简短描述。<br /> </td>
  </tr>
  <tr>
   <td>descriptionExtended</td>
   <td>服务的扩展描述。</td>
  </tr>
  <tr>
   <td>排名</td>
   <td>用于列表的服务排名。</td>
  </tr>
  <tr>
   <td>selectableChildren</td>
   <td>在“页面属性”对话框中显示配置的过滤器。</td>
  </tr>
  <tr>
   <td>serviceUrl</td>
   <td>服务网站的URL。</td>
  </tr>
  <tr>
   <td>serviceUrlLabel</td>
   <td>服务URL的标签。</td>
  </tr>
  <tr>
   <td>thumbnailPath</td>
   <td>服务的缩略图路径。</td>
  </tr>
  <tr>
   <td>可见</td>
   <td>页面属性对话框的可见性；默认可见（可选）</td>
  </tr>
 </tbody>
</table>

### 用例{#use-cases}

默认提供以下服务：

* [跟踪器片段](/help/sites-administering/external-providers.md) （Google、WebTrends等）
* [Adobe Analytics](/help/sites-administering/marketing-cloud.md#integrating-with-adobe-analytics)
* [Test&amp;Target](/help/sites-administering/marketing-cloud.md#integrating-with-adobe-target)
* [Search&amp;Promote](/help/sites-administering/marketing-cloud.md#integrating-with-search-promote)
* [Dynamic Media](/help/sites-administering/marketing-cloud.md#integrating-with-scene)

>[!NOTE]
>
>另请参阅[创建自定义Cloud Service](/help/sites-developing/extending-cloud-config-custom-cloud.md)。
