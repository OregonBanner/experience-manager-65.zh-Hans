---
title: 资产测试的命名约定
seo-title: Naming conventions for assets
description: 存储库中的节点遵循Java内容存储库的命名约定。 但是，Adobe Experience Manager对资源节点名称施加了进一步的约定。
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

# 资产测试的命名约定{#naming-conventions-for-assets-testing}

存储库中的节点遵循的命名约定 [Java内容存储库](/help/sites-developing/the-basics.md#java-content-repository). 但是，Adobe Experience Manager对资源节点名称施加了进一步的约定。

## 经典 UI {#classic-ui}

经典UI施加了更严格的限制：

* 在出现以下任一情况时验证资源名称：

   * 提供了资源标题以转换为节点名称
   * 提供了显式节点名称

* 有效字符（从经典UI中创建资产时，只有这些字符实际有效）：

   * &#39;a&#39;到&#39;z&#39;
   * &#39;A&#39;到&#39;Z&#39;
   * &#39;0&#39;到&#39;9&#39;
   * _ （下划线）
   * `-` （短划线/减号）
