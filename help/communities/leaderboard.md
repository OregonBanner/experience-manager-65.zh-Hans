---
title: 排行榜要点
description: 了解如何配置社区评分和徽章，以便您可以使用Adobe Experience Manager Communities中的排行榜组件。
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: fd1b1749-13f9-4079-ae39-348676105852
source-git-commit: 62d4a8b3af5031ccc539d78f7d06a8cd1fec7af1
workflow-type: tm+mt
source-wordcount: '112'
ht-degree: 4%

---

# 排行榜要点 {#leaderboard-essentials}

本页提供了使用排行榜功能的基本信息。

在页面上包含排行榜组件之前，需要配置 [社区评分和徽章](implementing-scoring.md).

请参阅 [评分和徽章要点](configure-scoring.md).

## 适用于客户端的Essentials {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/gamification/components/hbs/leaderboard</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>可包含</strong></a></td>
   <td>否</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md"><strong>clientllibs</strong></a></td>
   <td>cq.social.gamification.hbs.leaderboard</td>
  </tr>
  <tr>
   <td> <strong>模板</strong></td>
   <td> /libs/social/gamification/components/hbs/leaderboard/leaderboard.hbs<br /> </td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/gamification/components/hbs/leaderboard/clientlibs/leaderboard.css</td>
  </tr>
  <tr>
   <td><strong> 属性</strong></td>
   <td>请参阅 <a href="enabling-leaderboard.md">排行榜功能</a></td>
  </tr>
 </tbody>
</table>

* [客户端自定义](client-customize.md)

### 文件库功能 {#file-library-function}

社区站点结构包括 [排行榜功能](functions.md#leaderboard-function)，包括已配置的 `leaderboard` 组件。
