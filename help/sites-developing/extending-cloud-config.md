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
translation-type: tm+mt
source-git-commit: 5128a08d4db21cda821de0698b0ac63ceed24379

---


# 云服务配置{#cloud-service-configurations}

配置被设计为提供用于存储服务配置的逻辑和结构。

您可以扩展现有实例以创建您自己的配置。

## 概念 {#concepts}

开发配置时使用的原则基于以下概念：

* 服务／适配器用于检索配置。
* 配置（例如属性／段落）从父项继承。
* 按路径从分析节点引用。
* 轻松扩展。
* 具有灵活性，可满足更复杂的配置，如 [Adobe Analytics](/help/sites-administering/marketing-cloud.md#integrating-with-adobe-analytics)。
* 支持依赖项(例如 [Adobe Analytics插件需要](/help/sites-administering/marketing-cloud.md#integrating-with-adobe-analytics) Adobe Analytics配置 [](/help/sites-administering/marketing-cloud.md#integrating-with-adobe-analytics) )。

## 结构 {#structure}

配置的基本路径是：

`/etc/cloudservices`.

对于每种配置类型，都会提供一个模板和一个组件。这样，配置模板就可以满足自定义后的大多数需求。

要为新服务提供配置，您需要：

* 创建服务页面

   `/etc/cloudservices`

* 下：

   * 配置模板
   * 配置组件

模板和组件必须从基本模 `sling:resourceSuperType` 板继承：

`cq/cloudserviceconfigs/templates/configpage`

或基组件

`cq/cloudserviceconfigs/components/configpage`

服务提供商还应提供服务页面：

`/etc/cloudservices/<service-name>`

### 模板 {#template}

您的模板将扩展基本模板：

`cq/cloudserviceconfigs/templates/configpage`

并定义指 `resourceType` 向自定义组件的组件。

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

在设置模板和组件后，您可以通过在以下位置添加子页面来添加配置：

`/etc/cloudservices/<service-name>`

### 内容模型 {#content-model}

内容模型存储为 `cq:Page` :

`/etc/cloudservices/<service-name>(/*)`

```xml
/etc/cloudservices
/etc/cloudservices/service-name
/etc/cloudservices/service-name/config
/etc/cloudservices/service-name/config/inherited-config
```

配置存储在子节点下 `jcr:content`。

* 在对话框中定义的固定属性应直接存储在 `jcr:node` 上。
* 动态元素(使 `parsys` 用或 `iparsys`)使用子节点存储组件数据。

```xml
/etc/cloudservices/service/config/jcr:content as nt:unstructured
propertyname
*
par/component/ as cq:Component
propertyname
*
```

### API {#api}

有关API的参考文档，请参 [阅com.day.cq.wcm.webservices支持](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/webservicesupport/package-summary.html)。

### AEM集成 {#aem-integration}

可用服务列在“页面 **属性”对话框******`foundation/components/page``wcm/mobile/components/page`（从或继承的任何页面）的“云服务”选项卡中。

该选项卡还提供：

* 指向可启用服务的位置的链接
* 从路径字段中选择配置（服务的子节点）

#### 密码加密 {#password-encryption}

存储服务的用户凭据时，应加密所有密码。

您可以通过添加隐藏的表单字段来实现这一点。 此字段的属性名 `@Encrypted` 称中应包含注释；例如，对于字 `password` 段，名称将写为：

`password@Encrypted`

然后，该属性将由自动加密(使用 `CryptoSupport` 服务) `EncryptionPostProcessor`。

>[!NOTE]
>
>这与标准注释类 ` [SlingPostServlet](https://sling.apache.org/site/manipulating-content-the-slingpostservlet-servletspost.html)` 似。

>[!NOTE]
>
>默认情况下， `EcryptionPostProcessor` 仅加密 `POST` 对的请求 `/etc/cloudservices`。

#### “服务”页的其他属性jcr:content Nodes {#additional-properties-for-service-page-jcr-content-nodes}

<table>
 <tbody>
  <tr>
   <td><strong>属性</strong></td>
   <td><strong>描述</strong></td>
  </tr>
  <tr>
   <td>componentReference</td>
   <td>要自动包含在页面中的组件的引用路径。<br /> 这用于附加功能和JS包含。<br /> 这包括包含页面上的组件<br /> ( <code> cq/cloudserviceconfigs/components/servicecomponents</code><br /> 通常在标记之前 <code>body</code> )。<br /> 对于Analytics和Target，我们使用它包含其他功能，如跟踪访客行为的JavaScript调用。</td>
  </tr>
  <tr>
   <td>描述</td>
   <td>服务的简短说明。<br /> </td>
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
   <td>用于在页面属性对话框中显示配置的筛选器。</td>
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
   <td>页面属性对话框中的可见性；默认情况下可见（可选）</td>
  </tr>
 </tbody>
</table>

### Use Cases {#use-cases}

这些服务默认提供：

* [跟踪器片段](/help/sites-administering/external-providers.md) （Google、WebTrends等）
* [Adobe Analytics](/help/sites-administering/marketing-cloud.md#integrating-with-adobe-analytics)
* [Test&amp;Target](/help/sites-administering/marketing-cloud.md#integrating-with-adobe-target)
* [Search&amp;Promote](/help/sites-administering/marketing-cloud.md#integrating-with-search-promote)
* [Scene7](/help/sites-administering/marketing-cloud.md#integrating-with-scene)

>[!NOTE]
>
>另请参阅 [创建自定义云服务](/help/sites-developing/extending-cloud-config-custom-cloud.md)。

