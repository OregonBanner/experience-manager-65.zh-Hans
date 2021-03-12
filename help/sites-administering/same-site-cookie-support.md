---
title: 对AEM 6.5的相同站点Cookie支持
description: 对AEM 6.5的相同站点Cookie支持
topic-tags: security
translation-type: tm+mt
source-git-commit: ac2f3d69fd20d7779120a194c698d6f0dd6e6a84
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 0%

---


# 对AEM 6.5 {#same-site-cookie-support-for-aem-65}的相同站点Cookie支持

自版本80、Chrome和更高版本的Safari推出了Cookie安全的新模型。 此模式旨在通过名为`SameSite`的设置对Cookie向第三方站点的可用性引入安全控制。 有关详细信息，请参阅此[文章](https://web.dev/samesite-cookies-explained/)。

此设置(`SameSite=Lax`)的默认值可能导致AEM实例或服务之间的身份验证不工作。 这是因为这些服务的域或URL结构可能不受此Cookie策略的约束。

为了避免这种情况，您需要将登录令牌的SameSite cookieattribue设置为`None`。

您可以按照以下步骤操作：

1. 转到位于`http://serveraddress:serverport/system/console/configMgr`的Web控制台
1. 搜索并单击&#x200B;**AdobeGranite令牌身份验证处理程序**
1. 如下图所示，将登录令牌cookie **的** SameSite属性设置为`None`
   ![samesite](assets/samesite1.png)
1. 单击“保存”
1. 更新此设置后，用户将重新注销并登录，`login-token` cookie将设置`None`属性，并将包含在跨站点请求中。
