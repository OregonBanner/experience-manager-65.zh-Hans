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
translation-type: tm+mt
source-git-commit: 0885fb6eb6b6a6b8fefd522b2656c8f64e0a537e

---


# 网站管理{#website-administration}

以下管理工具可用于管理网站和页面：

* 多站点管理器(MSM)允许您在多个位置使用相同的站点内容，同时允许各种不同的内容：

   * [重用内容：多站点管理器和Live Copy](/help/sites-administering/msm.md)

* 翻译允许您自动翻译页面内容、资产和用户生成的内容，以创建和维护多语言网站：

   * [翻译多语言站点的内容](/help/sites-administering/translation.md)

* 这两个功能可以结合使用，以满足跨国和多语 [言网站的需要](#multinational-and-multilingual-sites)。

## 跨国和多语言站点 {#multinational-and-multilingual-sites}

通过组合使用多站点管理器和翻译工作流程，您可以高效地为跨国和多语言站点创建内容。 为特定国家／地区创建一种语言的主站点，然后将该内容用作其他站点的基础，根据需要使用翻译：

* [将主站点翻译](/help/sites-administering/translation.md) ，并将其翻译为不同的语言。

* 使用 [多站点管理器](/help/sites-administering/msm.md) :

   * 重用主站点中的内容和翻译，为其他国家和文化创建站点。
   * 确保将多站点管理器的使用限制在一种语言的内容中，例如，国家／地区站点的英语主页->英语分支，法语主页->国家／地区站点的法语分支。
   * 根据需要分离Live Copy的元素以添加本地化详细信息。

下图说明了主要概念的交叉方式（但不显示涉及的所有级别／元素）:

![chlimage_1-71](assets/chlimage_1-71a.png)

>[!NOTE]
>
>在这种情况下，MSM不会管理不同的语言版本，而且情况也比较类似。
>
>* [MSM](/help/sites-administering/msm.md) 管理从蓝图（例如全局主视图）到Live Copy（例如本地站点）的翻译内容在语言边界内的部署。
>* AEM [的翻译集成](/help/sites-administering/translation.md) 功能与第三方翻译管理服务一起管理语言并将内容翻译为这些不同的语言。
>
>
对于更高级的用例，MSM也可以跨语言主页使用。

>[!NOTE]
>
>对于所有用例，建议阅读以下最佳实践：
>
>* [MSM的最佳实践](/help/sites-administering/msm-best-practices.md);特别是：
   >
   >   
   * [创建站点](/help/sites-administering/msm-best-practices.md#create-site)
   >   * [MSM和多语言网站](/help/sites-administering/msm-best-practices.md#msm-and-multilingual-websites)
>
>* [翻译的最佳实践](/help/sites-administering/tc-bp.md)

