---
title: Cloud Service 配置
seo-title: Cloud Service Configurations
description: 您可以扩展现有实例以创建您自己的配置
seo-description: You can extend the existing instances to create your own configurations
uuid: 9d20c3a4-2a12-4d3c-80c3-fcac3137a675
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: d25c03bf-6eaa-45f4-ab60-298865935a62
exl-id: 20a19ee5-7113-4aca-934a-a42c415a8d93
source-git-commit: 58594be73372e128ba999a8290615fbcb447084e
workflow-type: tm+mt
source-wordcount: '564'
ht-degree: 3%

---

# Cloud Service 配置{#cloud-service-configurations}

配置旨在提供存储服务配置的逻辑和结构。

您可以扩展现有实例以创建自己的配置。

## 概念 {#concepts}

开发配置时采用的原则基于以下概念：

* 服务/适配器用于检索配置。
* 配置（例如属性/段落）继承自父项。
* 按路径从Analytics节点引用。
* 易于扩展。
* 能够灵活地满足更复杂的配置需求，例如 [Adobe Analytics](/help/sites-administering/marketing-cloud.md#integrating-with-adobe-analytics).
* 支持依赖项(例如 [Adobe Analytics](/help/sites-administering/marketing-cloud.md#integrating-with-adobe-analytics) 插件需要 [Adobe Analytics](/help/sites-administering/marketing-cloud.md#integrating-with-adobe-analytics) 配置)。

## 结构 {#structure}

配置的基本路径为：

`/etc/cloudservices`。

将为每种类型的配置提供一个模板和一个组件。这使得在自定义后可以拥有可满足大多数需求的配置模板。

要为新服务提供配置，您需要：

* 在中创建服务包

   `/etc/cloudservices`

* 在此下：

   * 配置模板
   * 配置组件

模板和组件必须继承 `sling:resourceSuperType` 从基本模板中：

`cq/cloudserviceconfigs/templates/configpage`

或基础组件分别

`cq/cloudserviceconfigs/components/configpage`

服务提供商还应提供以下服务页：

`/etc/cloudservices/<service-name>`

### 模板 {#template}

您的模板将扩展基本模板：

`cq/cloudserviceconfigs/templates/configpage`

并定义 `resourceType` 指向自定义组件。

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

### 内容模型 {#content-model}

内容模型存储为 `cq:Page` 在：

`/etc/cloudservices/<service-name>(/*)`

```xml
/etc/cloudservices
/etc/cloudservices/service-name
/etc/cloudservices/service-name/config
/etc/cloudservices/service-name/config/inherited-config
```

配置存储在子节点下 `jcr:content`.

* 在对话框中定义的固定属性应存储在 `jcr:node` 直接。
* 动态元素(使用 `parsys` 或 `iparsys`)使用子节点存储组件数据。

```xml
/etc/cloudservices/service/config/jcr:content as nt:unstructured
propertyname
*
par/component/ as cq:Component
propertyname
*
```

### API {#api}

有关API的参考文档，请参阅 [com.day.cq.wcm.webservicesupport](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/webservicesupport/package-summary.html).

### AEM集成 {#aem-integration}

可用的服务列在 **Cloud Services** 的选项卡 **页面属性** 对话框（继承自的任何页面的） `foundation/components/page` 或 `wcm/mobile/components/page`)。

该选项卡还提供：

* 可启用服务的位置的链接
* 从路径字段中选择配置（服务的子节点）

#### 密码加密 {#password-encryption}

存储服务的用户凭据时，所有密码都应加密。

您可以通过添加隐藏表单字段来实现此目的。 此字段应具有注释 `@Encrypted` 在属性名称中；即 `password` 字段名称将写成：

`password@Encrypted`

然后，将自动对属性进行加密(使用 `CryptoSupport` service)，由 `EncryptionPostProcessor`.

>[!NOTE]
>
>这类似于标准 ` [SlingPostServlet](https://sling.apache.org/site/manipulating-content-the-slingpostservlet-servletspost.html)` 注释。

>[!NOTE]
>
>默认情况下， `EcryptionPostProcessor` 仅加密 `POST` 向发出的请求 `/etc/cloudservices`.

#### “服务”页jcr：content节点的其他属性 {#additional-properties-for-service-page-jcr-content-nodes}

<table>
 <tbody>
  <tr>
   <td><strong>属性</strong></td>
   <td><strong>描述</strong></td>
  </tr>
  <tr>
   <td>componentreference</td>
   <td>自动包含在页面中的组件的引用路径。<br /> 这用于其他功能和JS包含。<br /> 这包括页面上的组件，其中<br /> <code> cq/cloudserviceconfigs/components/servicecomponents</code><br /> 包含(通常早于 <code>body</code> 标记)。<br /> 对于Analytics和Target，我们使用它来包含其他功能，例如用于跟踪访客行为的JavaScript调用。</td>
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
   <td>在列表中使用的服务排名。</td>
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
   <td>服务URL标签。</td>
  </tr>
  <tr>
   <td>thumbnailPath</td>
   <td>服务的缩略图路径。</td>
  </tr>
  <tr>
   <td>可见</td>
   <td>在页面属性对话框中可见；默认情况下可见（可选）</td>
  </tr>
 </tbody>
</table>

### 用例 {#use-cases}

默认提供以下服务：

* [跟踪器代码片段](/help/sites-administering/external-providers.md) (Google、WebTrends等)
* [Adobe Analytics](/help/sites-administering/marketing-cloud.md#integrating-with-adobe-analytics)
* [Test&amp;Target](/help/sites-administering/marketing-cloud.md#integrating-with-adobe-target)

<!-- Search&Promote is end of life as of September 1, 2022 * [Search&Promote](/help/sites-administering/marketing-cloud.md#integrating-with-search-promote) -->
* [Dynamic Media](/help/sites-administering/marketing-cloud.md#integrating-with-scene)

>[!NOTE]
>
>另请参阅 [创建自定义Cloud Service](/help/sites-developing/extending-cloud-config-custom-cloud.md).
