---
title: 高级URL配置
description: 了解如何自定义产品和类别页面的URL。 这允许实施优化搜索引擎的URL并促进发现。
sub-product: Commerce
doc-type: technical-video
activity: setup
audience: administrator
feature: Commerce Integration Framework
kt: 4933
thumbnail: 34350.jpg
exl-id: 0125021a-1c00-4ea3-b7fb-1533b7b9f4f2
source-git-commit: 1ef5593495b4bf22d2635492a360168bccc1725d
workflow-type: tm+mt
source-wordcount: '898'
ht-degree: 6%

---

# 高级URL配置 {#url}

>[!NOTE]
>
>搜索引擎优化 (SEO) 已成为许多营销人员关注的重点。因此，必须解决许多AEM项目中的SEO问题。 参见 [seo和URL管理最佳实践](https://experienceleague.adobe.com/docs/experience-manager-65/managing/managing-further-reference/seo-and-url-management.html) 以获取其他信息。

[AEM CIF核心组件](https://github.com/adobe/aem-core-cif-components) 提供高级配置以自定义产品和类别页面的URL。 许多实施都自定义这些URL以实现搜索引擎优化(SEO)。 以下视频详细介绍如何配置 `UrlProvider` 的服务和功能 [Sling映射](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html) 自定义产品和类别页面的URL。

>[!VIDEO](https://video.tv.adobe.com/v/34350/?quality=12)

## 配置 {#configuration}

要配置 `UrlProvider` 服务根据SEO要求和需求，项目必须提供“CIF URL提供程序配置”的OSGI配置。

>[!NOTE]
>
>自AEM CIF核心组件2.0.0版以来，“URL提供程序”配置仅提供预定义的url格式，而不提供1.x版中已知的自由文本可配置格式。 此外，使用选择器在URL中传递数据的方法已替换为后缀。

### 产品页面URL格式 {#product}

这会配置产品页面的URL，并支持以下选项：

* `{{page}}.html/{{sku}}.html#{{variant_sku}}`（默认）
* `{{page}}.html/{{url_key}}.html#{{variant_sku}}`
* `{{page}}.html/{{sku}}/{{url_key}}.html#{{variant_sku}}`
* `{{page}}.html/{{url_path}}.html#{{variant_sku}}`
* `{{page}}.html/{{sku}}/{{url_path}}.html#{{variant_sku}}`

对于 [Venia引用存储](https://github.com/adobe/aem-cif-guides-venia)：

* `{{page}}` 替换为 `/content/venia/us/en/products/product-page`
* `{{sku}}` 替换为产品的SKU，例如， `VP09`
* `{{url_key}}` 由产品的 `url_key` 属性，例如， `lenora-crochet-shorts`
* `{{url_path}}` 由产品的 `url_path`例如， `venia-bottoms/venia-pants/lenora-crochet-shorts`
* `{{variant_sku}}` 被当前选定的变体替换，例如， `VP09-KH-S`

由于 `url_path` 已弃用，预定义的产品URL格式使用产品的 `url_rewrites` 并选取路径段数最多的路径作为替代路径，如果 `url_path` 不可用。

对于上述示例数据，使用默认URL格式的产品变体URL如下所示 `/content/venia/us/en/products/product-page.html/VP09.html#VP09-KH-S`.

### 类别页面URL格式 {#product-list}

这将配置类别或产品列表页面的URL，并支持以下选项：

* `{{page}}.html/{{url_path}}.html`（默认）
* `{{page}}.html/{{url_key}}.html`

对于 [Venia引用存储](https://github.com/adobe/aem-cif-guides-venia)：

* `{{page}}` 替换为 `/content/venia/us/en/products/category-page`
* `{{url_key}}` 替换为类别的 `url_key` 属性
* `{{url_path}}` 替换为类别的 `url_path`

对于上述示例数据，使用默认URL格式设置的类别页面URL如下所示 `/content/venia/us/en/products/category-page.html/venia-bottoms/venia-pants.html`.

>[!NOTE]
> 
>此 `url_path` 是以下项的连接： `url_keys` 产品或类别的祖先以及产品或类别的 `url_key` 分隔方式 `/` slash。

### 特定类别 — /产品页面 {#specific-pages}

可以创建 [多个类别和产品页面](multi-template-usage.md) 仅用于特定类别子集或目录产品。

此 `UrlProvider` 已预配置为在创作层实例上生成指向此类页面的深层链接。 这对于编辑器非常有用，编辑器使用预览模式浏览网站，导航到特定产品或类别页面，然后切换回编辑模式以编辑页面。

另一方面，在发布层实例上，目录页面URL应保持稳定，以免在搜索引擎排名上失去优势。 因此，默认情况下，发布层实例不会呈现指向特定目录页面的深层链接。 要更改此行为，请 _特定于CIF URL提供程序的页面策略_ 可以配置为始终生成特定的页面url。

## 自定义URL格式 {#custom-url-format}

要提供项目可以实施的自定义URL格式，请执行以下操作 [`ProductUrlFormat`](https://javadoc.io/doc/com.adobe.commerce.cif/core-cif-components-core/latest/com/adobe/cq/commerce/core/components/services/urls/ProductUrlFormat.html) 或 [`CategoryUrlFormat`](https://javadoc.io/doc/com.adobe.commerce.cif/core-cif-components-core/latest/com/adobe/cq/commerce/core/components/services/urls/CategoryUrlFormat.html) 服务接口，并将实现注册为OSGI服务。 这些实施（如果可用）会替换已配置的预定义格式。 如果注册了多个实施，则服务排名较高的实施将替换服务排名较低的实施。

自定义URL格式实施必须实施一对方法，以便从给定参数构建URL，并解析URL以分别返回相同的参数。

## 与Sling映射组合 {#sling-mapping}

除了 `UrlProvider`，也可以配置 [Sling映射](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html) 重写和处理URL。 AEM原型项目还提供 [示例配置](https://github.com/adobe/aem-cif-project-archetype/tree/master/src/main/archetype/samplecontent/src/main/content/jcr_root/etc/map.publish) 为端口4503（发布）和80（调度程序）配置一些Sling映射。

## 与AEM调度程序相结合 {#dispatcher}

通过将AEM Dispatcher HTTP服务器与结合使用，还可以实现URL重写 `mod_rewrite` 模块。 此 [AEM项目原型](https://github.com/adobe/aem-project-archetype) 提供了参考AEM Dispatcher配置，其中已包含基本 [重写规则](https://github.com/adobe/aem-project-archetype/tree/master/src/main/archetype/dispatcher.cloud) 生成的大小。

## 示例

此 [Venia引用存储](https://github.com/adobe/aem-cif-guides-venia) project包含示例配置，用于演示自定义URL在产品和类别页面中的用法。 这样，每个项目就可以根据其SEO需求，为产品和类别页面设置单独的URL模式。 CIF组合 `UrlProvider` 和如上所述的Sling映射一起使用。

>[!NOTE]
>
>必须使用该项目使用的外部域调整此配置。 Sling映射基于主机名和域工作。 因此，此配置在默认情况下处于禁用状态，必须在部署之前启用。 为此，请重命名Sling映射 `hostname.adobeaemcloud.com` 文件夹位置 `ui.content/src/main/content/jcr_root/etc/map.publish/https` 根据使用的域名，并通过添加以下内容启用此配置 `resource.resolver.map.location="/etc/map.publish"` 到 `JcrResourceResolver` 项目的配置。

## 其他资源

* [Venia引用存储](https://github.com/adobe/aem-cif-guides-venia)
* [AEM资源映射](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/resource-mapping.html)
* [Sling映射](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html)
