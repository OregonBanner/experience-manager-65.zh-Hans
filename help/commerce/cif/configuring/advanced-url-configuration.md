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
source-git-commit: 014731aa9c5c4d7d419ff8b037142b47e7b7da01
workflow-type: tm+mt
source-wordcount: '910'
ht-degree: 4%

---

# 高级URL配置 {#url}

>[!NOTE]
>
> 搜索引擎优化 (SEO) 已成为许多营销人员关注的重点。因此，需要解决许多AEM项目中的SEO问题。 请阅读 [SEO和URL管理最佳实践](https://experienceleague.adobe.com/docs/experience-manager-65/managing/managing-further-reference/seo-and-url-management.html) 以了解其他信息。

[AEM CIF核心组件](https://github.com/adobe/aem-core-cif-components) 提供了高级配置，用于自定义产品和类别页面的URL。 许多实施都将自定义这些URL以用于搜索引擎优化(SEO)。 以下视频详细介绍了如何配置 `UrlProvider` 服务和功能 [Sling映射](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html) 自定义产品和类别页面的URL。

>[!VIDEO](https://video.tv.adobe.com/v/34350/?quality=12)

## 配置 {#configuration}

配置 `UrlProvider` 服务，且项目必须为“CIF URL提供程序配置”提供OSGI配置。

>[!NOTE]
>
> 自AEM CIF核心组件版本2.0.0起，URL提供程序配置仅提供预定义的URL格式，而不提供1.x版本中可配置的自由文本格式。 此外，使用选择器在URL中传递数据的方法已被替换为后缀。

### 产品页面URL格式 {#product}

这会配置产品页面的URL，并支持以下选项：

* `{{page}}.html/{{sku}}.html#{{variant_sku}}` (默认)
* `{{page}}.html/{{url_key}}.html#{{variant_sku}}`
* `{{page}}.html/{{sku}}/{{url_key}}.html#{{variant_sku}}`
* `{{page}}.html/{{url_path}}.html#{{variant_sku}}`
* `{{page}}.html/{{sku}}/{{url_path}}.html#{{variant_sku}}`

对于 [Venia参考存储](https://github.com/adobe/aem-cif-guides-venia):

* `{{page}}` 将替换为 `/content/venia/us/en/products/product-page`
* `{{sku}}` 将被产品的sku(例如， `VP09`
* `{{url_key}}` 将被产品的 `url_key` 属性，例如 `lenora-crochet-shorts`
* `{{url_path}}` 将被产品的 `url_path`，例如 `venia-bottoms/venia-pants/lenora-crochet-shorts`
* `{{variant_sku}}` 将被替换为当前选定的变体，例如 `VP09-KH-S`

自 `url_path` 已弃用，预定义的产品URL格式使用 `url_rewrites` 并选择路径段最多的路径段，如果 `url_path` 不可用。

对于上述示例数据，使用默认URL格式设置的产品变体URL将如下所示 `/content/venia/us/en/products/product-page.html/VP09.html#VP09-KH-S`.

### 类别页面URL格式 {#product-list}

这会配置类别或产品列表页面的URL，并支持以下选项：

* `{{page}}.html/{{url_path}}.html` (默认)
* `{{page}}.html/{{url_key}}.html`

对于 [Venia参考存储](https://github.com/adobe/aem-cif-guides-venia):

* `{{page}}` 将替换为 `/content/venia/us/en/products/category-page`
* `{{url_key}}` 将被类别的 `url_key` 属性
* `{{url_path}}` 将被类别的 `url_path`

根据上述示例数据，使用默认URL格式设置的类别页面URL将如下所示 `/content/venia/us/en/products/category-page.html/venia-bottoms/venia-pants.html`.

>[!NOTE]
> 
> 的 `url_path` 是 `url_keys` 产品或类别的祖先和产品或类别的 `url_key` 分隔 `/` 斜线。

### 特定类别/产品页面 {#specific-pages}

可以创建 [多类别和产品页面](multi-template-usage.md) 仅适用于目录类别或产品的特定子集。

的 `UrlProvider` 已预配置为在创作层实例上生成指向此类页面的深层链接。 对于使用“预览”模式浏览网站、导航到特定产品或类别页面并切换回“编辑”模式以编辑页面的编辑器而言，此操作非常有用。

另一方面，在发布层实例上，目录页面URL应保持稳定，以免在搜索引擎排名上丢失增益。 由于该发布层实例默认不会呈现指向特定目录页面的深层链接。 要更改此行为，请 _CIF URL提供商特定的页面策略_ 可以配置为始终生成特定的页面url。

## 自定义URL格式 {#custom-url-format}

要提供自定义URL格式，项目可以在 [`ProductUrlFormat`](https://javadoc.io/doc/com.adobe.commerce.cif/core-cif-components-core/latest/com/adobe/cq/commerce/core/components/services/urls/ProductUrlFormat.html) 或 [`CategoryUrlFormat`](https://javadoc.io/doc/com.adobe.commerce.cif/core-cif-components-core/latest/com/adobe/cq/commerce/core/components/services/urls/CategoryUrlFormat.html) 服务接口，并将实现注册为OSGI服务。 这些实施（如果可用）将替换已配置的预定义格式。 如果注册了多个实施，则具有较高服务排名的实施将替换具有较低服务排名的实施。

自定义URL格式实施必须实施一对方法，以根据给定参数构建URL，并解析URL以分别返回相同的参数。

## 与Sling映射结合使用 {#sling-mapping}

除 `UrlProvider`，则还可以配置 [Sling映射](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html) 以便重写和处理URL。 AEM Archetype项目还提供 [示例配置](https://github.com/adobe/aem-cif-project-archetype/tree/master/src/main/archetype/samplecontent/src/main/content/jcr_root/etc/map.publish) 为端口4503（发布）和80（调度程序）配置一些Sling映射。

## 与AEM Dispatcher结合使用 {#dispatcher}

还可以通过将AEM Dispatcher HTTP服务器与 `mod_rewrite` 模块。 的 [AEM项目原型](https://github.com/adobe/aem-project-archetype) 提供引用AEM Dispatcher配置，该配置已包含基本 [重写规则](https://github.com/adobe/aem-project-archetype/tree/master/src/main/archetype/dispatcher.cloud) 的值。

## 示例

的 [Venia参考存储](https://github.com/adobe/aem-cif-guides-venia) 项目包含用于演示产品和类别页面使用自定义URL的示例配置。 这允许每个项目根据其SEO需求为产品和类别页面设置单个URL模式。 CIF的组合 `UrlProvider` 和Sling映射（如上所述）。

>[!NOTE]
>
>此配置必须使用项目使用的外部域进行调整。 Sling映射基于主机名和域运行。 因此，此配置默认处于禁用状态，且必须在部署之前启用。 为此，请重命名Sling映射 `hostname.adobeaemcloud.com` 文件夹 `ui.content/src/main/content/jcr_root/etc/map.publish/https` 根据使用的域名，并通过添加 `resource.resolver.map.location="/etc/map.publish"` 到 `JcrResourceResolver` 项目的配置。

## 其他资源

* [Venia参考存储](https://github.com/adobe/aem-cif-guides-venia)
* [AEM资源映射](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/resource-mapping.html)
* [Sling映射](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html)
