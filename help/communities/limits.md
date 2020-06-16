---
title: 会员缴费限制
seo-title: 会员缴费限制
description: 贡献限制功能允许您限制贡献以防垃圾邮件
seo-description: 贡献限制功能允许您限制贡献以防垃圾邮件
uuid: 99b2a855-3f0d-41a0-9572-517a7f29af9f
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: d855aac2-f34d-402f-9dc3-c7ad494b45f2
translation-type: tm+mt
source-git-commit: df59879cfa6b0bc7eba13f679e833fabbcbe92f2
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 1%

---


# 会员缴费限制 {#member-contribution-limits}

## 概述 {#overview}

贡献限制功能允许限制社区成员的贡献作为防止垃圾邮件的一种手段。

如果会员人数有限，任何超出允许的缴费数量的员额都将发出警报，提示超出限额，并拒绝该员额。 然后，社区成员可以转到社区消息中心并与社区经理联系，后者可以在适当时取消限制。

贡献限制可以从成员控制台 [单独启用](members.md) ，和／或配置为在站点访客成为新成员时自动启用。

使用“成员”控制台，社区管理者可以随时主动删除某个成员的贡献限制，或者在成员向提出此类请求的社区管理者发送消息时主动删除该成员。

## AEM Communities用户生成的内容贡献限制配置 {#aem-communities-user-generated-content-contribution-limits-configuration}

此OSGi配置：

* 界定缴款限额的特点（一个时期内的员额数）。
* 标识当达到限制时成员能够发送消息的用户。
* 标识永远不需要约束的域。

要访问此OSGi配置：

* 在主发布者上：
* 以管理员权限登录。
* 访问 [Web控制台](../../help/sites-deploying/configuring-osgi.md)。

   * 例如， [http://localhost:4503/system/console/configMgr](http://localhost:4503/system/console/configMgr)

* 找到 `AEM Communities User Generated Content Contribution Limits Configuration`。
* 选择编辑图标。

![chlimage_1-127](assets/chlimage_1-127.png)

* **[!UICONTROL 自动应用UGC贡献限制]**

   如果选中此项，则在用户注册为社区成员时自动设置缴费限制。 这反映在社区成员的用户档案中，并可从成员控制台中启用/ [禁用](members.md)。 具有域允许列表中电子邮件地址的新成员从不受限。

   默认为未选中。

* **[!UICONTROL UGC限制]**

   最大捐款数。

   默认为10个帖子。

* **[!UICONTROL UGC限制频率]**

   限制UGC限制的时间段。

   默认为60分钟。

* **[!UICONTROL 域]**

   一个或多个电子邮件域的allowlist列表。 选择+图标以添加其他条目。

   在自动应用UGC贡献限制时，在域的允许列表中具有电子邮件地址的用户不受影响。 例如，如果将域 `mycompany.com` 添加到域的列表，则始终不限制具有电子邮件地址 `me@mycompany.com` 的成员进行发布。

   默认为空allowlist。

* **[!UICONTROL 消息传递收件人]**

   列表能够修改成员贡献限制的成员的一个或多个可授权ID。 选择+图标以添加其他条目。

   成员只有在达到其限制后才能与指定成员联系。

   默认值不是消息收件人。

注意： 默认配置在1小时内限制10个帖子。
