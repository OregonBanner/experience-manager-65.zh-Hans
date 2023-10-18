---
title: 存储配置
description: 了解Storage Configuration Console ，它作为一种标识为社区内容（也称为用户生成的内容）选择的存储的方法。
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: 67de7e26-3f93-4034-9e3a-5c127f7447bc
source-git-commit: 00b6f2f03470aca7f87717818d0dfcd17ac16bed
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 4%

---

# 存储配置 {#storage-configuration}

存储配置是标识为社区内容(也称为用户生成内容(UGC))选择的存储的方法。

此设置会通知AEM Communities代码，在访问UGC时使用了存储资源提供程序(SRP)的实现。 它必须反映部署Adobe Experience Manager (AEM)时建立的拓扑。

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

* 选择&#x200B;**[!UICONTROL 提交]**。

### 关于JCR存储 {#about-jcr-storage}

如果未进行任何选择，则默认为AEM存储库JCR。

JCR为 *非* 作者和发布环境共享的公用存储。 社区内容仅在创建该内容的创作或发布环境中可见。

访问 [JCR存储](jsrp.md) 以了解其他信息。

>[!NOTE]
>
>节点不存在 `srpc` 下 `/etc/socialconfig` 指示默认值 [JCR存储](jsrp.md).
