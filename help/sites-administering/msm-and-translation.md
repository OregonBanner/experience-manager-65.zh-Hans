---
title: 网站管理
seo-title: 网站管理
description: 了解如何在AEM中管理多语言网站。
seo-description: 了解如何在AEM中管理多语言网站。
uuid: a32d458b-a5ad-46ef-a68c-4717c63b4bdd
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: fabaa3e8-1657-4ed4-abb2-990117bec39c
exl-id: 8f11f5de-f5af-4ce7-a448-2b4299de2930
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '351'
ht-degree: 2%

---

# 网站管理{#website-administration}

以下管理工具可用于管理网站和页面：

* 多站点管理器(MSM)允许您在多个位置使用相同的站点内容，同时允许进行以下变量：

   * [重用内容：多站点管理器和Live Copy](/help/sites-administering/msm.md)

* 翻译允许您自动翻译页面内容、资产和用户生成的内容，以创建和维护多语言网站：

   * [翻译多语言站点的内容](/help/sites-administering/translation.md)

* 这两项功能可以结合使用，以满足[跨国网站和多语言网站](#multinational-and-multilingual-sites)的需求。

## 多国和多语言站点{#multinational-and-multilingual-sites}

通过组合使用多站点管理器和翻译工作流，您可以高效地为跨国和多语言站点创建内容。 为特定国家/地区创建一个主控网站，然后根据需要使用翻译，将该内容用作其他网站的基础：

* [](/help/sites-administering/translation.md) 将主控站点翻译成不同的语言。

* 使用[多站点管理器](/help/sites-administering/msm.md)可以：

   * 重新使用主控网站和翻译中的内容，为其他国家和文化创建网站。
   * 确保将多站点管理器的使用限制为一种语言的内容，例如，“英语主控” — >国家/地区站点中的英语分支、“法语主控” — >国家/地区站点中的法语分支。
   * 根据需要，分离Live Copy的元素以添加本地化详细信息。

下图说明了主要概念如何交叉（但不显示涉及的所有级别/元素）：

![chlimage_1-71](assets/chlimage_1-71a.png)

>[!NOTE]
>
>在此类情况和类似情况下，MSM不会管理不同的语言版本。
>
>* [](/help/sites-administering/msm.md) MSM管理语言边界内将已翻译内容从Blueprint(例如全局主控)部署到Live Copy（例如本地站点）。
>* AEM的[翻译](/help/sites-administering/translation.md)集成功能与第三方翻译管理服务一起管理语言并将内容翻译成这些不同的语言。
>
>对于更高级的用例，也可以跨语言母版使用MSM。

>[!NOTE]
>
>对于所有用例，建议阅读以下最佳实践：
>
>* [MSM最佳实践](/help/sites-administering/msm-best-practices.md);特别是：
>
>   * [创建站点](/help/sites-administering/msm-best-practices.md#create-site)
   * [MSM和多语言网站](/help/sites-administering/msm-best-practices.md#msm-and-multilingual-websites)
* [翻译最佳实践](/help/sites-administering/tc-bp.md)

