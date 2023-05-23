---
title: 简介和概述
description: Content and Commerce 的简介和概述。Experience Manager Commerce Integration Framework (CIF) 是 Adobe 推荐的模式，用于通过 Experience Cloud 集成和扩展来自 Adobe Commerce 和其他第三方商务解决方案的商务服务。
thumbnail: introducing-aem-commerce.jpg
exl-id: 52dad8f9-1812-42a3-8106-92b23f8517cd
source-git-commit: a467009851937c4a10b165a3d253c47bf990bbc5
workflow-type: tm+mt
source-wordcount: '870'
ht-degree: 92%

---

# Content and Commerce {#content-commerce}

借助 Adobe Experience Manager Content and Commerce，品牌可以更快地扩展和创新，区分商务体验并捕获快速增长的在线支出。AEM Content and Commerce 将 Experience Manager 中的沉浸式、全渠道和个性化体验与任意数量的商务解决方案相结合，为购物历程的各个部分带来差异化的体验，缩短价值实现时间并加快实现更高的转化率。

## Content and Commerce 如何帮助客户取得成功

随着客户对在线商务体验的期望不断提高，品牌不得不更快地交付差异化的体验和更多内容。然而，实施内容管理平台通常需要花费大量时间和预算来开发基础元素（例如，自定义组件和创作工具），并且会增加维护和升级成本。Experience Manager Sites 提供 Content and Commerce 作为 Experience Manager 的附加模块，这将提供现成的商务核心组件、创作工具和引用店面，以加速上线，实现跨团队的无缝协作并提高转化率。

品牌可以将 Experience Manager 与 Adobe Commerce（Adobe Experience Cloud 的一部分）以及任何选定商务引擎集成。借助 Experience Manager Content and Commerce，品牌可以：

* 更快地扩展和创新
* 用于推动转化的个性化体验
* 一次创建，随处发布
* 丰富和区分面向客户的体验
* 通过商业数据访问简化创作

## 介绍 AEM Commerce Integration Framework (CIF) {#cif-intro}

由于这些项目必须处理集成商务解决方案方面的复杂性。商務解決方案可以是任何商業解決方案，例如Adobe Commerce或一組自訂商務服務。 集成高度依赖于用例和生态系统。它通常涉及不同的位置并具有许多不同的风格：

* 集成复杂、动态的生态系统（示例产品目录）
* 企业需要以高效的全渠道方式管理具有其生命周期的产品内容
* 为各种头构建复杂、个性化的购物历程
* 能够在后端和前端快速适应并进行创新
* 运行可扩展、稳定的 E2E 基础架构，该基础架构专为实现最佳性能而构建（限时抢购、黑色星期五...）。这包括统一搜索和缓存管理。

这种复杂性会导致出现潜在故障点、增加 TCO、产生延迟和减少实现的价值。这些原因促使开发 Commerce Integration Framework (CIF)，它是 Experience Manager 的加载项。CIF 利用商务功能扩展 Experience Manager，并实施与商务引擎的集成的标准化。最终获得具有前瞻性、稳定且可扩展的解决方案，同时 TCO 更低。它通过敏捷的工具和无缝集成的功能解锁技术和业务创新，从而构建引人入胜的商务体验。

![CIF 元素](./assets/CIF/CIF_Overview.png)

## 自 2013 年以来，CIF 一直为客户提供强有力的支持

CIF 拥有 200 多家客户，已成为促使 Content and Commerce 项目取得成功的重要因素。这为当今和将来的 IT 和企业提供了价值。最近的客户项目将 CIF 描述为“用于加速和节省大量时间的绝佳工具，具有巨大的价值”。

## CIF 好处 {#cif-benefits}

CIF 提供现成的商务核心组件，可减少对自定义代码的需求，从而加快品牌的上市速度。所有核心组件都与 Adobe 的客户端数据层即时集成以补充客户配置文件（例如，统一配置文件）。此配置文件详细捕获访客行为，可用于实时预测和个性化设置客户历程。

CIF 加载项将产品上下文引入 Experience Manager 中，并提供产品控制台和产品/类别选取器等创作工具，使营销人员能够在 Experience Manager 中创建和交付可购买的体验，而无需依靠开发人员。优势包括：

### 体验

利用 AEM 中功能强大的 CIF 工具，内容创建者能够以可扩展且与交付无关的方式快速构建丰富且个性化的商务体验来抓住商机。

![CIF 元素](./assets/CIF/CIF_Product_Experience_Management.png)

### 价值实现时间 (TTV)

加速專案開發，使用 [AEM Core Components](https://www.aemcomponents.dev/)， [AEM Venia參考店面](https://github.com/adobe/aem-cif-guides-venia)， [AEM專案原型](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html)和PWA（Headless內容和商務）的整合模式。

CIF 旨在通过始终保持最新的加载项持续创新，使客户能够访问新的和改进的功能。

### 集成

使用以下專案將您的生態系統（例如商務解決方案）與Experience Cloud連線：  [Adobe I/O Runtime](https://www.adobe.io/apis/experienceplatform/runtime.html)，一種基於微服務的無伺服器PaaS，以及 [CIF的參考實作](https://github.com/adobe/commerce-cif-graphql-integration-reference).

## 经过验证的模式和最佳实践

CIF 利用基于最佳实践的标准化集成模式来为客户提供支持。这有助于客户在当今环境中取得成功，能够灵活地与客户一起成长并满足未来要求：

* 消除了可能出现的产品目录集成方面的典型挑战。示例：
   * 目录量或复杂性增加所带来的性能问题
   * 无法访问暂存数据
   * 需要实时产品数据和体验
* 不断提高的数字化成熟度产生了对体验管理的需求。CIF 附带产品体验管理功能，无需额外的 IT 工作即可逐步整合这些功能。
* 全渠道就绪：CIF 支持具有模式、加速器和核心组件的多种接触点技术（服务器端、混合、客户端）。
