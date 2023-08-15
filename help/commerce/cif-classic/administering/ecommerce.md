---
title: 电子商务集成框架
description: AEM eCommerce帮助营销人员跨Web、移动和社交接触点交付品牌化、个性化的购物体验。
topic-tags: e-commerce
content-type: reference
docset: aem65
exl-id: d995f0d6-9e48-4228-ac82-f33a0b25b9d3
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '749'
ht-degree: 2%

---

# 电子商务{#ecommerce}

* [概念](/help/commerce/cif-classic/administering/concepts.md)
* [管理（通用）](/help/commerce/cif-classic/administering/generic.md)

Adobe提供两个版本的Commerce Integration Framework：

<table>
 <tbody>
  <tr>
   <th><p> </p> </th>
   <th><p>CIF内部部署</p> </th>
   <th><p>CIF Cloud</p> </th>
  </tr>
  <tr>
   <td><p>支持的 AEM 版本</p> </td>
   <td><p>内部部署AEM或AMS 6.x</p> </td>
   <td>AEM AMS 6.4和6.5</td>
  </tr>
  <tr>
   <td><p>后端</p> </td>
   <td>
    <ul>
     <li>AEM， Java</li>
     <li>整体集成，预建映射（模板）</li>
     <li>JCR存储库</li>
    </ul> </td>
   <td>
    <ul>
     <li>Adobe Commerce</li>
     <li>Java和JavaScript</li>
     <li>JCR存储库中未存储商业数据</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>前端</p> </td>
   <td><p>AEM服务器端渲染的页面</p> </td>
   <td>混合页面应用程序（混合渲染）</td>
  </tr>
  <tr>
   <td><p>产品目录</p> </td>
   <td>
    <ul>
     <li>产品导入器、编辑器、AEM中的缓存</li>
     <li>带有AEM或代理页面的常规目录</li>
    </ul> </td>
   <td>
    <ul>
     <li>无产品导入</li>
     <li>通用模板</li>
     <li>通过连接器的按需数据</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>可扩展性</p> </td>
   <td>
    <ul>
     <li>最多可支持数百万个产品（取决于用例）</li>
     <li>Dispatcher上的缓存</li>
    </ul> </td>
   <td>
    <ul>
     <li>无音量限制</li>
     <li>Dispatcher或CDN上的缓存</li>
    </ul> </td>
  </tr>
  <tr>
   <td>标准化数据模型</td>
   <td>否</td>
   <td>是，Adobe Commerce GraphQL架构</td>
  </tr>
  <tr>
   <td>可用性</td>
   <td><p>是。SAPCommerce Cloud(扩展已更新，以支持AEM 6.4和Hybris 5 （默认），并保持与Hybris 4的兼容性</p> <p>SalesforceCommerce Cloud(支持AEM 6.4的开放源连接器)</p> </td>
   <td>通过GitHub的开源提供。 Adobe Commerce (支持2.3.2（默认）并与2.3.1兼容)。</td>
  </tr>
  <tr>
   <td>何时使用</td>
   <td>有限用例：例如，可能需要导入小型静态目录的情况</td>
   <td>大多数用例中的首选解决方案</td>
  </tr>
 </tbody>
</table>

电子商务与产品信息管理(PIM)一起，通过在线商店处理专注于销售产品的网站的活动：

* 产品的创建、生命周期和过时
* 价格管理
* 交易管理
* 管理整个目录
* 实时和集中存储记录
* Web界面

AEM eCommerce帮助营销人员跨Web、移动和社交接触点交付品牌化、个性化的购物体验。 AEM创作环境允许您根据目标访客上下文和促销策略自定义页面和组件；例如：

* 产品页面
* 购物车组件
* 签出组件

该实施允许实时访问产品信息。 这可用于强制执行：

* 产品信息完整性
* 定价
* 库存库存
* 购物车状态的变化

>[!NOTE]
>
>要将集成框架与外部电子商务提供商一起使用，您首先需要安装所需的包。 有关更多信息，请参阅 [部署电子商务](/help/commerce/cif-classic/deploying/ecommerce.md).
>
>有关扩展电子商务功能的信息，请参阅 [发展电子商务](/help/commerce/cif-classic/developing/ecommerce.md).

## 主要功能 {#main-features}

AEM eCommerce提供：

* 数量 **现成的AEM组件** 要说明可为您的项目实现什么，请执行以下操作：

   * 产品显示
   * 购物车
   * 结帐
   * 最近查看的产品
   * 优惠券
   * 和其他

  ![geometrixx组件示例](/help/sites-administering/assets/chlimage_1-130.png)

  >[!NOTE]
  >
  >通过AEM提供的集成框架，您还可以独立于特定的电子商务引擎为商业功能构建其他AEM组件。

* **Search**  — 使用：

   * AEM搜索
   * 电子商务系统的搜寻
   * 第三方搜索
   * 或两者的组合。

  ![搜索示例](/help/sites-administering/assets/chlimage_1-131.png)

* 使用AEM功能 **在多个渠道上展示您的内容**，可以是整个浏览器窗口或移动设备。 这将以访客所需的格式提供您的内容。

  ![移动设备视图示例](/help/sites-administering/assets/chlimage_1-132.png)

* 能够 **根据以下内容开发您自己的集成实施 [AEM电子商务框架](#the-framework)**.

  当前可用的两个实施均基于相同的基础构建 — 基于常规API（框架）。 实施新集成仅涉及实施您的集成所需的功能。 任何新实施均可使用前端组件，因为它们使用接口（因此独立于实施）。

* 开发以下项目的可能性 **基于购物者数据和活动的体验驱动型商务**. 这让您可以了解许多场景：

   * 例如，当订单总额超过特定数量时，可以降低运费。
   * 另一种方法可能会让您提供使用用户档案数据的季节性选件（例如，位置）。 之后，可以高亮显示这些内容，在必要时同样取决于其他因素。

  在下面的示例中，显示了一个Teaser，因为购物车的内容不到$75：

  ![具有客户上下文的购物车](/help/sites-administering/assets/chlimage_1-133.png)

  当购物车内容超过$75时，可以更改此设置：

  ![更改后具有客户端上下文的购物车](/help/sites-administering/assets/chlimage_1-134.png)

* 以及其他功能，包括：

   * 跨会话保留的购物车内容
   * 完整订单历史记录
   * 快速目录更新

## 框架 {#the-framework}

此 [概念](/help/commerce/cif-classic/administering/concepts.md) 部分将更详细地介绍该框架，但以下部分提供了该框架的高级、高速视图：

### 什么？ {#what}

* 集成框架提供了API、一系列用于说明功能的组件，以及多个用于提供连接方法示例的扩展。
* 该框架提供了项目实施所需的基本结构。
* 该框架是可扩展的。
* 该框架不提供现成、随时可用的站点。 始终需要执行一定数量的开发工作来根据您的规范调整框架。

### 为什么？ {#why}

* 提供快速实现定制电子商务网站所需的基本机制。
* Tp提供了开发实际电子商务网站所需的灵活性。
* 说明最佳实践。
