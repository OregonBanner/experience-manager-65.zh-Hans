---
title: 评分和徽章要点
seo-title: Scoring and Badges Essentials
description: 评分和徽章功能概述
seo-description: Scoring and Badges feature overview
uuid: 6e3af071-04e8-4dc1-977a-0da711b72961
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 628b6dcd-8b1c-4166-8fc2-843baa86ac1c
docset: aem65
exl-id: 470a382a-2aa7-449e-bf48-b5a804c5b114
source-git-commit: 4fa868f3ae4778d3a637e90b91f7c5909fe5f8aa
workflow-type: tm+mt
source-wordcount: '934'
ht-degree: 1%

---

# 评分和徽章要点 {#scoring-and-badges-essentials}

AEM Communities评分和徽章功能可识别和奖励社区成员。

有关设置该功能的详细信息，请参阅

* [社区评分和徽章](/help/communities/implementing-scoring.md)

此页面包含其他技术详细信息：

* 操作方法 [显示徽章](#displaying-badges) 作为图像或文本
* 如何启用大范围 [调试日志记录](#debug-log-for-scoring-and-badging)
* 操作方法 [访问UGC](#ugc-for-scoring-and-badging) 与评分和徽章相关

>[!CAUTION]
>
>在CRXDE Lite中可见的实施结构可能会发生更改。

## 显示徽章 {#displaying-badges}

在HBS模板中，是在客户端控制徽章是显示为文本还是图像。

例如，搜索 `this.isAssigned` 在 `/libs/social/forum/components/hbs/topic/list-item.hbs`：

```
{{#each author.badges}}

  {{#if this.isAssigned}}

    <div class="scf-badge-text">

      {{this.title}}

    </div>

  {{/if}}

{{/each}}

{{#each author.badges}}

  {{#unless this.isAssigned}}

    <img class="scf-badge-image" alt="{{this.title}}" title="{{this.title}}" src="{{this.imageUrl}}" />

  {{/unless}}

{{/each}}
```

如果为true，则isAssigned表示已为角色分配了徽章，并且该徽章应显示为文本。

如果为false，则isAssigned表示该徽章已获得已习得的分数，并且该徽章应显示为图像。

对此行为的任何更改都应在自定义脚本中进行（覆盖或叠加）。 参见 [客户端自定义](/help/communities/client-customize.md).

## 评分和徽章的调试日志 {#debug-log-for-scoring-and-badging}

为了帮助调试评分和标记，可以设置自定义日志文件。 之后，如果功能出现问题，可以将该日志文件的内容提供给客户支持。

有关详细说明，请访问 [创建自定义日志文件](/help/sites-deploying/monitoring-and-maintaining.md#create-a-custom-log-file).

要快速设置slinglog文件：

1. 访问 **Adobe Experience Manager Web控制台日志支持**&#x200B;例如

   * https://localhost:4502/system/console/slinglog

1. 选择 **添加新记录器**

   1. 选择 `DEBUG` 对象 **日志级别**

   1. 输入名称 **日志文件**&#x200B;例如

      * logs/scoring-debug.log
   1. 输入两个 **Logger** （类）条目(使用 `+` 图标)

      * `com.adobe.cq.social.scoring`
      * `com.adobe.cq.social.badging`
   1. 选择 **保存**



![debug-scoring-log](assets/debug-scoring-log.png)

要查看日志条目，请执行以下操作：

* 从Web控制台

   * 在 **状态** 菜单
   * 选择 **日志文件**
   * 搜索日志文件名称，例如 `scoring-debug`

* 在服务器的本地磁盘上

   * 日志文件位于&lt;*server-install-dir*>/crx-quickstart/logs/&lt;*log-file-name*>.log

   * 例如，`.../crx-quickstart/logs/scoring-debug.log`

![scoring-log](assets/scoring-log.png)

## 评分和徽章的UGC {#ugc-for-scoring-and-badging}

当所选的SRP是JSRP或MSRP，而不是ASRP时，可以查看与评分和标记相关的UGC。 (如果不熟悉这些术语，请参阅 [社区内容存储](/help/communities/working-with-srp.md) 和 [存储资源提供程序概述](/help/communities/srp.md).)

访问评分和徽章数据的描述使用JSRP，因为UGC易于访问，使用 [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md).

**创作实例上的JSRP**：在创作环境中进行实验会生成仅从创作环境中可见的UGC。

**发布时JSRP**：同样，如果在发布环境中进行测试，则需要在发布实例上使用管理权限访问CRXDE Lite。 如果发布实例在中运行 [生产模式](/help/sites-administering/production-ready.md) (nosamplecontent runmode)，必须 [启用CRXDE Lite](/help/sites-administering/enabling-crxde-lite.md).

JSRP上UGC的基本位置为 `/content/usergenerated/asi/jcr/`.

### 评分和徽章API {#scoring-and-badging-apis}

以下API可供使用：

* [com.adobe.cq.social.scoring.api在6.3中](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=zh-Hans)
* [com.adobe.cq.social.badging.api在6.3中](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=zh-Hans)

开发人员可以从Adobe存储库中找到已安装功能包的最新Javadoc。 参见 [使用Maven for Communities ：Javadocs](/help/communities/maven.md#javadocs).

**UGC在存储库中的位置和格式可能会发生更改，恕不发出警告**.

### 示例设置 {#example-setup}

存储库数据的屏幕截图来自为两个不同AEM站点上的论坛设置评分和徽章：

1. AEM站点 *替换为* 唯一id（使用向导创建的社区站点）：

   * 使用在中创建的快速入门教程（参与）站点 [入门教程](/help/communities/getting-started.md)
   * 找到论坛页面节点

      `/content/sites/engage/en/forum/jcr:content`

   * 添加评分和徽章属性

   ```
   scoringRules = [/libs/settings/community/scoring/rules/comments-scoring,
   /libs/settings/community/scoring/rules/forums-scoring]
   ```

   ```
   badgingRules =[/libs/settings/community/badging/rules/comments-scoring,
   /libs/settings/community/badging/rules/forums-scoring]
   ```

   * 找到论坛组件节点

      `/content/sites/engage/en/forum/jcr:content/content/primary/forum`
( `sling:resourceType = social/forum/components/hbs/forum`)

   * 要显示徽章，请添加属性

      `allowBadges = true`

   * 用户登录、创建论坛主题并获得“铜牌”


1. AEM站点 *不含* 唯一ID ：

   * 使用 [社区组件指南](/help/communities/components-guide.md)
   * 找到论坛页面节点

      `/content/community-components/en/forum/jcr:content`

   * 添加评分和徽章属性

   ```
   scoringRules = [/libs/settings/community/scoring/rules/comments-scoring,
   /libs/settings/community/scoring/rules/forums-scoring]
   ```

   ```
   badgingRules =[/libs/settings/community/badging/rules/comments-badging,
   /libs/settings/community/badging/rules/forums-badging]
   ```

   * 找到论坛组件节点

      `/content/community-components/en/forum/jcr:content/content/forum`
( `sling:resourceType = social/forum/components/hbs/forum`)

   * 要显示徽章，请添加属性

      `allowBadges = true`

   * 用户登录、创建论坛主题并获得“铜牌”


1. 已使用cURL为用户分配了审查方徽章：

   ```shell
   curl -i -X POST -H "Accept:application/json" -u admin:admin -F ":operation=social:assignBadge" -F "badgeContentPath=/libs/settings/community/badging/images/moderator/jcr:content/moderator.png" https://localhost:4503/home/users/community/w271OOup2Z4DjnOQrviv/profile.social.json
   ```

   由于用户已获得两个铜牌并获得了版主徽章，因此该用户将与其论坛条目一起显示，如下所示：

   ![审查方](assets/moderator.png)

>[!NOTE]
>
>此示例不遵循以下最佳实践：
>
>* 评分规则名称应在全局范围内是唯一的；它们不应以相同的名称结尾。
>
>  以下示例 *非* 待办事项：
>
>  /libs/settings/community/scoring/rules/site1/forums-scoring
>  /libs/settings/community/scoring/rules/site2/forums-scoring
>
>* 为不同的AEM站点创建唯一的徽章图像


### 访问评分UGC {#access-scoring-ugc}

使用 [API](#scoring-and-badging-apis) 是首选。

出于调查目的，以JSRP为例，包含分数的基本文件夹为

* `/content/usergenerated/asi/jcr/scoring`

的子节点 `scoring` 是评分规则名称。 因此，最佳实践是服务器上的评分规则名称具有全局唯一性。

对于GeometrixxEngage站点，用户及其分数位于使用评分规则名称、社区站点的站点ID ( `engage-ba81p`)、唯一ID和用户的ID ：

* `.../scoring/forums-scoring/engage-ba81p/6d179715c0e93cb2b20886aa0434ca9b5a540401/riley`

对于社区组件指南网站，用户及其分数位于使用评分规则名称(默认ID ( `default-site`)、唯一ID和用户的ID ：

* `.../scoring/forums-scoring/default-site/b27a17cb4910a9b69fe81fb1b492ba672d2c086e/riley`

分数存储在属性中 `scoreValue_tl` 只能包含值，或者间接引用atomicCounter。

![access-scoring-ugc](assets/access-scoring-ugc.png)

### 访问徽章UGC {#access-badging-ugc}

使用 [API](#scoring-and-badging-apis) 是首选。

出于调查目的，以JSRP为例，包含有关已分配或已授予徽章的信息的基本文件夹为

* `/content/usergenerated/asi/jcr`

后跟用户配置文件的路径，以徽章文件夹结尾，例如：

* `/home/users/community/w271OOup2Z4DjnOQrviv/profile/badges`

#### 已授予的徽章 {#awarded-badge}

![warded-badging-ugc](assets/access-badging-ugc.png)

#### 已分配的徽章 {#assigned-badge}

![assigned-badge](assets/assigned-badge.png)

## 附加信息 {#additional-information}

要根据点显示已排序的成员列表，请执行以下操作：

* [排行榜功能](/help/communities/functions.md#leaderboard-function) 社区站点或组模板中的内容。
* [排行榜组件](/help/communities/enabling-leaderboard.md)，排行榜功能的特色组件，用于页面创作。
