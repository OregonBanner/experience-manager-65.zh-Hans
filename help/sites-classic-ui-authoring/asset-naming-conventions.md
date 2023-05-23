---
title: 資產測試的命名慣例
seo-title: Naming conventions for assets
description: 存放庫中的節點會受到Java內容存放庫的命名慣例的約束。 不過，Adobe Experience Manager對資產節點名稱施加了進一步的慣例。
seo-description: Nodes in the repository are subject to naming conventions of the Java Content Repository. However, Adobe Experience Manager imposes further conventions for the name of asset nodes.
uuid: 6b622a60-90e8-461e-9b67-42c11c7038f9
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: authoring
content-type: reference
discoiquuid: 55e66c66-0120-4ed4-94c5-d65a434bb59b
exl-id: bb6a5913-0871-47c7-8641-936e98920ec0
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '128'
ht-degree: 1%

---

# 資產測試的命名慣例{#naming-conventions-for-assets-testing}

存放庫中的節點受限於的命名慣例 [Java內容存放庫](/help/sites-developing/the-basics.md#java-content-repository). 不過，Adobe Experience Manager對資產節點名稱施加了進一步的慣例。

## 经典 UI {#classic-ui}

傳統UI施加了更嚴格的限制：

* 當出現下列任一情況時，當有明確的節點名稱時，會驗證資產名稱：

   * 提供了資產標題，以便轉換為節點名稱
   * 提供了明確的節點名稱

* 有效字元（從傳統UI中建立資產時，實際只有這些字元有效）：

   * &#39;a&#39;至&#39;z&#39;
   * &#39;A&#39;至&#39;Z&#39;
   * &#39;0&#39;到&#39;9&#39;
   * _ （底線）
   * `-` （破折號/減號）
