---
title: 成员缴款限制
seo-title: Member Contribution Limits
description: 通过贡献限制功能，您可以限制抵御垃圾邮件的贡献
seo-description: Contribution limits feature lets you limit the contributions to protect against spam
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
source-wordcount: '434'
ht-degree: 1%

---

# 成员缴款限制 {#member-contribution-limits}

## 概述 {#overview}

贡献限制功能提供了限制社区成员贡献的功能，作为抵御垃圾邮件的一种方法。

当成员受限时，任何超出允许贡献数量的帖子都将导致超出限制的警报，并拒绝帖子。 随后，社区成员可以转到社区消息中心并联系社区经理，后者可以在适当时删除限制。

贡献限制可以从 [成员控制台](members.md) 和/或配置为在网站访客成为新成员时自动启用。

使用“成员”控制台，社区管理员可以随时主动为成员删除贡献限制，或者在成员向发出此类请求的社区管理员发送消息时被动删除贡献限制。

## AEM Communities用户生成的内容贡献限制配置 {#aem-communities-user-generated-content-contribution-limits-configuration}

此OSGi配置：

* 定义缴款限制的特征（一个时期内的员额数）。
* 标识当达到限制时能够发送消息的成员。
* 标识永远不需要限制的域。

要访问此OSGi配置，请执行以下操作：

* 在主发布服务器上：
* 使用管理员权限登录。
* 访问 [Web控制台](../../help/sites-deploying/configuring-osgi.md).

   * 例如， [http://localhost:4503/system/console/configMgr](http://localhost:4503/system/console/configMgr)

* 查找 `AEM Communities User Generated Content Contribution Limits Configuration`.
* 选择编辑图标。

![configure-limits](assets/configure-limits.png)

* **[!UICONTROL 自动应用UGC贡献限制]**

   如果选中，则在用户注册为社区成员时自动设置贡献限制。 这反映在社区成员的配置文件中，并可从启用/禁用 [成员控制台](members.md). 拥有域允许列表电子邮件地址的新成员绝不受限制。

   默认值为未选中。

* **[!UICONTROL UGC限制]**

   最大贡献数量。

   默认值为10个帖子。

* **[!UICONTROL UGC限制频率]**

   限制UGC限制的时间段。

   默认值为60分钟。

* **[!UICONTROL 域]**

   一个或多个电子邮件域的允许列表列表。 选择+图标可生成其他条目。

   当自动应用UGC贡献限制时，域允许列表中具有电子邮件地址的用户不受影响。 例如，如果域 `mycompany.com` 添加到域列表，然后添加具有电子邮件地址的成员 `me@mycompany.com` 从未被限制过发帖。

   默认值为空允许列表。

* **[!UICONTROL 消息收件人]**

   成员的一个或多个可授权ID的列表，这些ID能够修改成员的贡献限制。 选择+图标可生成其他条目。

   成员只能在达到其限制时联系指定的成员。

   默认为无消息收件人。

注意：默认配置导致在1小时内的限制为10个帖子。
