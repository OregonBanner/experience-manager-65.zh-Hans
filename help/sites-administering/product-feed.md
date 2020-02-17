---
title: 产品信息源
seo-title: 产品信息源
description: 了解AEM产品源。
seo-description: 了解AEM产品源。
uuid: 99eb9bdc-2717-45d4-9203-6394b7d7ddc6
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 1f920892-c52e-42ca-900c-2c7ab3c503b3
translation-type: tm+mt
source-git-commit: 1c1ade947f2cbd26b35920cfd10b1666b132bcbd

---


# Product Feed {#product-feed}

AEM与 [Search&amp;Promote集成](https://www.adobe.com/solutions/testing-targeting/searchandpromote.html) ，允许您：

* 使用独立于基础存储库结构和商务平台的eCommerce API。
* 利用Search&amp;Promote的Index Connector功能以XML格式提供产品源。
* 利用Search&amp;Promote的远程控制功能执行产品源的按需或计划请求
* 不同Search&amp;Promote帐户的源生成，配置为云服务配置。

您需要有一个有效的帐户并配 [置与Search&amp;Promote的连接](/help/sites-administering/search-and-promote.md#configuring-the-connection-to-search-promote)。 您还必须验证您使用的是正确的 [数据中心](/help/sites-administering/search-and-promote.md#configuring-the-data-center) ，并确保已配置**远程服务器URI **。

## 设置产品源 {#set-up-the-product-feed}

您首先必须输入Web站点根目录和标识符属性。 要执行此操作：

1. 导航到您的Search&amp;Promote配置。
1. 单击&#x200B;**[!UICONTROL 编辑]**。
1. 单击“索 **[!UICONTROL 引连接器源配置]** ”选项卡。
1. 输入 **[!UICONTROL Web站点根目录和]** “标 **[!UICONTROL 识符”属性]**。

   >[!NOTE]
   >
   >例 **[!UICONTROL 如]** ，网站根目录是电子商务网站的根目录 `/content/geometrixx-outdoors/en`。
   >
   >“标 **[!UICONTROL 识符]** ”属性是可唯一标识产品的JCR属性： `identifier`.

1. 单击&#x200B;**[!UICONTROL 确定]**。

然后，您还必须在Web控制台中编辑两个配置，然后才能生成产品源。

### 为Geometrixx配置Day CQ Search&amp;Promote产品Crawler实施 {#configuring-the-day-cq-search-promote-products-crawler-implementation-for-geometrixx}

1. 导航到 [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr)。
1. 单击 **[!UICONTROL Day CQ Search&amp;Promote products crawler implementation for Geometrixx]**。
1. 指定此Crawler所链接的Search&amp;Promote帐号。 它将用于查找此Crawler使用的云服务配置。
1. 单击&#x200B;**[!UICONTROL 保存]**。

### 为Geometrixx配置Day CQ Search&amp;Promote产品Feed Generator {#configuring-the-day-cq-search-promote-products-feed-generator-for-geometrixx}

1. 导航到 [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr)。
1. 单击 **[!UICONTROL Day CQ Search&amp;Promote products feed generator for Geometrixx]**。
1. 指定此生成器所链接的Search&amp;Promote帐号。 它将用于查找此生成器使用的云服务配置。
1. 单击&#x200B;**[!UICONTROL 保存]**。

## 计划产品源 {#schedule-the-product-feed}

要启用计划的源生成，必须为其配置调度程序。
将调度程序配置为特定Search&amp;Promote云服务配置的子配置。

1. 导航到您的Search&amp;Promote配置。
1. 单击“ **[!UICONTROL 调度程]** 序配置” **[!UICONTROL 旁边的+]**。
1. 输入页 **[!UICONTROL 面作者]** 、可识别的标题和唯一 **[!UICONTROL 名称]**。
1. 单击&#x200B;**[!UICONTROL 创建]**。此时将打开一个对话框。

   ![chlimage_1-108](assets/chlimage_1-108a.png)

1. 输入“ **[!UICONTROL Remote Control Password”]**。 这是您在Search&amp;Pronote帐户中配置的密码。

   >[!NOTE]
   >
   >这不是Search&amp;Promote帐户的口令。 您可以通过登录Search&amp;Promote帐户并转到Index **[!UICONTROL ，然后转到Remote]** Control来查找和更改此密码 ****。

1. 选中 **[!UICONTROL 启用计划]** 框。
1. 选择计 **[!UICONTROL 划]**。 它是实际的供给生成计划。
1. 是否启 **[!UICONTROL 用按需索引]** 。 此功能用于手动调用Search&amp;Promote索引。 如果 **[!UICONTROL 选中“请求完整产品源]** ”，则Search&amp;Promote将请求完整产品源。 否则，请求增量产品供给。

   >[!NOTE]
   >
   >点播索引功能利用了Search&amp;Promote的“遥控”功能。 调用远程索引时，索引不会立即启动，但是使用远程控制功能将索引请求发布到Search&amp;Promote。

1. 单击&#x200B;**[!UICONTROL 确定]**。

现在，您已配置了所有内容，可以看到一个XML页面，其中包含所配置网站根目录下的所有产品： [http://localhost:4502/etc/commerce/searchpromote/feed/full](http://localhost:4502/etc/commerce/searchpromote/feed/full)。
