---
title: 存储配置
seo-title: 存储配置
description: 如何访问存储配置控制台
seo-description: 如何访问存储配置控制台
uuid: 6a5a71d5-6aaa-4635-8852-4dae33c497a9
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 71fac7e9-814a-48b5-b816-9bdcb2a05190
translation-type: tm+mt
source-git-commit: 3296db289b2e2f4ca0d1981597ada6ca1310bd46

---


# 存储配置 {#storage-configuration}

存储配置是标识为社区内容选择的存储(也称为用户生成的内容(UGC))的方法。

此设置会通知AEM Communities代码，在访问UGC时将使用存储资源提供者(SRP)的实现，并且必须反映部署AEM时建立的拓扑。

有关存储选项和部署拓扑的讨论，请访问：

* [社区内容商店](working-with-srp.md)
* [推荐的拓扑](topologies.md)

## 存储配置控制台 {#storage-configuration-console}

![chlimage_1-188](assets/chlimage_1-188.png)

在创作环境中，要访问存储配置控制台。

* 从全局导航中，选择“工 **[!UICONTROL 具]** ”>“ **[!UICONTROL 社区]** ” **[!UICONTROL >“存储配置”]**

要选择默认JCR以外的存储选项，请执行以下操作：

* 选择选项
* 正确配置

   * 查看有关选择MSRP的 [详细信息](msrp.md#select-msrp)
   * 查看有关选择DSRP的 [详细信息](dsrp.md#select-dsrp)
   * 查看有关选择ASRP [的详细信息](asrp.md#select-asrp)

* 选择&#x200B;**[!UICONTROL 提交]**。

### 关于JCR存储 {#about-jcr-storage}

请注意，如果未进行任何选择，则默认值为AEM存储库JCR。

JCR不是 *作者* 和发布环境共享的公用商店。 社区内容仅在创建时所在的创作或发布环境中可见。

请访 [问JCR商店](jsrp.md) ，以了解更多信息。

>[!NOTE]
>
>缺少下方的节 `srpc` 点 `/etc/socialconfig` 表示默认 [JCR存储](jsrp.md)。


