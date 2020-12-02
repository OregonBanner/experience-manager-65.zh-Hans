---
title: 产品信息源
seo-title: 产品信息源
description: 了解AEM产品信息源。
seo-description: 了解AEM产品信息源。
uuid: 99eb9bdc-2717-45d4-9203-6394b7d7ddc6
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 1f920892-c52e-42ca-900c-2c7ab3c503b3
translation-type: tm+mt
source-git-commit: 1c1ade947f2cbd26b35920cfd10b1666b132bcbd
workflow-type: tm+mt
source-wordcount: '584'
ht-degree: 4%

---


# 产品源{#product-feed}

AEM与[Search&amp;Promote](https://www.adobe.com/solutions/testing-targeting/searchandpromote.html)集成，并允许您：

* 使用独立于基础存储库结构和商务平台的eCommerce API。
* 利用Search&amp;Promote的索引连接器功能以XML格式提供产品源。
* 利用Search&amp;Promote的远程控制功能执行产品源的按需或计划请求
* 不同Search&amp;Promote帐户的源生成，配置为云服务配置。

您需要有有效帐户并配置到Search&amp;Promote[的连接。 ](/help/sites-administering/search-and-promote.md#configuring-the-connection-to-search-promote)您还必须验证您使用的[数据中心](/help/sites-administering/search-and-promote.md#configuring-the-data-center)是否正确，并确保已配置**远程服务器URI **。

## 设置产品源{#set-up-the-product-feed}

您首先必须输入网站根目录和标识符属性。 要执行此操作：

1. 导航到您的Search&amp;Promote配置。
1. 单击&#x200B;**[!UICONTROL 编辑]**。
1. 单击&#x200B;**[!UICONTROL 索引连接器源配置]**&#x200B;选项卡。
1. 输入&#x200B;**[!UICONTROL 网站根]**&#x200B;和&#x200B;**[!UICONTROL 标识符属性]**。

   >[!NOTE]
   >
   >**[!UICONTROL 网站根]**&#x200B;是电子商务网站的根，例如`/content/geometrixx-outdoors/en`。
   >
   >**[!UICONTROL Identifier属性]**&#x200B;是可唯一标识产品的JCR属性：`identifier`。

1. 单击&#x200B;**[!UICONTROL 确定]**。

然后，您还必须在Web控制台中编辑两个配置，然后才能生成产品源。

### 为Geometrixx{#configuring-the-day-cq-search-promote-products-crawler-implementation-for-geometrixx}配置Day CQSearch&amp;Promote产品Crawler实施

1. 导航到[http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr)。
1. 单击&#x200B;**[!UICONTROL Day CQSearch&amp;Promote产品Crawler实现，以获取Geometrixx]**。
1. 指定此Crawler所链接的Search&amp;Promote帐号。 它将用于查找此Crawler使用的云服务配置。
1. 单击&#x200B;**[!UICONTROL 保存]**。

### 为Geometrixx{#configuring-the-day-cq-search-promote-products-feed-generator-for-geometrixx}配置Day CQSearch&amp;Promote产品供给生成器

1. 导航到[http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr)。
1. 单击&#x200B;**[!UICONTROL Day CQSearch&amp;Promote产品供给生成器，Geometrixx]**。
1. 指定此生成器所链接的Search&amp;Promote帐号。 它将用于查找此生成器使用的云服务配置。
1. 单击&#x200B;**[!UICONTROL 保存]**。

## 计划产品源{#schedule-the-product-feed}

要启用计划的源生成，必须为它配置调度程序。
调度程序配置为特定Search&amp;Promote云服务配置的子配置。

1. 导航到您的Search&amp;Promote配置。
1. 单击&#x200B;**[!UICONTROL 调度程序配置]**&#x200B;旁边的&#x200B;**[!UICONTROL +]**。
1. 输入页面作者可识别的&#x200B;**[!UICONTROL 标题]**&#x200B;和唯一的&#x200B;**[!UICONTROL 名称]**。
1. 单击&#x200B;**[!UICONTROL 创建]**。将打开一个对话框。

   ![chlimage_1-108](assets/chlimage_1-108a.png)

1. 输入&#x200B;**[!UICONTROL 远程控制密码]**。 它是您在Search&amp;Pronote帐户中配置的密码。

   >[!NOTE]
   >
   >这不是您的Search&amp;Promote帐户的密码。 您可以通过登录您的Search&amp;Promote帐户并转到&#x200B;**[!UICONTROL 索引]**，然后转到&#x200B;**[!UICONTROL 远程控制]**&#x200B;来查找和更改此密码。

1. 选中&#x200B;**[!UICONTROL 启用计划]**&#x200B;框。
1. 选择&#x200B;**[!UICONTROL 计划]**。 它是实际的馈源生成计划。
1. 启用或不启用&#x200B;**[!UICONTROL 按需索引。]**&#x200B;此功能用于手动调用Search&amp;Promote索引。 如果选中“请求完整产品源&#x200B;**[!UICONTROL ”,Search&amp;Promote将请求完整产品源。]**&#x200B;否则，请求增量产品源。

   >[!NOTE]
   >
   >点播索引功能利用了Search&amp;Promote的远程控制功能。 调用远程索引时，索引不会立即开始，但将使用远程控制功能向Search&amp;Promote发布索引请求。

1. 单击&#x200B;**[!UICONTROL 确定]**。

现在，您已配置了所有内容，所以您可以看到一个XML页面，其中包含所配置网站根目录下的所有产品：[http://localhost:4502/etc/commerce/searchpromote/feed/full](http://localhost:4502/etc/commerce/searchpromote/feed/full)。
