---
title: 网站管理
seo-title: Website Administration
description: 了解如何在AEM中管理多语言网站。
seo-description: Learn how to manage multilingual websites in AEM.
uuid: a32d458b-a5ad-46ef-a68c-4717c63b4bdd
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: fabaa3e8-1657-4ed4-abb2-990117bec39c
exl-id: 8f11f5de-f5af-4ce7-a448-2b4299de2930
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '341'
ht-degree: 42%

---

# 网站管理{#website-administration}

以下管理工具可用于管理网站和页面：

* 多站点管理器(MSM)允许您在多个位置使用相同的站点内容，同时允许以下变化：

   * [重用内容：多站点管理器和 Live Copy](/help/sites-administering/msm.md)

* 翻译允许您自动翻译页面内容、资产和用户生成的内容，以创建和维护多语言网站：

   * [翻译多语言站点的内容](/help/sites-administering/translation.md)

* 可以结合使用这两种功能，以满足兼具两种功能的网站的需求 [跨国和多语言](#multinational-and-multilingual-sites).

## 跨国和多语言站点 {#multinational-and-multilingual-sites}

通过结合使用多站点管理器和翻译工作流，您可以高效地为跨国和多语言站点创建内容。为特定国家/地区以一种语言创建主控站点，然后将该内容用作其他站点的基础，并在需要时使用翻译：

* 将主站点[翻译](/help/sites-administering/translation.md)成其他语言。

* 使用[多站点管理器](/help/sites-administering/msm.md)可以：

   * 重复使用主控站点的内容和翻译，为其他国家/地区和文化创建站点。
   * 确保将多站点管理器的使用限制为使用一种语言的内容，例如，英语主控->国家/地区站点的英语分支，法语主控->国家/地区站点的法语分支。
   * 如果需要，可分离活动副本的元素以添加本地化详细信息。

下图说明了主要概念的相交部分（但未显示涉及的所有级别/元素）：

![chlimage_1-71](assets/chlimage_1-71a.png)

>[!NOTE]
>
>在此场景以及类似场景中，MSM 不会管理不同的语言版本。
>
>* [MSM](/help/sites-administering/msm.md) 管理在语言边界内从Blueprint(例如全局主控)到活动副本（例如本地站点）的已翻译内容部署。
>* AEM 的[翻译](/help/sites-administering/translation.md)集成功能与第三方翻译管理服务相结合，可以管理语言并将内容翻译成这些不同的语言。
>
>在更高级的用例中，也可以跨语言母版使用 MSM。

>[!NOTE]
>
>对于所有用例，建议阅读以下最佳实践：
>
>* [MSM 的最佳实践](/help/sites-administering/msm-best-practices.md)；特别是：
   >
   >   * [创建站点](/help/sites-administering/msm-best-practices.md#create-site)
   >   * [MSM 和多语言网站](/help/sites-administering/msm-best-practices.md#msm-and-multilingual-websites)
>
>* [翻译的最佳实践](/help/sites-administering/tc-bp.md)

