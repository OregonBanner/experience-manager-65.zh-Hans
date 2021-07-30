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
exl-id: 0125021a-1c00-4ea3-b7fb-1533b7b9f4f2
source-git-commit: dbd38aa75caa7c3c2feee79702ab85ab397eb583
workflow-type: tm+mt
source-wordcount: '745'
ht-degree: 3%

---

# 高级URL配置 {#url}

[AEM CIF核心组](https://github.com/adobe/aem-core-cif-components) 件提供了高级配置，用于自定义产品和类别页面的URL。许多实施都将自定义这些URL以用于搜索引擎优化(SEO)。 以下视频详细介绍了如何配置`UrlProvider`服务和[Sling映射](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html)的功能，以自定义产品和类别页面的URL。

>[!VIDEO](https://video.tv.adobe.com/v/34350/?quality=12)

## 配置 {#configuration}

要根据SEO要求和需要配置`UrlProvider`服务，项目必须为“CIF URL提供程序配置”提供OSGI配置。

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

对于[Venia引用存储](https://github.com/adobe/aem-cif-guides-venia):

* `{{page}}` 将替换为  `/content/venia/us/en/products/product-page`
* `{{sku}}` 将被产品的sku(例如，  `VP09`
* `{{url_key}}` 将被产品的属 `url_key` 性(例如  `lenora-crochet-shorts`
* `{{url_path}}` 将被产品的(例如， `url_path`C.  `venia-bottoms/venia-pants/lenora-crochet-shorts`
* `{{variant_sku}}` 将被替换为当前选定的变体，例如  `VP09-KH-S`

根据上述示例数据，使用默认URL格式设置格式的产品变体URL将类似于`/content/venia/us/en/products/product-page.html/VP09.html#VP09-KH-S`。

### 类别页面URL格式 {#product-list}

这会配置类别或产品列表页面的URL，并支持以下选项：

* `{{page}}.html/{{url_path}}.html` (默认)
* `{{page}}.html/{{url_key}}.html`

对于[Venia引用存储](https://github.com/adobe/aem-cif-guides-venia):

* `{{page}}` 将替换为  `/content/venia/us/en/products/category-page`
* `{{url_key}}` 将替换为类别的属 `url_key` 性
* `{{url_path}}` 将被类别的  `url_path`

根据上述示例数据，使用默认URL格式设置的类别页面URL将类似于`/content/venia/us/en/products/category-page.html/venia-bottoms/venia-pants.html`。

>[!NOTE]
> 
> `url_path`是产品或类别的祖先的`url_keys`与产品或类别的`url_key`之间以`/`斜杠分隔的串联。

## 自定义URL格式 {#custom-url-format}

要提供自定义URL格式，项目可以实施[`UrlFormat`界面](https://javadoc.io/doc/com.adobe.commerce.cif/core-cif-components-core/latest/com/adobe/cq/commerce/core/components/services/urls/UrlFormat.html)并将实施注册为OSGI服务，将其用作类别页面或产品页面URL格式。 `UrlFormat#PROP_USE_AS`服务属性指示要替换的已配置预定义格式中的哪些格式：

* `useAs=productPageUrlFormat`，将替换配置的产品页面url格式
* `useAs=categoryPageUrlFormat`，将替换已配置的类别页面url格式

如果有多个已注册为OSGI服务的`UrlFormat`实现，则具有较高服务排名的实现将具有较低服务排名的实现替换掉。

`UrlFormat`必须实施一对方法，以根据给定的参数映射构建URL，并解析URL以返回相同的参数映射。 参数与上述内容相同，只有对于类别，才向`UrlFormat`提供附加的`{{uid}}`参数。

## 与Sling映射结合使用 {#sling-mapping}

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
