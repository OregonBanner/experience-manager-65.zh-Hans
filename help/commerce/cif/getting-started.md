---
title: AEM Content and Commerce快速入门
description: 了解如何部署AEM内容和商务项目。
topics: Commerce
feature: 商务集成框架
source-git-commit: 1b200ea21709cd9234c92da8a8ef6145d2c2f635
workflow-type: tm+mt
source-wordcount: '721'
ht-degree: 1%

---


# AEM Content and Commerce快速入门 {#start}

要开始使用AEM Content and Commerce，您需要安装适用于AEM 6.5的AEM Content and Commerce Add-On。

## 最低软件要求

[需要AEM 6.5 Service Pack](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)  7或更高版本。

## 入门 {#onboarding}

AEM内容和商务的入门过程分为两步：

1. 安装适用于AEM 6.5的AEM Content and Commerce加载项

2. 将AEM与您的商务解决方案连接

### 安装适用于AEM 6.5的AEM Content and Commerce加载项 {#install-add-on}

从[Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)门户下载并安装适用于AEM 6.5的AEM Commerce附加组件。

启动并安装所需的AEM 6.5 Service Pack。 我们建议安装最后一个可用的Service Pack。

>[!NOTE]
>
>这将由AEM Managed Service客户的CSE来完成。

### 将AEM连接到您的Commerce System {#connect}

AEM可以连接到任何具有AEM可访问GraphQL端点的商务系统。 这些端点通常是公开可用的，或可通过专用VPN或本地连接进行连接，具体取决于各个项目设置。

可选地，可以提供验证标头以使用需要验证的其他CIF功能。

必须调整由[AEM项目原型](https://github.com/adobe/aem-project-archetype)和[AEM Venia引用存储](https://github.com/adobe/aem-cif-guides-venia)生成的项目，这些项目已包含在[默认配置](https://github.com/adobe/aem-cif-guides-venia/blob/main/ui.config/src/main/content/jcr_root/apps/venia/osgiconfig/config/com.adobe.cq.commerce.graphql.client.impl.GraphqlClientImpl~default.cfg.json)中。

将`com.adobe.cq.commerce.graphql.client.impl.GraphqlClientImpl~default.cfg.json`中的`url`值替换为商务系统的GraphQL端点。 此配置可通过OSGi控制台或通过项目部署OSGi配置来完成。 使用不同的AEM运行模式支持暂存和生产系统的不同配置。

AEM内容和商务附加组件和CIF核心组件同时使用AEM服务器端和客户端连接。 客户端CIF核心组件和CIF附加组件创作工具默认会连接到`/api/graphql`。 如有需要，可通过CIFCloud Service配置调整此值（请参阅下文）。

CIF附加组件在`/api/graphql`处提供了GraphQL代理Servlet，可选择用于[本地开发](develop.md)。 对于生产部署，强烈建议通过AEM Dispatcher或其他网络层（如CDN）设置商务GraphQL端点的反向代理。

## 配置存储和目录 {#catalog}

附加组件和[CIF核心组件](https://github.com/adobe/aem-core-cif-components)可用于连接到不同商务商店（或存储视图等）的多个AEM站点结构。 默认情况下，CIF附加组件会部署为一个默认配置，该配置连接到Adobe商务的默认商店和目录(Magento)。

可通过CIFCloud Service配置按照以下步骤操作，针对项目调整此配置：

1. 在AEM中，转到“工具” — >“Cloud Services” — > CIF配置

2. 选择要更改的商务配置

3. 通过操作栏打开配置属性

![CIFCloud Services配置](/help/commerce/cif/assets/cif-cloud-service-config.png)

可以配置以下属性：

- GraphQL客户端 — 为商务后端通信选择已配置的GraphQL客户端。 此设置通常应保持默认状态。
- 存储视图 — (Magento)存储视图标识符。 如果为空，则使用默认的存储视图。
- GraphQL代理路径 — AEM中用于将请求代理到商务后端GraphQL端点的URL路径GraphQL代理。
   >[!NOTE]
   >
   > 在大多数设置中，默认值`/api/graphql`不得更改。 只有不使用提供的GraphQL代理的高级设置才应更改此设置。
- 启用目录UID支持 — 在商务后端GraphQL调用中启用对UID的支持，而不是ID。
   >[!NOTE]
   >
   > 在Adobe商务(Magento)2.4.2中引入了对UID的支持。仅当您的商务后端支持版本2.4.2或更高版本的GraphQL架构时，才启用此功能。
- 目录根类别标识符 — 存储目录根的标识符（UID或ID）
   >[!CAUTION]
   >
   > 从CIF核心组件版本2.0.0开始，`id`支持已移除，并替换为`uid`。 如果您的项目使用CIF核心组件版本2.0.0，则必须启用“目录UID支持”，并使用有效的类别UID作为“目录根类别标识符”。

上面显示的配置供参考。 项目应提供自己的配置。

有关使用多个AEM站点结构并结合不同商务目录的更复杂设置，请参阅[商务多商店设置](configuring/multi-store-setup.md)教程。

## 其他资源 {#additional-resources}

- [AEM 项目原型](https://github.com/adobe/aem-project-archetype)
- [AEM Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia)
- [商务多商店设置](configuring/multi-store-setup.md)
