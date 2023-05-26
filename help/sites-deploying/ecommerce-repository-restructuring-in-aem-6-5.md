---
title: AEM 6.5中的电子商务存储库重组
seo-title: E-Commerce Repository Restructuring in AEM 6.5
description: 了解如何进行必要的更改，以迁移到AEM 6.5 for E-Commerce中的新存储库结构。
seo-description: Learn how to make the necessary changes in order to migrate to the new repository structure in AEM 6.5 for E-Commerce.
uuid: 1fff1a4b-c8d0-4016-92fb-e2ea26e3a302
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
discoiquuid: 28c92e7d-2106-4333-afa6-c5528a00d7b4
feature: Upgrading
exl-id: 78b7c497-c474-4308-bfab-8f424b5f7268
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '202'
ht-degree: 2%

---

# AEM 6.5中的电子商务存储库重组{#e-commerce-repository-restructuring-in-aem}

如父项中所述 [AEM 6.5中的存储库重组](/help/sites-deploying/repository-restructuring.md) 页面，升级到AEM 6.5的客户应使用此页面评估与影响AEM E-Commerce Solution的存储库更改相关的工作量。 在AEM 6.5升级过程中，有些更改需要您投入精力，而有些则可能会推迟到将来升级。

## 6.5版升级 {#with-upgrade}

### 产品、订单、托收、分类、配送方式和支付方式数据 {#product-order-collections-classifications-shipping-methods-and-payment-methods-data}

<table>
 <tbody>
  <tr>
   <td><strong>上一个位置</strong></td>
   <td><p><code>/etc/commerce/products</code></p> <p><code>/etc/commerce/orders</code></p> <p><code>/etc/commerce/collections</code></p> <p><code>/etc/commerce/classifications</code></p> <p><code>/etc/commerce/shipping-methods</code></p> <p><code>/etc/commerce/payment-methods</code></p> </td>
  </tr>
  <tr>
   <td><strong>新位置</strong></td>
   <td><p><code>/var/commerce/products</code></p> <p><code>/var/commerce/orders</code></p> <p><code>/var/commerce/collections</code></p> <p><code>/var/commerce/classifications</code></p> <p><code>/var/commerce/shipping-methods</code></p> <p><code>/var/commerce/payment-methods</code></p> </td>
  </tr>
  <tr>
   <td><strong>重构指南</strong></td>
   <td><p>您可以使用 <a href="/help/sites-deploying/lazy-content-migration.md" target="_blank">延迟迁移</a> 迁移电子商务数据的任务。</p> <p>它执行以下步骤：</p>
    <ul>
     <li>调整对旧位置的引用以指向新位置</li>
     <li>将内容从旧位置移动到新位置</li>
     <li>删除旧位置以最终激活整个系统中新位置的使用</li>
    </ul> <p>任务覆盖的位置包括：</p>
    <ul>
     <li>/etc/commerce/products</li>
     <li>/etc/commerce/collections<br /> </li>
     <li>/etc/commerce/orders<br /> </li>
     <li>/etc/commerce/payment-methods<br /> </li>
     <li>/etc/commerce/shipping-methods<br /> </li>
    </ul> <p>对于较大的目录，建议通过将以下Java系统属性传递给AEM来单独运行商务迁移任务：</p> <p><code>propertyname: com.adobe.upgrade.forcemigration</code></p> <p><code>property value: com.day.cq.compat.codeupgrade.impl.cq64.CQ64CommerceMigrationTask</code></p> <p>迁移后，AEM需要重新启动。</p> </td>
  </tr>
  <tr>
   <td><strong>注释</strong></td>
   <td>不适用<br /> </td>
  </tr>
 </tbody>
</table>
