---
title: 存储配置
seo-title: Storage Configuration
description: 如何访问存储配置控制台
seo-description: How to access the Storage Configuration Console
uuid: 6a5a71d5-6aaa-4635-8852-4dae33c497a9
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 71fac7e9-814a-48b5-b816-9bdcb2a05190
role: Admin
exl-id: 67de7e26-3f93-4034-9e3a-5c127f7447bc
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '199'
ht-degree: 3%

---

# 存储配置 {#storage-configuration}

存储配置是标识为社区内容(也称为用户生成内容(UGC))选择的存储的方法。

此设置会通知AEM Communities代码，在访问UGC时将使用存储资源提供程序(SRP)的哪个实现，并且必须反映在部署AEM时建立的拓扑。

有关存储选项和部署拓扑的讨论，请访问：

* [社区内容存储](working-with-srp.md)
* [推荐的拓扑](topologies.md)

## 存储配置控制台 {#storage-configuration-console}

![jsrp配置](assets/jsrp-configuration.png)

在创作环境中，访问存储配置控制台。

* 在全局导航中，选择 **[!UICONTROL 工具]** > **[!UICONTROL Communities]** > **[!UICONTROL 存储配置]**

要选择默认JCR以外的存储选项，请执行以下操作：

* 选择选项
* 正确配置

   * 查看详细信息 [选择MSRP](msrp.md#select-msrp)
   * 查看详细信息 [选择DSRP](dsrp.md#select-dsrp)
   * 查看详细信息 [选择ASRP](asrp.md#select-asrp)

* 选择 **[!UICONTROL 提交]**.

### 关于JCR存储 {#about-jcr-storage}

请注意，如果未进行任何选择，则默认为AEM存储库JCR。

JCR是 *非* 作者和发布环境共享的公用存储。 社区内容将仅从创建它的创作或发布环境中可见。

访问 [JCR存储](jsrp.md) 以获取其他信息。

>[!NOTE]
>
>节点不存在 `srpc` 下 `/etc/socialconfig` 指示默认值 [JCR存储](jsrp.md).
