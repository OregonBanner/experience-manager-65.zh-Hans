---
title: 对AEM 6.5的相同网站Cookie支持
description: 对AEM 6.5的相同网站Cookie支持
topic-tags: security
exl-id: e1616385-0855-4f70-b787-b01701929bbc
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 0%

---

# 对AEM 6.5 {#same-site-cookie-support-for-aem-65}的相同站点Cookie支持

自版本80、Chrome及更高版本的Safari以来，为Cookie安全引入了新模型。 此模式旨在通过名为`SameSite`的设置，对Cookie向第三方站点的可用性引入安全控制。 有关更多详细信息，请参阅此[文章](https://web.dev/samesite-cookies-explained/)。

此设置的默认值(`SameSite=Lax`)可能会导致AEM实例或服务之间的身份验证无法工作。 这是因为这些服务的域或URL结构可能不受此Cookie策略的约束。

要解决此问题，您需要将登录令牌的SameSite Cookieattribe设置为`None`。

您可以按照以下步骤执行操作：

1. 转到位于`http://serveraddress:serverport/system/console/configMgr`的Web控制台
1. 搜索并单击&#x200B;**AdobeGranite令牌身份验证处理程序**
1. 将登录令牌Cookie **的** SameSite属性设置为`None`，如下图所示
   ![samesite](assets/samesite1.png)
1. 单击Save
1. 更新此设置后，用户将注销并再次登录， `login-token` Cookie将设置`None`属性，并将包含在跨站点请求中。
