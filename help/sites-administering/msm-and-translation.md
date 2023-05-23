---
title: 網站管理
seo-title: Website Administration
description: 瞭解如何在AEM中管理多語言網站。
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

# 網站管理{#website-administration}

下列管理工具可用來管理網站和頁面：

* 多網站管理員(MSM)可讓您在多個位置使用相同的網站內容，同時允許以下變化：

   * [重用内容：多站点管理器和 Live Copy](/help/sites-administering/msm.md)

* 翻譯可讓您自動翻譯頁面內容、資產和使用者產生的內容，以建立和維護多語言網站：

   * [翻译多语言站点的内容](/help/sites-administering/translation.md)

* 這兩個功能可結合使用，以符合以下兩種網站的需求： [跨國及多國語言](#multinational-and-multilingual-sites).

## 跨国和多语言站点 {#multinational-and-multilingual-sites}

通过结合使用多站点管理器和翻译工作流，您可以高效地为跨国和多语言站点创建内容。針對特定國家/地區，以一種語言建立主要網站，然後將該內容作為其他網站的基礎，並在需要時使用翻譯：

* 将主站点[翻译](/help/sites-administering/translation.md)成其他语言。

* 使用[多站点管理器](/help/sites-administering/msm.md)可以：

   * 重複使用主要網站的內容和翻譯，為其他國家/地區和文化建立網站。
   * 請務必將多網站管理員的使用限製為使用單一語言的內容，例如，英文母版 — >國網站的英文分支，法文母版 — >國網站的法文分支。
   * 必要時，請分離即時副本的元素，以新增本地化詳細資訊。

下图说明了主要概念的相交部分（但未显示涉及的所有级别/元素）：

![chlimage_1-71](assets/chlimage_1-71a.png)

>[!NOTE]
>
>在此场景以及类似场景中，MSM 不会管理不同的语言版本。
>
>* [MSM](/help/sites-administering/msm.md) 管理在語言範圍內從Blueprint （例如全域主版）到即時副本（例如本機站台）的翻譯內容部署。
>* AEM 的[翻译](/help/sites-administering/translation.md)集成功能与第三方翻译管理服务相结合，可以管理语言并将内容翻译成这些不同的语言。
>
>在更高级的用例中，也可以跨语言母版使用 MSM。

>[!NOTE]
>
>对于所有用例，建议阅读以下最佳实践：
>
>* [MSM 的最佳实践](/help/sites-administering/msm-best-practices.md)；尤其是：
   >
   >   * [创建站点](/help/sites-administering/msm-best-practices.md#create-site)
   >   * [MSM 和多语言网站](/help/sites-administering/msm-best-practices.md#msm-and-multilingual-websites)
>
>* [翻译的最佳实践](/help/sites-administering/tc-bp.md)

