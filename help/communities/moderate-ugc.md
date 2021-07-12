---
title: 审核社区内容
seo-title: 审核社区内容
description: 审核概念和操作
seo-description: 审核概念和操作
uuid: 5c991d3a-0037-4d78-8f91-bb62e44441fa
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 6866d209-5789-4ef9-bc3c-d644d4fb4b1c
docset: aem65
role: Admin
exl-id: 22276580-e6bc-41c5-9ac3-e8f291f676b7
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '1523'
ht-degree: 1%

---

# 审核社区内容 {#moderating-community-content}

## 概述 {#overview}

社区内容也称为用户生成内容(UGC)，它是在成员（登录到站点访客）通过与以下社区组件之一交互从已发布的社区站点发布内容时创建的：

* [博客](/help/communities/blog-feature.md):成员会发布博客文章或评论。
* [日历](/help/communities/calendar.md):成员发布日历事件或评论。
* [评论](/help/communities/comments.md):成员发布评论或回复评论。

* [论坛](/help/communities/forum.md):成员发布新主题或回复主题。
* [构思](/help/communities/ideation-feature.md):成员会发布想法或评论。
* [问题解答](/help/communities/working-with-qna.md):成员可创建问题或回答问题。
* [评论](/help/communities/reviews.md):成员在对项目进行评级时发布评论。

审核UGC对于确认积极贡献以及限制消极贡献（如垃圾邮件和辱骂语言）非常有用。 UGC可以从以下几个环境中审核：

* [社区内容存储](working-with-srp.md)

* [批量审核控制台](moderation.md)

   管理员和[社区审核者](/help/communities/users.md)可在公共环境中访问审核控制台，也可在创作环境中由管理员访问。 当社区内容存储在[公共存储](/help/communities/working-with-srp.md)中时，这是可能的。

* [上下文审核](in-context.md)

   发布环境中的审核可由管理员和社区审核者直接在发布内容的页面上执行。

## 审核操作 {#moderation-actions}

可对发布内容(UGC)执行的操作会因用户身份和环境而异。 下表使用以下术语根据用户身份描述各种角色：

* `Admin`

   [community-administrators](users.md)组成员的用户。

* `Moderator`

   [社区审核者](users.md#publishenvironmentusersandgroups)组的成员（具有[审核者权限](in-context.md#moderatorpermissions)）。

* `Creator`

   发布内容的用户。

* `Member`

   没有特殊权限的登录用户。

* `Visitor`

   匿名用户。

<table>
 <tbody>
  <tr>
   <td> </td>
   <td><strong>管理员</strong></td>
   <td><strong>审查方</strong></td>
   <td><strong>创建者</strong></td>
   <td><strong>成员</strong></td>
   <td><strong>访客</strong></td>
   <td><strong>已触发事件<br /></strong></td>
   <td><strong>预审</strong></td>
  </tr>
  <tr>
   <td><strong>编辑/<br />删除</strong></td>
   <td>X</td>
   <td>X</td>
   <td>X</td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>剪切</strong></td>
   <td>X</td>
   <td>X</td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>拒绝</strong></td>
   <td>X</td>
   <td>X</td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td>X</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>关闭/<br />重新打开</strong></td>
   <td>X</td>
   <td>X</td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td>X</td>
   <td>X<br /> </td>
  </tr>
  <tr>
   <td><strong>标记/<br />取消标记</strong></td>
   <td>X</td>
   <td>X</td>
   <td> </td>
   <td>X</td>
   <td> </td>
   <td>X</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>允许</strong></td>
   <td>X</td>
   <td>X</td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td>X</td>
   <td>X</td>
  </tr>
 </tbody>
</table>

### 编辑/删除 {#edit-delete}

帖子发布后，创建者、管理员或社区审查者可以编辑或删除该帖子。

删除UGC后，它将从存储库中删除，并且可能无法恢复。

### 剪切 {#cut}

管理员或社区主持人可以将一个或多个论坛主题或问题解答问题从一个位置移动到另一个位置。 这包括从一个社区站点到另一个社区站点，前提是同一成员在两个站点上都具有审核权限。

通过选择“剪切”操作，内容将复制到剪贴板。 可以将多个帖子作为群组复制并移动到新位置。

![cutugc](assets/cutugc.png)

![putbackugc](assets/putbackugc.png)

在另一个位置，当剪贴板中存在内容时，“新建帖子”旁会显示“粘贴”按钮，其中包含一个用于标识将粘贴的帖子数量的数字。 “粘贴”按钮包含一个用于清除剪贴板的选项，而不是粘贴。

![巴氏](assets/pasteugc.png)

![pasteug1](assets/pasteugc1.png)

### 拒绝 {#deny}

审核者可能不允许UGC在已发布的网站上保持可见。 对于管理员和社区审核者而言，该帖子仍然可用，并且会添加垃圾信息注释。

### 关闭/重新打开 {#close-reopen}

“关闭”操作在整个对话线程（论坛主题或初始评论）中运行，并且包含所有后续帖子或回复。

关闭后，不仅无法再进行进一步的回复，还不允许执行审核操作。

要执行任何操作，主题或注释必须重新打开。

管理员或社区审核者可以执行关闭/重新打开操作。

### 标记/取消标记 {#flag-unflag}

标记是任何已登录成员（内容的创建者除外）的一种方式，用于指示帖子内容存在问题。 标记后，将显示一个取消标记图标，允许同一成员取消标记内容。

可以将上下文关联审核配置为允许成员在标记帖子时选择原因。 可配置可选标记原因的列表，包括是否可以输入自定义原因。 标记原因已与UGC一起保存，但原因未触发任何特定操作。 只有标记数会触发通知。 标记内容会这样添加注释，以便审核者可以对其执行操作。

系统会跟踪所有标记的标记以及标记原因，并在达到阈值时发送事件。 如果社区审核者允许使用UGC，则会存档这些标记。 在允许和存档后，如果存在后续标记，则会像之前没有标记一样将其存档。

### 允许 {#allow}

“允许”操作是已标记、拒绝或未在预审核系统中批准的UGC选项。 “允许”操作将清除任何已标记或已拒绝/垃圾邮件状态，并存档任何已标记的数据。

## 常见审核概念 {#common-moderation-concepts}

### 预审核 {#premoderation}

UGC经过预审核后，在审核操作批准之前，不会在已发布的网站上显示该帖子。 在创建[社区站点](/help/communities/sites-console.md)期间，选中[内容为预审的](sites-console.md#moderation)框将为整个站点启用预审。 将组件放置到页面上后，可以使用编辑对话框中的设置，为预审核配置支持审核的组件：

* [](comments.md) “用户 [](reviews.md)
审核” **** >“预审” ****&#x200B;中的评论和审阅。

* [论坛](/help/communities/forum.md)、 [构思](/help/communities/ideation-feature.md)、 [QnA](/help/communities/working-with-qna.md)和日历 [](/help/communities/calendar.md)
设 **[!UICONTROL 置]**  >  **[!UICONTROL 已审核]**。

### 垃圾邮件检测 {#spam-detection}

垃圾邮件检测是一项自动审核功能，可通过将提交的用户生成的内容标记为垃圾邮件，过滤掉不可期待的内容。 启用后，它会根据预先配置的垃圾词集合来识别用户生成的内容是否为垃圾邮件。 默认的垃圾邮件词位于

`/libs/settings/community/sites/moderation/spamdetector-conf/profiles/spam_words.txt`。

但是，要自定义或扩展默认垃圾词，请通过[overlay](/help/communities/overlay-comments.md)在/apps目录中按照默认垃圾词的结构创建一组词。

用户生成的包含垃圾词的帖子（涵盖所有内容类型，例如博客、论坛和评论）在帖子上方标有“此帖子被分类为垃圾邮件”文本。

审核者可以查看此类帖子并标记相同的帖子，以允许或拒绝在网站上显示。 可以在上下文中或通过批量审核UI对这些帖子执行审核操作。

![垃圾邮件检测](assets/spamdetection.png)

要启用垃圾邮件检测引擎，请执行以下步骤：

1. 通过转到`/system/console/configMgr`打开[Web控制台](https://localhost:4502/system/console/configMgr)。

1. 找到&#x200B;**AEM Communities自动审核**&#x200B;配置，并对其进行编辑。
1. 添加&#x200B;**[!UICONTROL SpamProcess]**&#x200B;条目。

![垃圾进程](assets/spamprocess.png)

>[!NOTE]
>
>垃圾邮件检测仅针对英语区域设置实施。

### 情绪 {#sentiment}

情绪是根据帖子(UGC)中存在的正面和负面关键词（[关注词](#configuringwatchwords)）的数量计算的。

情绪分析使用一组预配置的规则并计算UGC的情绪。 默认规则位于：`/libs/cq/workflow/components/workflow/social/sentiments/rules.`

规则生成的值从1（所有负数，无正数字）到10（所有正数字，无负数字）。 情绪值为5是中性情绪，为默认值。

/libs组件中定义的规则包括：

* 规则1:如果没有正面词语和至少一个负面词语，则将值设置为1。
* 规则2:如果没有负词且至少有一个正词，则将值设置为10。
* 规则3:如果比正面词语多的负面词语，则将值设置为3。
* 规则4:如果正面词语多于负面词语，则将值设置为8。

要覆盖或添加规则，请按照默认规则的结构在/apps目录中创建一组规则。 编辑情绪配置以标识规则的位置。

分析后，情绪将与UGC一起存储。

从[批量审核控制台](/help/communities/moderation.md)中，可以根据情绪是负面、中性还是正面来过滤和查看UGC。

#### 关注词 {#watchwords}

AEM社区提供&#x200B;*观看词分析器*&#x200B;作为评估[情绪](#sentiment)过程中的步骤。 关注词对情绪值的贡献是对已发布内容中使用的负面和正面关注词以及禁止的词语进行比较所致。

#### 配置情绪和关注词 {#configure-sentiment-and-watchwords}

可以自定义正面和负面关键词列表，因为它可以是情绪规则。

默认的关注词列表可以作为存储库中节点的属性输入，与默认值类似，或者通过使用词语列表配置OSGi服务`sentimentprocess.name`来覆盖默认值。

也可以修改&#x200B;**sentimentprocess.name**&#x200B;以引用一组自定义情绪规则的位置。

要配置情绪和口号，请执行以下操作：

* 以管理员身份登录到创作实例。
* 打开[Web控制台](https://localhost:4502/system/console/configMgr)。
* 找到`sentimentprocess.name`。
* 选择要在编辑模式下打开的配置。

![情绪过程](assets/sentimentprocess.png)

* **积极的口号**

   对覆盖默认值的积极情绪做出贡献的词语列表（以逗号分隔）。 默认为空列表。

* **负面关键词**

   导致覆盖默认值的负面情绪的词语列表（以逗号分隔）。 默认为空列表。

* **关注词节点的显式路径**

   包含指定默认关注词的默认`positive`和`negative`属性的节点的存储库位置。 默认值为`/libs/settings/community/watchwords/default`。

* **情绪规则**

   用于根据正面和负面关键词计算情绪的规则的存储库位置。 默认值为`/libs/cq/workflow/components/workflow/social/sentiments/rules`（但是，不再涉及任何工作流）。

以下是将`Explicit Path to Watchwords Node`设置为`/libs/settings/community/watchwords/default`时默认关注词的自定义条目示例。

![crxde](assets/crxde.png)

### 审核者权限 {#moderator-permissions}

以下权限在分配给同一资源时统称为`moderator permissions`:

* `Read`
* `Modify`
* `Create`
* `Delete`
* `Replicate`
