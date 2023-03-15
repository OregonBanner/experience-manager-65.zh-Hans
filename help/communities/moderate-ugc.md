---
title: 审核社区内容
seo-title: Moderating Community Content
description: 审核概念和操作
seo-description: Moderation concepts and actions
uuid: 5c991d3a-0037-4d78-8f91-bb62e44441fa
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 6866d209-5789-4ef9-bc3c-d644d4fb4b1c
docset: aem65
role: Admin
exl-id: 22276580-e6bc-41c5-9ac3-e8f291f676b7
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '1516'
ht-degree: 1%

---

# 审核社区内容 {#moderating-community-content}

## 概述 {#overview}

社区内容，也称为用户生成内容(UGC)，是在成员（已登录站点访客）通过与以下社区组件之一交互而发布已发布社区站点的内容时创建的：

* [博客](/help/communities/blog-feature.md)：成员发布博客文章或评论。
* [日历](/help/communities/calendar.md)：成员发布日历事件或评论。
* [评论](/help/communities/comments.md)：成员发布评论或回复评论。

* [论坛](/help/communities/forum.md)：成员发布新主题或回复主题。
* [构思](/help/communities/ideation-feature.md)：成员发布想法或评论。
* [问题与解答](/help/communities/working-with-qna.md)：成员创建问题或回答问题。
* [审核](/help/communities/reviews.md)：成员在对项目进行评级时发表评论。

审核UGC对于识别正面贡献以及限制负面贡献（例如垃圾邮件和滥用语言）很有用。 UGC可从多个环境中审核：

* [社区内容存储](working-with-srp.md)

* [批量审核控制台](moderation.md)

   管理员可以访问“审核”控制台，并且 [社区审查方](/help/communities/users.md) 以及作者环境中的管理员。 当社区内容存储在时，这是可能的 [公用存储](/help/communities/working-with-srp.md).

* [上下文审核](in-context.md)

   管理员和社区审查方可以直接在发布内容的页面上执行发布环境中的审查工作。

## 审核操作 {#moderation-actions}

可以对发布的内容(UGC)执行的操作因用户身份和环境而异。 下表使用以下术语根据用户身份描述各种角色：

* `Admin`

   作为会员的用户 [社区管理员](users.md) 组。

* `Moderator`

   成员属于 [社区审查方](users.md#publishenvironmentusersandgroups) 组(具有 [审查方权限](in-context.md#moderatorpermissions))。

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
   <td><strong>事件<br /> 已触发</strong></td>
   <td><strong>已预审</strong></td>
  </tr>
  <tr>
   <td><strong>编辑/<br /> 删除</strong></td>
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
   <td><strong>关闭/<br /> 重新打开</strong></td>
   <td>X</td>
   <td>X</td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td>X</td>
   <td>X<br /> </td>
  </tr>
  <tr>
   <td><strong>标志/<br /> 取消标记</strong></td>
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

发布帖子后，创建者、管理员或社区审查方可以对其进行编辑或删除。

删除UGC时，它会从存储库中删除，并且可能无法恢复。

### 剪切 {#cut}

管理员或社区审查方可以将一个或多个论坛主题或QnA问题从一个位置移动到另一个位置。 这包括从一个社区站点到另一个社区站点，前提是同一成员在两个站点上具有审核权限。

通过选择“剪切”操作，内容将被复制到剪贴板。 可以将多个帖子作为一个组复制并移动到新位置。

![cutugc](assets/cutugc.png)

![putbackugc](assets/putbackugc.png)

在另一个位置，当内容显示在剪贴板中时，“新建帖子”旁会显示“粘贴”按钮，其中带有一个标识将粘贴的帖子数的数字。 “粘贴”按钮包含一个选项，用于清除剪贴板而不是粘贴。

![帕斯泰于克](assets/pasteugc.png)

![pasteugc1](assets/pasteugc1.png)

### 拒绝 {#deny}

审查方可能不允许在发布的网站上显示UGC。 对于管理员和社区审查方，该帖子仍然可用，并被注释为垃圾邮件。

### 关闭/重新打开 {#close-reopen}

“关闭”操作作用于整个对话会话（论坛主题或初始评论），并包括所有后续帖子或回复。

关闭后，不仅无法进一步回复，还不允许审核操作。

要执行任何操作，必须重新打开主题或注释。

管理员或社区审查方可以执行“关闭/重新打开”操作。

### 标记/取消标记 {#flag-unflag}

标记是除内容创建者之外的任何登录成员指示帖子内容存在问题的一种方式。 标记后，将显示取消标记图标，以允许同一成员取消标记内容。

可以将上下文审核配置为允许成员在标记帖子时选择原因。 可选择的标志原因列表是可配置的，包括是否可以输入自定义原因。 标记原因会与UGC一起保存，但该原因不会触发任何特定操作。 只有标记的数量会触发通知。 已标记的内容会进行相应的注释，以便审查方可以对其进行处理。

系统跟踪所有已标记的标记和标记原因，并在达到阈值时发送事件。 如果社区审查方允许UGC，则会存档这些标记。 在允许和存档之后，如果存在后续标记，则将其存档，就像之前没有标记一样。

### 允许 {#allow}

对于在预审核系统中已标记、已拒绝或未批准的UGC，允许操作是一个选项。 允许操作将清除任何已标记或已拒绝/垃圾邮件状态并存档任何已标记的数据。

## 常见的审核概念 {#common-moderation-concepts}

### 预审 {#premoderation}

预审UGC时，帖子只有在获得审核操作批准后才会显示在已发布的网站上。 创建期间 [社区站点](/help/communities/sites-console.md)，勾选方框 [内容已预审](sites-console.md#moderation) 将为整个站点启用预审。 将组件放在页面上后，可以使用其“编辑”对话框中的设置将支持审核的组件配置为预审：

* [注释](comments.md) 和 [审核](reviews.md)
在 **[!UICONTROL 用户审核]** > **[!UICONTROL 预审]**.

* [论坛](/help/communities/forum.md)， [构思](/help/communities/ideation-feature.md)， [问题与解答](/help/communities/working-with-qna.md)、和 [日历](/help/communities/calendar.md)
在 **[!UICONTROL 设置]** > **[!UICONTROL 已审核]**.

### 垃圾邮件检测 {#spam-detection}

垃圾邮件检测是一种自动审核功能，它通过将用户生成的提交内容标记为垃圾邮件来过滤掉不需要的部分。 一旦启用，它就会根据预配置的垃圾邮件词语集合来识别用户生成的内容是否为垃圾邮件。 默认垃圾邮件字词提供于

`/libs/settings/community/sites/moderation/spamdetector-conf/profiles/spam_words.txt`。

但是，要自定义或扩展默认垃圾邮件单词，请按照默认垃圾邮件单词的结构在/apps目录中创建一组单词，方法是 [叠加](/help/communities/overlay-comments.md).

用户生成的包含垃圾邮件词的帖子（在所有内容类型中，例如博客、论坛和评论）在帖子上方标有“此帖子被分类为垃圾邮件”文本。

审查方可以查看此类帖子并标记该帖子，以允许或拒绝显示在网站上。 可以在上下文中或通过批量审核UI对这些帖子执行审核操作。

![垃圾邮件检测](assets/spamdetection.png)

要启用垃圾邮件检测引擎，请执行以下步骤：

1. 打开 [Web控制台](https://localhost:4502/system/console/configMgr)，通过转到 `/system/console/configMgr`.

1. 查找 **AEM Communities自动审核** 配置，并编辑它。
1. 添加 **[!UICONTROL 垃圾邮件处理]** 登入。

![spamprocess](assets/spamprocess.png)

>[!NOTE]
>
>垃圾邮件检测仅针对英语区域设置实施。

### 情绪 {#sentiment}

情绪根据正关键字和负关键字的数量计算([标语](#configuringwatchwords))存在于帖子(UGC)中。

情绪分析使用一组预配置的规则并计算UGC的情绪。 默认规则位于： `/libs/cq/workflow/components/workflow/social/sentiments/rules.`

规则生成的值介于1（所有负值，无正字）到10（所有正值，无负字）之间。 情绪值为5表示中性情绪，并且是默认值。

/libs组件中定义的规则包括：

* 规则1：如果没有正词和至少一个负词，则将值设置为1。
* 规则2：如果没有负词和至少一个正词，则将值设置为10。
* 规则3：如果负词多于正词，则将值设置为3。
* 规则4：如果正字多于负字，则将值设置为8。

要覆盖或添加规则，请按照默认规则的结构在/apps目录中创建一组规则。 编辑情绪配置以标识规则的位置。

分析完毕后，该情绪将与UGC一起存储。

从 [批量审核控制台](/help/communities/moderation.md)，可以根据情绪是消极、中性还是正面来过滤和查看UGC。

#### 标语 {#watchwords}

AEM communities提供 *关注词分析器* 作为评估过程中的步骤 [情绪](#sentiment). 关注字词对情绪值的贡献是由于对发布内容中使用的负面和正面关注字词以及禁止字词的比较。

#### 配置情绪和标语 {#configure-sentiment-and-watchwords}

可以自定义正面和负面标语列表，也可以自定义情绪规则。

可以将默认关注字列表作为存储库中节点的属性输入，这与默认列表类似，也可以通过配置OSGi服务来覆盖默认列表 `sentimentprocess.name` 和单字的清单。

此 **sentimentprocess.name** 也可以修改为引用自定义情绪规则集的位置。

要配置情绪和标语，请执行以下操作：

* 以管理员身份登录到您的创作实例。
* 打开 [Web控制台](https://localhost:4502/system/console/configMgr).
* 查找 `sentimentprocess.name`.
* 选择要在编辑模式下打开的配置。

![情绪化过程](assets/sentimentprocess.png)

* **正面标语**

   以逗号分隔的单词列表，这些单词有助于覆盖默认值的正面情绪。 默认列表为空。

* **负面标语**

   以逗号分隔的单词列表，这些单词会导致覆盖默认值的负面情绪。 默认列表为空。

* **Watchwords节点的显式路径**

   包含默认值的节点的存储库位置 `positive` 和 `negative` 属性指定默认标语。 默认为 `/libs/settings/community/watchwords/default`.

* **情绪规则**

   用于基于正面和负面关注词计算情绪的规则的存储库位置。 默认为 `/libs/cq/workflow/components/workflow/social/sentiments/rules` （但是，不再涉及任何工作流）。

以下是默认关注字的自定义条目示例，当 `Explicit Path to Watchwords Node` 设置为 `/libs/settings/community/watchwords/default`.

![crxde](assets/crxde.png)

### 审查方权限 {#moderator-permissions}

将以下权限分配给同一资源时，统称为 `moderator permissions`：

* `Read`
* `Modify`
* `Create`
* `Delete`
* `Replicate`
