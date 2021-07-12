---
title: 会员缴费限制
seo-title: 会员缴费限制
description: 贡献限制功能允许您限制贡献内容以抵御垃圾邮件
seo-description: 贡献限制功能允许您限制贡献内容以抵御垃圾邮件
uuid: 99b2a855-3f0d-41a0-9572-517a7f29af9f
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: d855aac2-f34d-402f-9dc3-c7ad494b45f2
role: Admin
exl-id: d00a8eb2-47ce-425a-a312-f043f82912be
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 1%

---

# 会员缴费限制 {#member-contribution-limits}

## 概述 {#overview}

贡献限制功能提供了限制社区成员贡献的功能，以此来防止垃圾邮件。

当成员受到限制时，任何超过允许的贡献数量的帖子都将导致警报超出限制并拒绝该帖子。 然后，社区成员可以前往社区消息中心，并联系社区经理，该经理可以在适当时取消限制。

贡献限制可以从[成员控制台](members.md)单独启用，和/或配置为当站点访客成为新成员时自动启用。

使用“成员”控制台，社区管理员可以随时主动删除成员的贡献限制，或者在成员向提出此类请求的社区管理员发送消息时主动删除贡献限制。

## AEM Communities用户生成的内容贡献限制配置 {#aem-communities-user-generated-content-contribution-limits-configuration}

此OSGi配置：

* 界定缴款限额的特点（一个时期内的员额数）。
* 确定当达到限制时，成员能够向谁发送消息。
* 标识不需要受到约束的域。

要访问此OSGi配置，请执行以下操作：

* 在主发布者上：
* 使用管理员权限登录。
* 访问[Web控制台](../../help/sites-deploying/configuring-osgi.md)。

   * 例如， [http://localhost:4503/system/console/configMgr](http://localhost:4503/system/console/configMgr)

* 找到`AEM Communities User Generated Content Contribution Limits Configuration`。
* 选择编辑图标。

![配置限制](assets/configure-limits.png)

* **[!UICONTROL 自动应用UGC贡献限制]**

   如果选中此选项，则在用户注册为社区成员时自动为其设置贡献限制。 这反映在社区成员的配置文件中，并可以从[成员控制台](members.md)启用/禁用。 具有域中电子邮件地址的新成允许列表员从不会受到限制。

   默认为未选中。

* **[!UICONTROL UGC限制]**

   贡献的最大数量。

   默认为10个帖子。

* **[!UICONTROL UGC限制频率]**

   限制UGC限制的时间段。

   默认值为60分钟。

* **[!UICONTROL 域]**

   一个允许列表或多个电子邮件域的列表。 选择+图标以进行其他条目。

   自动应用UGC贡献限允许列表制时，在域名中具有电子邮件地址的用户不会受到影响。 例如，如果域`mycompany.com`被添加到域列表，则电子邮件地址为`me@mycompany.com`的成员永远不会被限制发布。

   默认为空允许列表。

* **[!UICONTROL 消息传送收件人]**

   能够修改成员贡献限制的一个或多个可授权成员ID的列表。 选择+图标以进行其他条目。

   成员只有在达到其限制时才能与指定成员联系。

   默认为没有消息传送收件人。

注意：默认配置在1小时内限制10个帖子。
