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
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 5%

---


# 存储配置 {#storage-configuration}

存储配置是标识为社区内容选择的存储(也称为用户生成的内容(UGC))的方法。

此设置告知AEM Communities代码在访问UGC时要使用存储资源提供程序(SRP)的实现，并且必须反映部署AEM时建立的拓扑。

有关存储选项和部署拓扑的讨论，请访问：

* [社区内容商店](working-with-srp.md)
* [推荐的拓扑](topologies.md)

## 存储配置控制台{#storage-configuration-console}

![jsrp配置](assets/jsrp-configuration.png)

在创作环境中，访问存储配置控制台。

* 从全局导航中，选择&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 社区]** > **[!UICONTROL 存储配置]**

要选择默认JCR以外的存储选项：

* 选择选项
* 正确配置

   * 请参阅[选择MSRP](msrp.md#select-msrp)的详细信息
   * 请参阅[选择DSRP](dsrp.md#select-dsrp)的详细信息
   * 请参阅[选择ASRP](asrp.md#select-asrp)的详细信息

* 选择&#x200B;**[!UICONTROL 提交]**。

### 关于JCR存储{#about-jcr-storage}

请注意，如果未进行任何选择，则默认值为AEM存储库JCR。

JCR是&#x200B;*不*&#x200B;作者和发布环境共享的公用存储。 社区内容将仅在创建时的作者或发布环境中可见。

请访问[JCR商店](jsrp.md)以了解详细信息。

>[!NOTE]
>
>在`/etc/socialconfig`下缺少节点`srpc`表示默认的[ JCR存储](jsrp.md)。
