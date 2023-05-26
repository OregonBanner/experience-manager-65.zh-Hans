---
title: 使用审阅和审阅摘要（显示）
seo-title: Using Reviews and Reviews Summary (Display)
description: 将审阅和审阅摘要组件添加到页面
seo-description: Adding the Reviews and Reviews Summary components to a page
uuid: bd1ccee7-b26b-4a27-b1ea-89609f5080af
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: bf4e7809-8def-4647-aaa6-3ac36865511f
exl-id: 170414a6-c40b-4ad2-9294-7c2266850c3d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1294'
ht-degree: 2%

---

# 使用审阅和审阅摘要（显示） {#using-reviews-and-reviews-summary-display}

此 `Reviews` 组件是以下项的组合： [注释](comments.md) 和 [评级](rating.md) 组件可供使用。

此 `Reviews Summary (Display)` 组件提供活动或已关闭实例的摘要 `Reviews` 组件以便在网站上的其他位置显示。

>[!NOTE]
>
>不支持评论的匿名发布。 网站访客必须注册（成为会员）并登录才能参与。 已登录的访客可以随时更新其评论。

## 将审阅添加到页面 {#adding-a-review-to-a-page}

添加 `Reviews` 组件添加到创作模式下的页面，请使用组件浏览器来查找 `Communities / Reviews` 并将其拖动到页面上的适当位置，例如相对于该功能的位置以供用户查看。

有关必要信息，请访问 [社区组件基础知识](basics.md).

当 [所需的客户端库](reviews-basics.md#essentials-for-client-side) 包括，这就是 `Reviews` 组件随即出现。

![create-review](assets/create-review.png)

## 配置审核 {#configuring-reviews}

选择已放置的 `Reviews` 组件以访问和选择 `Configure` 图标，打开“编辑”对话框。

![configure-new](assets/configure-new.png)

在 **[!UICONTROL 允许的评级]** 选项卡，指定要向成员显示的完整评级列表。 第一个评级应为总体/综合评级，因为它是为以下类别提供平均评级的评级 `Review Summary (Display)` 组件。 默认配置中的后续两个评级应该使用不同的标题，而不是“子评级1”或“子评级2”。

![允许评级](assets/configure-review1.png)

* **[!UICONTROL 允许的评级]**

   成员可以从中进行选择的评级列表。

   使用向上箭头、向下箭头和删除按钮修改可见选择。

   单击 **[!UICONTROL 添加项目]** 以添加其他评级选择。

在 **[!UICONTROL 所需评级]** 选项卡，从列表中重新输入项目 **[!UICONTROL 允许的评级]** 需要进行评级的。 如果仅在“允许的评级”选项卡上指定了项目，则成员提交该项目时，该项目可能会保持未标记状态。

在网站上，必填评级标有星号。 如果某个项目是必需的且未标记，则会向成员显示一条消息，并且会拒绝提交，直到标记完所有必需的评级为止。

![required-rating](assets/configure-review2.png)

* **[!UICONTROL 所需的评级]**

   允许的评级子集，指示所需的评级。

   使用向上箭头、向下箭头和删除按钮修改可见选择。

   单击 **[!UICONTROL 添加项目]** 以添加其他响应选择。

>[!NOTE]
>
>如果在以下位置输入了项目： **[!UICONTROL 所需评级]** 选项卡上未指定的 **[!UICONTROL 允许的评级]** 选项卡，则它不会包含在要评分的项目中。

在 **[!UICONTROL 审核]** 选项卡，指定如何处理审核。

![审核](assets/configure-review3.png)

* **[!UICONTROL 允许回复]**

   如果选中，则允许回复审核。 默认值为未选中。

* **[!UICONTROL 已关闭]**

   如果选中，则对于新审阅和回复，审阅将被关闭。 默认值为未选中。

* **[!UICONTROL 允许文件上传]**

   如果选中，则允许上载文件附件以供审阅。 默认值为未选中。

* **最大文件大小**

   相关条件仅限于 **[!UICONTROL 允许文件上传]** 已选中。 此字段限制已上传文件的大小（以字节为单位）。 默认值为10 MB。

* **[!UICONTROL 最大消息长度]**

   文本框中可以输入的最大字符数。 默认值为4096个字符。

* **[!UICONTROL 允许的文件类型]**

   相关条件仅限于 **[!UICONTROL 允许文件上传]** 已选中。 包含“点”分隔符的逗号分隔文件扩展名列表。 例如： .jpg、.jpeg、.png、.doc、.docx、.pdf。 如果指定了任何文件类型，则将不允许未指定的文件类型。 缺省值为none以便允许所有文件类型。

* **[!UICONTROL 富文本编辑器]**

   如果选中，则可以使用标记输入帖子。 默认值为未选中。

* **[!UICONTROL 允许投票]**

   如果选中，则为主题包含投票功能。 默认值为未选中。

在 **[!UICONTROL 用户审核]** 选项卡，指定如何管理已发布的审核。 有关更多信息，请参阅 [审核用户生成的内容](moderate-ugc.md).

![user-moderation](assets/configure-review4.png)

* **[!UICONTROL 预审]**

   如果选中，审阅必须先获得批准，然后才能显示在发布网站上。 默认值为未选中。

* **[!UICONTROL 删除审核]**

   如果选中，则为发布审阅的成员提供删除审阅的功能。 默认值为未选中。

* **[!UICONTROL 拒绝审核]**

   如果选中，则允许审查方拒绝审核。 默认值为未选中。

* **[!UICONTROL 关闭/重新打开审阅]**

   如果选中，则允许审查方关闭和重新打开审查。 默认值为未选中。

* **[!UICONTROL 标记审核]**

   如果选中，则允许成员将审核标记为不适当。 默认值为未选中。

* **[!UICONTROL 标记原因列表]**

   如果选中，则允许成员从下拉列表中选择将审核标记为不适当的原因。 默认值为未选中。

* **[!UICONTROL 自定义标志原因]**

   如果选中，则允许成员输入他们自己的原因，将审核标记为不适当。 默认值为未选中。

* **[!UICONTROL 审核阈值]**

   输入在通知审查方之前，成员必须标记审查的次数。 默认值为一次(1)。

* **[!UICONTROL 标记限制]**

   输入在将审阅从公众视野中隐藏之前必须将其标记的次数。 此数字必须大于或等于 **[!UICONTROL 审核阈值]**. 默认值为5。

### 向页面添加审核摘要（显示） {#adding-a-review-summary-display-to-a-page}

添加 `Reviews Summary (Display)` 组件到创作模式下的页面，找到该组件

* `Communities / Reviews Summary (Display)`

并将其拖动到将显示活动或已关闭审阅的摘要的页面上。

有关必要信息，请访问 [社区组件基础知识](basics.md).

当 [所需的客户端库](reviews-basics.md#essentials-for-client-side) 包括，这就是 `Reviews Summary (Display)`组件随即出现。

![review-summary](assets/configure-review5.png)

>[!NOTE]
>
>“平均值”反映所总结评论的“允许的评级”选项卡上列出的第一个项目的投票数。

### 配置审阅摘要（显示） {#configuring-reviews-summary-display}

选择已放置的 `Reviews Summary (Display)` 组件以访问和选择 `Configure` 图标，打开“编辑”对话框。

![配置](assets/configure-new.png)

在 **[!UICONTROL 审核摘要]** 选项卡

![review-summary](assets/configure-review6.png)

* `Review Path`

   输入或浏览到放置的实例 `reviews`要总结的组件，例如，如果添加到 [Geometrixx参与网站，](getting-started.md) 路径将为：

   `/content/sites/engage/en/page/jcr:content/content/primary/reviews`

* `Include histogram`

   如果选中，则显示一个条形图，指示所总结的评论中存在多少个星级。 默认值为未选中。

### 更改为自定义审核类型 {#changing-to-a-custom-review-type}

“审阅”组件使用注释系统。

通过更改评论资源类型，评论系统不再使用默认选项生成评论的实例，而是由开发人员自定义（扩展）的实例。

在已知自定义资源类型后，输入 [设计模式](../../help/sites-authoring/default-components-designmode.md) 并双击所放置的 `Comments` 组件打开带有附加选项卡的对话框。

在 **[!UICONTROL 资源类型]** 选项卡，为的新实例指定自定义资源类型 `Comments or Voting` 组件：

![评论投票](assets/configure-review7.png)

* **[!UICONTROL 评论资源类型]**

   导航到扩展的资源类型 `comment`/apps中的组件（单个注释）。 例如：`/apps/social/commons/components/hbs/comments/comment`。

   此资源将标识访客发表评论时创建的UGC的resourceType。

* **[!UICONTROL 投票资源类型]**

   导航到扩展的资源类型 `voting`/apps中的组件 例如：`/apps/social/components/hbs/voting`。

   此资源将标识访客发表投票时创建的UGC的资源类型。

* **[!UICONTROL 评论系统资源类型]**

   导航到扩展的资源类型 `comments`/apps中的组件（注释系统）。 除非页面模板，否则保留为空 [动态包括](scf.md#add-or-include-a-communities-component) 基础脚本中的注释系统，而不是作为资源（注释节点）添加到页面中。 通过阅读有关 [{{include}} 辅助函数](handlebars-helpers.md#include).

## 网站访客体验 {#site-visitor-experience}

### 版主和管理员 {#moderators-and-administrators}

当登录用户具有审阅人或管理员权限时，无论审阅的作者是谁，他们都能执行组件配置允许的审阅任务。

### 成员 {#members}

当站点访客登录时，根据配置，他们可能：

* 发布新审核
* 编辑他们自己的评论
* 删除他们自己的审核
* 标记其他人的审阅注释

每个成员只允许一个评级。 会员可以随时变更等级。

### 匿名 {#anonymous}

未登录的网站访客只能阅读已发布的评论，如果支持则进行翻译，但不得添加评级或评论，也不得标记其他人的评论意见。

## 附加信息 {#additional-information}

欲知更多信息，请访问 [查看Essentials](reviews-basics.md) 适用于开发人员的页面。

有关审核已发布的评论，请参阅 [审核用户生成的内容](moderate-ugc.md).

有关已发布评论的翻译，请参阅 [翻译用户生成的内容](translate-ugc.md).
