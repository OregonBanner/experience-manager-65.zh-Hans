---
title: JSRP - JCR存储资源提供程序
seo-title: JSRP - JCR存储资源提供程序
description: JSRP通常最适合用于一个发布实例和一个作者实例的演示或开发环境
seo-description: JSRP通常最适合用于一个发布实例和一个作者实例的演示或开发环境
uuid: 358a43c1-4137-4300-8443-c0d7166968ad
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: f5316a73-84e2-4a18-98c1-a384eeaa77cf
role: Administrator
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '463'
ht-degree: 0%

---


# JSRP - JCR存储资源提供程序{#jsrp-jcr-storage-resource-provider}

## 关于JSRP {#about-jsrp}

当AEM Communities使用JSRP作为其存储选项（默认）时，社区内容存储在JCR中，用户生成的内容(UGC)只能从发布它的作者或发布实例访问。

由于部署的简单性，JSRP通常最适合用于一个发布实例和一个作者实例的演示或开发环境。

另请参阅[SRP选项的特性](working-with-srp.md#characteristics-of-srp-options)和[推荐拓扑](topologies.md)。

## 配置 {#configuration}

### 选择JSRP {#select-jsrp}

默认情况下，JSRP是UGC的存储选项。

[存储配置控制台](srp-config.md)允许选择默认存储配置，该配置标识要使用的SRP实现。

在创作环境中，要访问存储配置控制台

* 从全局导航：**[!UICONTROL 工具]** > **[!UICONTROL 社区]** > **[!UICONTROL 存储配置]**

* 选择&#x200B;**[!UICONTROL JCR存储资源提供程序(JSRP)]**

* 选择&#x200B;**[!UICONTROL 提交]**

![jsrp-configuration](assets/jsrp-configuration.png)

### 发布配置{#publishing-the-configuration}

虽然JSRP是默认配置，但要确保在发布环境中设置相同的配置：

* 从全局导航：**[!UICONTROL 工具]** > **[!UICONTROL 部署]** > **[!UICONTROL 复制]**
* 选择&#x200B;**[!UICONTROL 激活树]** > **[!UICONTROL 开始路径]**:

   * 浏览到`/conf/global/settings/community/srpc/`

* 选择&#x200B;**[!UICONTROL 激活]**

## 管理用户数据{#managing-user-data}

有关&#x200B;*用户*、*用户用户档案*&#x200B;和&#x200B;*用户组*&#x200B;的信息，请访问：

* [用户同步](sync.md)
* [管理用户和用户组](users.md)

## 疑难解答 {#troubleshooting}

### UGC在JCR {#ugc-not-visible-in-jcr}中不可见

通过检查存储选项的配置，确保JSRP已配置为默认提供程序。 默认情况下，存储资源提供程序为JSRP。

在所有创作和发布AEM实例上，重新访问存储配置控制台或检查AEM存储库：

* 在JCR中，如果[/conf/global/settings/community](http://localhost:4502/crx/de/index.jsp#/conf/global/settings/community)

   * 不包含[srpc](http://localhost:4502/crx/de/index.jsp#/conf/global/settings/community/srpc)节点，它表示存储提供程序是JSRP。
   * 如果srpc节点存在并包含节点[defaultconfiguration](http://localhost:4502/crx/de/index.jsp#/conf/global/settings/community/srpc/defaultconfiguration)，则defaultconfiguration的属性应将JSRP定义为默认提供程序。

### UGC在创作实例{#ugc-not-visible-on-author-instance}上不可见

这不是错误。 JSRP的一个特点是，在发布环境中输入的社区内容仅在发布环境中可见。

### UGC在发布实例{#ugc-not-visible-on-publish-instance}上不可见

如果部署了单个发布实例或发布群集，则按照[UGC Not Visible in JCR](#ugc-not-visible-in-jcr)的说明操作。

如果部署了发布场，JSRP的一个特点是社区内容将仅在发布到的发布实例上可见。

要使UGC在任何发布实例中都可见，需要发布群集。
