---
title: 使用审阅和审阅摘要（显示）
seo-title: Using Reviews and Reviews Summary (Display)
description: 将“审阅和审阅摘要”组件添加到页面
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
ht-degree: 3%

---

# 使用审阅和审阅摘要（显示） {#using-reviews-and-reviews-summary-display}

的 `Reviews` 组件是 [评论](comments.md) 和 [评级](rating.md) 组件已准备就绪，可供使用。

的 `Reviews Summary (Display)` 组件提供活动或关闭实例的摘要 `Reviews` 组件，以在网站的其他位置显示。

>[!NOTE]
>
>不支持匿名发布审阅。 网站访客必须注册（成为会员）并登录以参与。 已登录的访客可以随时更新其审阅。

## 向页面添加审阅 {#adding-a-review-to-a-page}

添加 `Reviews` 组件添加到创作模式下的页面，可使用组件浏览器找到 `Communities / Reviews` 并将其拖动到页面上的适当位置，如相对于要供用户查看的功能的位置。

有关必要信息，请访问 [社区组件基础知识](basics.md).

当 [所需的客户端库](reviews-basics.md#essentials-for-client-side) 包含，这是 `Reviews` 组件。

![创建审阅](assets/create-review.png)

## 配置审阅 {#configuring-reviews}

选择已放置的 `Reviews` 要访问和选择的组件 `Configure` 图标，打开编辑对话框。

![configure-new](assets/configure-new.png)

在 **[!UICONTROL 允许的评级]** 选项卡，指定要向成员显示的评级的完整列表。 第一个评级应为整体/一般评级，因为它是提供 `Review Summary (Display)` 组件。 默认配置中的后两个评级应指定不同的标题，而不是“Subrating 1”或“Subrating 2”。

![允许评级](assets/configure-review1.png)

* **[!UICONTROL 允许的评级]**

   成员可从中选择的评级列表。

   使用向上箭头、向下箭头和删除按钮来修改可见的选择。

   单击 **[!UICONTROL 添加项目]** 添加其他评级选择。

在 **[!UICONTROL 必需评级]** 选项卡，从 **[!UICONTROL 允许的评级]** 需要评级的。 如果某个项目仅在允许的评级选项卡上指定，则在成员提交该项目时，该项目可能不会被标记。

在网站上，必需的评级标有星号。 如果某个项目是必需的并且未标记，则会向成员显示一条消息，并在标记所有必需评级之前拒绝提交。

![必需评级](assets/configure-review2.png)

* **[!UICONTROL 所需的评级]**

   允许的评级的子集，用于指示需要哪些评级。

   使用向上箭头、向下箭头和删除按钮来修改可见的选择。

   单击 **[!UICONTROL 添加项目]** 添加其他响应选项。

>[!NOTE]
>
>如果在 **[!UICONTROL 必需评级]** 选项卡 **[!UICONTROL 允许的评级]** 选项卡，则不会将其包含在要评级的项目中。

在 **[!UICONTROL 评论]** 选项卡，指定审阅的处理方式。

![审核](assets/configure-review3.png)

* **[!UICONTROL 允许回复]**

   如果选中此项，则允许回复审阅。 默认为未选中。

* **[!UICONTROL 关闭]**

   如果选中，则审阅将不再对新审阅和回复进行。 默认为未选中。

* **[!UICONTROL 允许文件上传]**

   如果选中此项，则允许上传文件附件以供审阅。 默认为未选中。

* **最大文件大小**

   仅在 **[!UICONTROL 允许文件上传]** 复选框。 此字段限制已上传文件的大小（以字节为单位）。 默认为10 MB。

* **[!UICONTROL 最大消息长度]**

   可在文本框中输入的最大字符数。 默认为4096个字符。

* **[!UICONTROL 允许的文件类型]**

   仅在 **[!UICONTROL 允许文件上传]** 复选框。 以逗号分隔的文件扩展名列表，其中带有“圆点”分隔符。 例如：.jpg、.jpeg、.png、.doc、.docx、.pdf。 如果指定了任何文件类型，则将不允许指定未指定的文件类型。 默认值未指定，以便允许使用所有文件类型。

* **[!UICONTROL 富文本编辑器]**

   如果选中此项，则可以输入带有标记的帖子。 默认为未选中。

* **[!UICONTROL 允许投票]**

   如果选中此项，则包含主题的投票功能。 默认为未选中。

在 **[!UICONTROL 用户审核]** 选项卡，指定如何管理已发布的审阅。 有关更多信息，请参阅 [审核用户生成的内容](moderate-ugc.md).

![用户审核](assets/configure-review4.png)

* **[!UICONTROL 预审]**

   如果选中此项，则必须先批准审阅，然后才能在发布网站上显示审阅。 默认为未选中。

* **[!UICONTROL 删除审阅]**

   如果选中，则发布审核的成员将能够删除审核。 默认为未选中。

* **[!UICONTROL 拒绝审阅]**

   如果选中，则允许审核者拒绝审阅。 默认为未选中。

* **[!UICONTROL 关闭/重新打开审阅]**

   如果选中，则允许审核者关闭并重新打开审阅。 默认为未选中。

* **[!UICONTROL 标记审阅]**

   如果选中，则允许成员将审阅标记为不适当。 默认为未选中。

* **[!UICONTROL 标记原因列表]**

   如果选中，则允许成员从下拉列表中选择其标记审阅不适当的原因。 默认为未选中。

* **[!UICONTROL 自定义标记原因]**

   如果选中，则允许成员输入自己将审阅标记为不适当的原因。 默认为未选中。

* **[!UICONTROL 审核阈值]**

   输入在通知审核者之前必须由成员标记审核的次数。 默认值为一次(1)。

* **[!UICONTROL 标记限制]**

   输入必须标记某个审阅才能将其隐藏在公共视图中的次数。 此数字必须大于或等于 **[!UICONTROL 审核阈值]**. 默认值为5。

### 向页面添加审阅摘要（显示） {#adding-a-review-summary-display-to-a-page}

添加 `Reviews Summary (Display)` 组件到创作模式下的页面，找到组件

* `Communities / Reviews Summary (Display)`

并将其拖动到要显示活动或已关闭审阅摘要的页面上。

有关必要信息，请访问 [社区组件基础知识](basics.md).

当 [所需的客户端库](reviews-basics.md#essentials-for-client-side) 包含，这是 `Reviews Summary (Display)`组件。

![审阅摘要](assets/configure-review5.png)

>[!NOTE]
>
>“平均值”反映在所汇总的审阅的“允许的评级”选项卡上列出的第一个项目的投票。

### 配置审阅摘要（显示） {#configuring-reviews-summary-display}

选择已放置的 `Reviews Summary (Display)` 要访问和选择的组件 `Configure` 图标，打开编辑对话框。

![配置](assets/configure-new.png)

在 **[!UICONTROL 查看摘要]** 选项卡

![审阅摘要](assets/configure-review6.png)

* `Review Path`

   输入或浏览到 `reviews`组件进行汇总，例如，如果添加到 [Geometrixx参与网站，](getting-started.md) 路径将为：

   `/content/sites/engage/en/page/jcr:content/content/primary/reviews`

* `Include histogram`

   如果选中，则包括条形图的显示，该条形图指示所汇总的评论中每个星级的多少。 默认为未选中。

### 更改为自定义审阅类型 {#changing-to-a-custom-review-type}

“审阅”组件使用评论系统。

通过更改注释资源类型，注释系统将不再使用默认值生成注释的实例，而是使用开发人员自定义（扩展）的实例。

在自定义资源类型已知后，输入 [设计模式](../../help/sites-authoring/default-components-designmode.md) 并双击已放置的 `Comments` 组件来打开一个包含其他选项卡的对话框。

在 **[!UICONTROL 资源类型]** 选项卡，为的新实例指定自定义resourceType `Comments or Voting` 组件：

![评论投票](assets/configure-review7.png)

* **[!UICONTROL 评论资源类型]**

   导航到扩展的resourceType `comment`组件（单个注释）。 例如：`/apps/social/commons/components/hbs/comments/comment`。

   此资源将识别访客发布评论时创建的UGC的resourceType。

* **[!UICONTROL 投票资源类型]**

   导航到扩展的resourceType `voting`组件。 例如：`/apps/social/components/hbs/voting`。

   此资源将确定访客发布投票时创建的UGC的资源类型。

* **[!UICONTROL 注释系统资源类型]**

   导航到扩展的resourceType `comments`组件（注释系统）。 留空，除非页面模板 [动态包含](scf.md#add-or-include-a-communities-component) 注释系统，而不是作为资源（注释节点）添加到页面中。 阅读 [{{include}} 助手](handlebars-helpers.md#include).

## 网站访客体验 {#site-visitor-experience}

### 审核者和管理员 {#moderators-and-administrators}

当登录用户具有审核者或管理员权限时，他们便能够执行组件配置所允许的审核任务，而不管是谁创作了审核。

### 成员 {#members}

网站访客登录后，根据配置的不同，他们可能会：

* 发布新审阅
* 编辑他们自己的审阅
* 删除其自己的审阅
* 标记他人的评论

每个成员只允许一个评级。 会员可随时更改其评级。

### 匿名 {#anonymous}

未登录的网站访客只能阅读已发布的评论，在受支持时翻译这些评论，但不得添加评级或评论，也不得标记其他评论。

## 附加信息 {#additional-information}

有关 [查看要点](reviews-basics.md) 页面。

有关审核已发布的评论，请参阅 [审核用户生成的内容](moderate-ugc.md).

有关已发布评论的翻译，请参阅 [翻译用户生成的内容](translate-ugc.md).
