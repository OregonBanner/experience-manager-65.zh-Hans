---
title: 会员供款限制
seo-title: 会员供款限制
description: 贡献限制功能允许您限制贡献以防垃圾邮件
seo-description: 贡献限制功能允许您限制贡献以防垃圾邮件
uuid: 99b2a855-3f0d-41a0-9572-517a7f29af9f
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: d855aac2-f34d-402f-9dc3-c7ad494b45f2
role: Administrator
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 1%

---


# 成员贡献限制{#member-contribution-limits}

## 概述 {#overview}

贡献限制功能提供了限制社区成员贡献的能力，作为防止垃圾邮件的一种手段。

如果会员人数有限，任何超出允许的缴费数量的帖子都会发出警报，提示已超出限额，并拒绝该帖子。 然后，社区成员可以访问社区消息中心并与社区经理联系，后者可以在适当时取消限制。

贡献限制可以从[成员控制台](members.md)单独启用，和/或配置为在站点访客成为新成员时自动启用。

使用“成员”控制台，社区管理者可以随时主动删除某个成员的贡献限制，或者在成员向提出此类请求的社区管理者发送消息时主动删除。

## AEM Communities用户生成的内容贡献限制配置{#aem-communities-user-generated-content-contribution-limits-configuration}

此OSGi配置：

* 界定捐款限额的特点（一个时期内的员额数）。
* 标识当达到限制时成员能够向谁发送消息。
* 标识无需受限的域。

要访问此OSGi配置：

* 在主发行商上：
* 使用管理员权限登录。
* 访问[Web控制台](../../help/sites-deploying/configuring-osgi.md)。

   * 例如，[http://localhost:4503/system/console/configMgr](http://localhost:4503/system/console/configMgr)

* 找到`AEM Communities User Generated Content Contribution Limits Configuration`。
* 选择编辑图标。

![配置限制](assets/configure-limits.png)

* **[!UICONTROL 自动应用UGC贡献限制]**

   如果选中此项，则在用户注册为社区成员时自动设置供款限制。 这反映在社区成员的用户档案中，并可从[成员控制台](members.md)中启用/禁用。 具有来自一域的电子邮允许列表件地址的新成员从不受限。

   默认为未选中。

* **[!UICONTROL UGC限制]**

   最大捐款数。

   默认为10个帖子。

* **[!UICONTROL UGC限制频率]**

   限制UGC限制的时间段。

   默认为60分钟。

* **[!UICONTROL 域]**

   一个允许列表或多个电子邮件域的列表。 选择+图标以添加其他条目。

   在自动应用UGC贡献限允许列表制时，在域管理中具有电子邮件地址的用户不受影响。 例如，如果将域`mycompany.com`添加到域的列表，则电子邮件地址为`me@mycompany.com`的成员从不限制发布。

   默认为空允许列表。

* **[!UICONTROL 消息收件人]**

   列表一个或多个可授权的ID，成员可以修改成员的贡献限制。 选择+图标以添加其他条目。

   成员只有在达到其限制时才能与指定成员联系。

   默认不是消息收件人。

注意：默认配置在一小时内限制为10个帖子。
