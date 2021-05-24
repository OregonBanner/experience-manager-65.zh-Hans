---
title: 资产测试的命名约定
seo-title: 资产的命名约定
description: 存储库中的节点须遵守 Java 内容存储库的命名约定。但是，Adobe Experience Manager 对资产节点的名称做了进一步约定。
seo-description: 存储库中的节点须遵守 Java 内容存储库的命名约定。但是，Adobe Experience Manager 对资产节点的名称做了进一步约定。
uuid: 6b622a60-90e8-461e-9b67-42c11c7038f9
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: authoring
content-type: reference
discoiquuid: 55e66c66-0120-4ed4-94c5-d65a434bb59b
exl-id: bb6a5913-0871-47c7-8641-936e98920ec0
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '159'
ht-degree: 89%

---

# 资产的命名约定 测试{#naming-conventions-for-assets-testing}

存储库中的节点受[Java内容存储库](/help/sites-developing/the-basics.md#java-content-repository)的命名约定的约束。 但是，Adobe Experience Manager 对资产节点的名称做了进一步约定。

## 经典 UI {#classic-ui}

经典 UI 实施更严格的限制：

* 在以下情况下验证资产名称：

   * 提供了资产标题以将其转换为节点名称
   * 提供了明确的节点名称

* 有效字符（从经典 UI 中创建资产时，实际上只有这些字符才有效）：

   * “a”至“z”
   * “A”至“Z”
   * “0”至“9”
   * _（下划线）
   * `-` （短划线/减号）
