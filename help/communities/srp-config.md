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
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 存储配置 {#storage-configuration}

存储配置是标识为社区内容(也称为用户生成的内容(UGC))选择的存储的方法。

此设置会通知AEM Communities代码，在访问UGC时将使用存储资源提供者(SRP)的实现，并且必须反映部署AEM时建立的拓扑。

有关存储选项和部署拓扑的讨论，请访问

* [社区内容商店](working-with-srp.md)
* [推荐的拓扑](topologies.md)

## 存储配置控制台 {#storage-configuration-console}

![chlimage_1-188](assets/chlimage_1-188.png)

在创作环境中，要访问存储配置控制台

* 从全局导航：“工 **[!UICONTROL 具”>“社区”>“存储配置”]**

要选择默认JCR以外的存储选项，请执行以下操作：

* 选择选项
* 正确配置

   * 查看有关选择MSRP的 [详细信息](msrp.md#select-msrp)
   * 查看有关选择DSRP的 [详细信息](dsrp.md#select-dsrp)
   * 查看有关选择ASRP [的详细信息](asrp.md#select-asrp)

* Select **[!UICONTROL Submit]**

### 关于JCR存储 {#about-jcr-storage}

请注意，如果未进行任何选择，则默认值为AEM存储库JCR。

JCR不是 *作者和发布环境* 共享的公用存储。 社区内容仅在创建时所在的创作或发布环境中可见。

请访 [问JCR商店](jsrp.md) ，以了解更多信息。

>[!NOTE]
>
>缺少下方的节 `srpc`点 `/etc/socialconfig` 表示默认 [JCR存储](jsrp.md)。

