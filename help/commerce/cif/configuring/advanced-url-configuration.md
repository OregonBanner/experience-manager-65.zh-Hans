---
title: 高级URL配置
description: 了解如何自定义产品和类别页面的URL。 这允许实施优化搜索引擎的URL并促进发现。
sub-product: 商务
doc-type: technical-video
activity: setup
audience: administrator
feature: 商务集成框架
kt: 4933
thumbnail: 34350.jpg
source-git-commit: da538dac17b4c6182b44801b4c79d6cdbf35f640
workflow-type: tm+mt
source-wordcount: '791'
ht-degree: 3%

---

# 高级URL配置 {#url}

[AEM CIF核心组](https://github.com/adobe/aem-core-cif-components) 件提供了高级配置，用于自定义产品和类别页面的URL。许多实施都将自定义这些URL以用于搜索引擎优化(SEO)。 以下视频详细介绍了如何配置`UrlProvider`服务和[Sling映射](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html)的功能，以自定义产品和类别页面的URL。

>[!VIDEO](https://video.tv.adobe.com/v/34350/?quality=12)

## 配置 {#configuration}

要根据SEO要求和需要配置`UrlProvider`服务，项目必须为“CIF URL提供程序配置”配置提供OSGI配置，并按照以下所述配置服务。

>[!NOTE]
>
> 请参见下文的[Venia Reference store](https://github.com/adobe/aem-cif-guides-venia)项目包含用于演示产品和类别页面自定义URL使用情况的示例配置。

### 产品页面URL模板 {#product}

这会使用以下属性配置产品页面的URL:

* **产品URL模板**:通过一组占位符定义URL的格式。默认值为`{{page}}.{{url_key}}.html#{{variant_sku}}`，最终生成URL，例如`/content/venia/us/en/products/product-page.chaz-kangeroo-hoodie.html#MH01-M-Orange`，其中
   * `{{page}}` 替换为  `/content/venia/us/en/products/product-page`
   * `{{url_key}}` 已被Magento的 `url_key` 产品属性替换，此处  `chaz-kangeroo-hoodie`
   * `{{variant_sku}}` 已被替换为当前选定的变体，此处  `MH01-M-Orange`
* **产品标识符位置**:定义用于获取产品数据的标识符的位置。默认值为`SELECTOR`，另一个可能值为`SUFFIX`。 对于上一个示例URL，这表示将使用标识符`chaz-kangeroo-hoodie`获取产品数据。
* **产品标识符类型**:定义获取产品数据时要使用的标识符类型。默认值为`URL_KEY`，另一个可能值为`SKU`。 对于上一个示例URL，这意味着将使用MagentoGraphQL过滤器（如`filter:{url_key:{eq:"chaz-kangeroo-hoodie"}}`）获取产品数据。

### 产品列表页面URL模板{#product-list}

这会使用以下属性配置类别或产品列表页面的URL:

* **类别URL模板**:通过一组占位符定义URL的格式。默认值为`{{page}}.{{id}}.html`，最终生成URL，例如`/content/venia/us/en/products/category-page.3.html`，其中
   * `{{page}}` 替换为  `/content/venia/us/en/products/category-page`
   * `{{id}}` 已被Magento的 `id` 类别属性替换，此处  `3`
* **类别标识符位置**:定义用于获取产品数据的标识符的位置。默认值为`SELECTOR`，另一个可能值为`SUFFIX`。 对于上一个示例URL，这表示将使用标识符`3`获取产品数据。
* **类别标识符类型**:定义获取产品数据时要使用的标识符类型。默认值和当前仅支持的值为`ID`。 对于上一个示例URL，这意味着将使用MagentoGraphQL过滤器（如`category(id:3)`）获取类别数据。

只要组件使用`UrlProvider`设置了相应的数据，就可以为每个模板添加自定义属性。 例如，检查`ProductListItemImpl`类的代码，以了解如何实现此功能。

也可以将`UrlProvider`服务替换为完全自定义的OSGi服务。 在这种情况下，必须实施`UrlProvider`接口，并使用更高的服务等级进行注册，以替换默认实施。

## 与Sling映射组合{#sling-mapping}

除了`UrlProvider`之外，还可以配置[Sling映射](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html)，以便重写和处理URL。 AEM Archetype项目还提供了[一个示例配置](https://github.com/adobe/aem-cif-project-archetype/tree/master/src/main/archetype/samplecontent/src/main/content/jcr_root/etc/map.publish)，用于为端口4503（发布）和80（调度程序）配置一些Sling映射。

## 与AEM Dispatcher结合使用 {#dispatcher}

还可以通过将AEM Dispatcher HTTP服务器与`mod_rewrite`模块结合使用来实现URL重写。 [AEM项目原型](https://github.com/adobe/aem-project-archetype)提供引用AEM Dispatcher配置，该配置已包含生成大小的基本[重写规则](https://github.com/adobe/aem-project-archetype/tree/master/src/main/archetype/dispatcher.cloud)。

## 示例

[Venia引用存储](https://github.com/adobe/aem-cif-guides-venia)项目包含用于演示产品和类别页面自定义URL使用情况的示例配置。 这允许每个项目根据其SEO需求为产品和类别页面设置单个URL模式。 将使用如上所述的CIF `UrlProvider`和Sling映射的组合。

>[!NOTE]
>
>此配置必须使用项目使用的外部域进行调整。 Sling映射基于主机名和域运行。 因此，此配置默认处于禁用状态，且必须在部署之前启用。 为此，请根据使用的域名，重命名`ui.content/src/main/content/jcr_root/etc/map.publish/https`中的Sling映射`hostname.adobeaemcloud.com`文件夹，并通过将`resource.resolver.map.location="/etc/map.publish"`添加到项目的`JcrResourceResolver`配置来启用此配置。

## 其他资源

* [Venia参考存储](https://github.com/adobe/aem-cif-guides-venia)
* [AEM资源映射](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/resource-mapping.html)
* [Sling映射](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html)
