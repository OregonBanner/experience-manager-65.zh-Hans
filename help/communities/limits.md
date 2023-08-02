---
title: 成员贡献限制
description: 通过贡献限制功能，您可以限制针对垃圾邮件提供保护的贡献
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: d00a8eb2-47ce-425a-a312-f043f82912be
source-git-commit: f0dd1ac3ab9c17a8b331f5048d84ec97dd23924f
workflow-type: tm+mt
source-wordcount: '431'
ht-degree: 1%

---

# 成员贡献限制 {#member-contribution-limits}

## 概述 {#overview}

贡献限制功能允许您限制社区成员在抵御垃圾邮件方面的贡献。

当成员数量有限时，任何超出允许贡献数量的帖子都会导致超出限制的警报，并拒绝帖子。 然后，社区成员可以转到社区消息中心并联系社区管理员，后者可以在适当时删除限制。

可以从以下位置单独启用贡献限制 [成员控制台](members.md) 和/或配置为在网站访客成为新成员时自动启用。

使用“成员”控制台，社区管理员可随时主动为成员删除贡献限制，或者在成员向发出此类请求的社区管理员发送消息时，主动删除贡献限制。

## AEM Communities用户生成的内容贡献限制配置 {#aem-communities-user-generated-content-contribution-limits-configuration}

此OSGi配置：

* 定义缴款限制的特征（一段时间内员额数）。
* 标识当达到限制时能够发送消息的成员。
* 标识永远不需要限制的域。

要访问此OSGi配置，请执行以下操作：

* 在主发布服务器上：
* 使用管理员权限登录。
* 访问 [Web控制台](../../help/sites-deploying/configuring-osgi.md).

   * 例如， [http://localhost:4503/system/console/configMgr](http://localhost:4503/system/console/configMgr)

* 定位 `AEM Communities User Generated Content Contribution Limits Configuration`.
* 选择编辑图标。

![configure-limits](assets/configure-limits.png)

* **[!UICONTROL 自动应用UGC贡献限制]**

  如果选中，则在用户注册为社区成员时自动设置贡献限制。 这反映在社区成员的配置文件中，并可从中启用/禁用 [成员控制台](members.md). 拥有域允许列表电子邮件地址的新成员从不受到限制。

  默认值为未选中。

* **[!UICONTROL UGC限制]**

  最大贡献数量。

  默认为十个帖子。

* **[!UICONTROL UGC限制频率]**

  限制UGC限制的时间段。

  默认值为60分钟。

* **[!UICONTROL 域]**

  一个或多个电子邮件域的允许列表列表。 选择+图标可添加其他条目。

  当自动应用UGC贡献限制时，域允许列表中具有电子邮件地址的用户不受影响。 例如，如果域 `mycompany.com` 添加到域列表，然后添加具有电子邮件地址的成员 `me@mycompany.com` 不受限制地发帖。

  默认值为空允许列表。

* **[!UICONTROL 消息收件人]**

  成员的一个或多个可授权ID列表，这些ID可修改成员的贡献限制。 选择+图标可添加其他条目。

  成员只能在达到其限制时联系指定的成员。

  默认为无消息收件人。

注意：默认配置导致在1小时内的时间段内限制10个帖子。
