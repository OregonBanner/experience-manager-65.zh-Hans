---
title: AEM内容和商务入门
description: 了解如何部署AEM内容和商务项目。
topics: Commerce
feature: Commerce Integration Framework
thumbnail: 37843.jpg
translation-type: tm+mt
source-git-commit: 8ead3d1b24177effa4d40141408c5676eaabcc30
workflow-type: tm+mt
source-wordcount: '682'
ht-degree: 2%

---

# AEM Content and Commerce {#start}快速入门

要开始使用AEM Content and Commerce，您需要安装AEM Content and Commerce Add-On for AEM 6.5。

## 最低软件要求

[需要AEM 6.5 Service](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)  Pack 7或更高版本。

## 入门 {#onboarding}

AEM内容和商务入门是一个分两步的过程：

1. 安装适用于AEM 6.5的AEM Content and Commerce Add-On

2. 将AEM与您的商业解决方案连接

### 安装适用于AEM 6.5的AEM Content and Commerce Add-on

从[软件分发](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)门户下载并安装AEM Commerce Add-On for AEM 6.5。

开始并安装所需的AEM 6.5 Service Pack。 我们建议安装上一个可用的Service Pack。

    >[!NOTE]
    >
    >这将由AEM Managed Service客户的CSE完成。

### 将AEM连接到您的商务系统

AEM可以连接到任何具有AEM的可访问GraphQL端点的商务系统。 这些端点通常是公开可用的，也可以通过专用VPN或本地连接进行连接，具体取决于各个项目设置。

或者，可以提供身份验证头以使用需要身份验证的附加CIF功能。

必须调整由[AEM Project Archetype](https://github.com/adobe/aem-project-archetype)和[AEM Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia)生成的项目（已包含在[默认配置](https://github.com/adobe/aem-cif-guides-venia/blob/main/ui.config/src/main/content/jcr_root/apps/venia/osgiconfig/config/com.adobe.cq.commerce.graphql.client.impl.GraphqlClientImpl~default.cfg.json)中）。

将`com.adobe.cq.commerce.graphql.client.impl.GraphqlClientImpl~default.cfg.json`中`url`的值替换为商务系统的GraphQL端点。 此配置可以通过OSGI控制台或通过项目部署OSGI配置来完成。 使用不同的AEM运行模式支持不同的暂存和生产系统配置。

AEM Content and Commerce Add-On和CIF核心组件使用AEM服务器端和客户端连接。 默认情况下，客户端CIF核心组件和CIF附加创作工具会连接到`/api/graphql`。 如有需要，可通过CIFCloud Service配置来调整此值（见下文）。

CIF加载项在`/api/graphql`处提供GraphQL代理servlet，该GraphQL代理servlet可选用于[本地开发](develop.md)。 对于生产部署，强烈建议通过AEM Dispatcher或其他网络层（如CDN）设置商务GraphQL端点的反向代理。

## 配置商店和目录{#catalog}

加载项和[CIF核心组件](https://github.com/adobe/aem-core-cif-components)可用于连接到不同商店(或商店视图等)的多个AEM站点结构。 默认情况下，CIF加载项部署时会使用连接到Adobe Commerce的默认商店和目录(Magento)的默认配置。

此配置可通过CIFCloud Service配置按以下步骤调整：

1. 在AEM中，转到工具 — >Cloud Services-> CIF配置

2. 选择要更改的商务配置

3. 通过操作栏打开配置属性

![CIFCloud Services配置](/help/commerce/cif/assets/cif-cloud-service-config.png)

可以配置以下属性：

- GraphQL客户端 — 为商务后端通信选择已配置的GraphQL客户端。 这通常应保持为默认值。
- 存储视图-(Magento)存储视图标识符。 如果为空，则使用默认存储视图。
- GraphQL代理路径 — AEM中用于代理向商务后端GraphQL端点的请求的URL路径GraphQL代理。
   >[!NOTE]
   >
   > 在大多数设置中，默认值`/api/graphql`不得更改。 只有不使用提供的GraphQL代理的高级设置才应更改此设置。
- 启用目录UID支持 — 在商务后端GraphQL调用中启用UID而非ID支持。
   >[!NOTE]
   >
   > Adobe Commerce(Magento)2.4.2中引入了对UID的支持。仅当您的商务后端支持版本2.4.2或更高版本的GraphQL模式时，才启用此功能。
- 目录根类别标识符 — 存储目录根的标识符（UID或ID）

上面所示的配置供参考。 项目应提供自己的配置。

有关使用多个AEM站点结构并结合不同商务目录的更复杂设置，请参阅[商务多商店设置](configuring/multi-store-setup.md)教程。

## 其他资源 {#additional-resources}

- [AEM 项目原型](https://github.com/adobe/aem-project-archetype)
- [AEM Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia)
- [商务多商店设置](configuring/multi-store-setup.md)
