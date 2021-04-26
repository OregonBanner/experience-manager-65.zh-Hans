---
title: 高级URL配置
description: 了解如何自定义产品和类别页面的URL。 这允许实施优化搜索引擎的URL并促进发现。
sub-product: 商务
doc-type: technical-video
activity: setup
audience: administrator
feature: Commerce Integration Framework
kt: 4933
thumbnail: 34350.jpg
translation-type: tm+mt
source-git-commit: d92a635d41cf1b14e109c316bd7264cf7d45a9fe
workflow-type: tm+mt
source-wordcount: '792'
ht-degree: 3%

---

# 高级URL配置{#url}

[AEM CIF核心组](https://github.com/adobe/aem-core-cif-components) 件提供高级配置，以自定义产品和类别页面的URL。许多实施将自定义这些URL以用于搜索引擎优化(SEO)目的。  以下视频详细说明了如何配置`UrlProvider`服务和[Sling Mapping](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html)的功能，以自定义产品和类别页面的URL。

>[!VIDEO](https://video.tv.adobe.com/v/34350/?quality=12)

## 配置 {#configuration}

要根据SEO要求配置`UrlProvider`服务，并需要项目必须为“CIF URL提供程序配置”配置提供OSGI配置，并按如下所述配置服务。

>[!NOTE]
>
> [Venia Reference store](https://github.com/adobe/aem-cif-guides-venia)项目，请参见下文，其中包含说明产品和类别页面使用自定义URL的示例配置。

### 产品页面URL模板{#product}

这会使用以下属性配置产品页面的URL:

* **产品URL模板**:通过一组占位符定义URL的格式。默认值为`{{page}}.{{url_key}}.html#{{variant_sku}}`，最后生成URL，如`/content/venia/us/en/products/product-page.chaz-kangeroo-hoodie.html#MH01-M-Orange`
   * `{{page}}` 替换为  `/content/venia/us/en/products/product-page`
   * `{{url_key}}` 已被Magento的 `url_key` 产品属性替换，此处  `chaz-kangeroo-hoodie`
   * `{{variant_sku}}` 由当前选定的变体替换，此处  `MH01-M-Orange`
* **产品标识符位置**:定义将用于获取产品数据的标识符的位置。默认值为`SELECTOR`，另一个可能值为`SUFFIX`。 对于上一个示例URL，这意味着标识符`chaz-kangeroo-hoodie`将用于获取产品数据。
* **产品标识符类型**:定义获取产品数据时要使用的标识符的类型。默认值为`URL_KEY`，另一个可能值为`SKU`。 对于上一个示例URL，这意味着将使用MagentoGraphQL过滤器（如`filter:{url_key:{eq:"chaz-kangeroo-hoodie"}}`）获取产品数据。

### 产品列表页URL模板{#product-list}

这将使用以下属性配置类别或产品列表页面的URL:

* **类别URL模板**:通过一组占位符定义URL的格式。默认值为`{{page}}.{{id}}.html`，最后生成URL，如`/content/venia/us/en/products/category-page.3.html`
   * `{{page}}` 替换为  `/content/venia/us/en/products/category-page`
   * `{{id}}` 被Magento的 `id` 类别属性替换  `3`
* **类别标识符位置**:定义将用于获取产品数据的标识符的位置。默认值为`SELECTOR`，另一个可能值为`SUFFIX`。 对于上一个示例URL，这意味着标识符`3`将用于获取产品数据。
* **类别标识符类型**:定义获取产品数据时要使用的标识符的类型。默认值和当前仅支持的值为`ID`。 对于上一个示例URL，这意味着将使用MagentoGraphQL过滤器（如`category(id:3)`）获取类别数据。

只要组件使用`UrlProvider`设置了相应的数据，就可以为每个模板添加自定义属性。 检查`ProductListItemImpl`类的代码示例，了解如何实现该类。

还可以用完全自定义的OSGi服务替换`UrlProvider`服务。 在这种情况下，必须实现`UrlProvider`接口，并使用更高的服务等级对其进行注册，以替换默认实现。

## 与Sling映射组合{#sling-mapping}

除了`UrlProvider`之外，还可以配置[Sling映射](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html)以重写和处理URL。 AEM Archetype项目还提供[示例配置](https://github.com/adobe/aem-cif-project-archetype/tree/master/src/main/archetype/samplecontent/src/main/content/jcr_root/etc/map.publish)，以为端口4503（发布）和80（调度程序）配置某些Sling映射。

## 与AEM Dispatcher {#dispatcher}结合使用

也可以通过使用带有`mod_rewrite`模块的AEM Dispatcher HTTP服务器来实现URL重写。 [AEM Project Archetype](https://github.com/adobe/aem-project-archetype)提供引用AEM Dispatcher配置，该配置已经包含生成大小的基本[重写规则](https://github.com/adobe/aem-project-archetype/tree/master/src/main/archetype/dispatcher.cloud)。

## 示例

[Venia Reference store](https://github.com/adobe/aem-cif-guides-venia)项目包含示例配置，用于演示产品和类别页面的自定义URL的用法。 这允许每个项目根据其SEO需求为产品和类别页面设置单独的URL模式。 使用CIF `UrlProvider`和Sling映射的组合，如上所述。

>[!NOTE]
>
>此配置必须使用项目使用的外部域进行调整。 Sling映射基于主机名和域运行。 因此，此配置在默认情况下处于禁用状态，在部署之前必须启用。 为此，请根据使用的域名重命名`ui.content/src/main/content/jcr_root/etc/map.publish/https`中的Sling Mapping `hostname.adobeaemcloud.com`文件夹，并通过将`resource.resolver.map.location="/etc/map.publish"`添加到项目的`JcrResourceResolver`配置来启用此配置。

## 其他资源

* [Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia)
* [AEM资源映射](https://docs.adobe.com/content/help/en/experience-manager-65/deploying/configuring/resource-mapping.html)
* [Sling映射](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html)
