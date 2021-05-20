---
title: 电子商务
description: AEM eCommerce可帮助营销人员在Web、移动和社交接触点中提供品牌化的个性化购物体验。
topic-tags: e-commerce
content-type: reference
docset: aem65
source-git-commit: da538dac17b4c6182b44801b4c79d6cdbf35f640
workflow-type: tm+mt
source-wordcount: '733'
ht-degree: 1%

---

# 电子商务{#ecommerce}

* [概念 ](/help/commerce/cif-classic/administering/concepts.md)
* [管理（一般）](/help/commerce/cif-classic/administering/generic.md)

Adobe提供了商务集成框架的两个版本：

<table>
 <tbody>
  <tr>
   <th><p> </p> </th>
   <th><p>CIF上线</p> </th>
   <th><p>CIF云</p> </th>
  </tr>
  <tr>
   <td><p>支持的 AEM 版本</p> </td>
   <td><p>AEM on-prem或AMS 6.x</p> </td>
   <td>AEM AMS 6.4和6.5</td>
  </tr>
  <tr>
   <td><p>后端</p> </td>
   <td>
    <ul>
     <li>AEM, Java</li>
     <li>整体集成、预构建映射（模板）</li>
     <li>JCR存储库</li>
    </ul> </td>
   <td>
    <ul>
     <li>Magento</li>
     <li>Java和Javascript</li>
     <li>未在JCR存储库中存储商务数据</li>
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
     <li>包含AEM或代理页的常规目录</li>
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
     <li>无卷限制</li>
     <li>Dispatcher或CDN上的缓存</li>
    </ul> </td>
  </tr>
  <tr>
   <td>标准化数据模型</td>
   <td>否</td>
   <td>是，MagentoGraphQL架构</td>
  </tr>
  <tr>
   <td>可用性</td>
   <td><p>是. SAPCommerce Cloud(扩展已更新以支持AEM 6.4和Hybris 5（默认），并维护与Hybris 4的兼容性</p> <p>SalesforceCommerce Cloud(连接器开源以支持AEM 6.4)</p> </td>
   <td>是，可通过GitHub通过开源。 Magento Commerce(支持Magento2.3.2（默认）并与Magento2.3.1兼容)。</td>
  </tr>
  <tr>
   <td>何时使用</td>
   <td>有限用例：例如，可能需要导入小型静态目录的情景</td>
   <td>大多数用例中的首选解决方案</td>
  </tr>
 </tbody>
</table>

电子商务与产品信息管理(PIM)一起处理网站的活动，重点是通过在线商店销售产品：

* 产品的创建、生命周期和过期
* 价格管理
* 交易管理
* 管理整个目录
* 实时和集中存储记录
* Web界面

AEM eCommerce可帮助营销人员在Web、移动和社交接触点中提供品牌化的个性化购物体验。 AEM创作环境允许您根据目标访客上下文和促销策略自定义页面和组件；例如：

* 产品页面
* 购物车组件
* 结帐组件

该实施允许实时访问产品信息。 这可用于强制执行：

* 产品信息完整性
* 定价
* 库存库存
* 购物车状态的变化

>[!NOTE]
>
>要将集成框架与外部电子商务提供程序结合使用，您首先需要安装所需的包。 有关更多信息，请参阅[部署eCommerce](/help/commerce/cif-classic/deploying/ecommerce.md)。
>
>有关扩展电子商务功能的信息，请参阅[开发电子商务](/help/commerce/cif-classic/developing/ecommerce.md)。

## 主要功能{#main-features}

AEM电子商务提供：

* 许多&#x200B;**现成的AEM组件**&#x200B;以说明可为项目实现的目标：

   * 产品显示
   * 购物车
   * 结帐
   * 最近查看的产品
   * 优惠券
   * 其他

   ![](/help/sites-administering/assets/chlimage_1-130.png)

   >[!NOTE]
   >
   >AEM提供的集成框架还允许您为独立于特定电子商务引擎的商务功能构建其他AEM组件。

* **搜索**  — 使用以下任一方式：

   * AEM搜索
   * 电子商务系统的探索
   * 第三方搜索(如Search&amp;Promote)
   * 或两者的组合。

   ![](/help/sites-administering/assets/chlimage_1-131.png)

* 使用AEM功能&#x200B;**在多个渠道（无论是整个浏览器窗口还是移动设备）上显示您的内容**。 这会以访客所需的格式交付内容。

   ![](/help/sites-administering/assets/chlimage_1-132.png)

* 能够根据[AEM电子商务框架&#x200B;](#the-framework)**开发您自己的集成实施。**

   当前可用的两个实施都基于相同的基础构建 — 基于常规API（框架）。 实施新集成仅涉及实施集成所需的功能。 前端组件可供任何新实施使用，因为它们使用的是接口（因此与实施无关）。

* 根据购物者数据和活动&#x200B;**开发**&#x200B;体验驱动型商务的可能性。 这样，您就可以了解许多情景：

   * 例如，当总订单超过特定金额时，可能会降低运输成本。
   * 另一种方法可能允许您提供使用用户档案数据（例如位置）的季节性选件。 然后，可根据其他因素在必要时再次突出显示这些内容。

   在以下示例中，显示了一个Teaser，因为购物车的内容小于$75:

   ![](/help/sites-administering/assets/chlimage_1-133.png)

   当购物车内容超过$75时，可以更改此设置：

   ![](/help/sites-administering/assets/chlimage_1-134.png)

* 以及其他功能，包括：

   * 会话期间保留的购物车内容
   * 完整订单历史记录
   * 快速目录更新

## 框架{#the-framework}

[Concepts](/help/commerce/cif-classic/administering/concepts.md)部分更详细地介绍了框架，但以下部分提供了框架的高级、高速视图：

### 什么？ {#what}

* 集成框架提供了API、一系列用于说明功能的组件以及多个用于提供连接方法示例的扩展。
* 该框架提供了项目实施所需的基本结构。
* 该框架是可扩展的。
* 该框架不提供现成可用的站点。 要使框架符合您的规范，始终需要进行一定量的开发工作。

### 为什么？ {#why}

* 提供快速实现自定义电子商务网站所需的基本机制。
* Tp提供开发真实电子商务网站所需的灵活性。
* 说明最佳实践。
