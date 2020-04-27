---
title: 使用审阅和审阅摘要（显示）
seo-title: 使用审阅和审阅摘要（显示）
description: 将“审阅”和“审阅摘要”组件添加到页面
seo-description: 将“审阅”和“审阅摘要”组件添加到页面
uuid: bd1ccee7-b26b-4a27-b1ea-89609f5080af
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: bf4e7809-8def-4647-aaa6-3ac36865511f
translation-type: tm+mt
source-git-commit: 62f2a11491e427a13cecae75c225ed41a44783cd

---


# 使用审阅和审阅摘要（显示） {#using-reviews-and-reviews-summary-display}

该组 `Reviews` 件是可供使用的 [评论和](comments.md) 评级组 [件的组合](rating.md) 。

该组 `Reviews Summary (Display)` 件提供组件的活动或关闭实例的摘要，以 `Reviews` 便在站点的其他位置显示。

>[!NOTE]
>
>不支持匿名发布审阅。 站点访客必须注册（成为会员）并登录以参与。 已签署的访客可随时更新其审阅。


## Adding a Review to a Page {#adding-a-review-to-a-page}

要在创作模 `Reviews``Communities / Reviews` 式下将组件添加到页面，请使用组件浏览器在页面上查找并将其拖动到相应位置，如相对于要供用户查看的功能的位置。

有关必要的信息，请访 [问社区组件基础](basics.md)。

当包含 [所需的客户端库时](reviews-basics.md#essentials-for-client-side) ，组件的显示 `Reviews`方式为此。

![chlimage_1-344](assets/chlimage_1-340.png)

## 配置审阅 {#configuring-reviews}

选择要访问 `Reviews` 的已放置组件，然后选择打 `Configure` 开编辑对话框的图标。

![chlimage_1-341](assets/chlimage_1-341.png)

在“允 **[!UICONTROL 许的评级]** ”选项卡下，指定要向成员显示的评级的完整列表。 第一个评级应是总体／一般评级，因为它是提供组件平均评级的评 `Review Summary (Display)` 级。 默认配置中的后两个评级应指定不同的标题，而不是“Subrating 1”或“Subrating 2”。

![chlimage_1-342](assets/chlimage_1-342.png)

* **[!UICONTROL 允许的评级]**

   一个评级列表，成员可从中进行选择。

   使用向上箭头、向下箭头和删除按钮可修改可见的选择。

   单击 **[!UICONTROL 添加项目]** ，以添加其他评级选择。

在“必 **[!UICONTROL 需评级]** ”选项卡下，从“允许评级”列表中重新输入 **[!UICONTROL 需要评级的项]** 。 如果某个项目仅在“允许的评级”选项卡上指定，则该项目在由成员提交时可能会保持无标记状态。

在网站上，必需评级标有星号。 如果某个项目是必需的并且未标记，则会向成员显示一条消息，并且在标记所有必需评级之前拒绝提交。

![chlimage_1-343](assets/chlimage_1-343.png)

* **[!UICONTROL 所需的评级]**

   允许的评级的子集，指示需要哪些评级。

   使用向上箭头、向下箭头和删除按钮可修改可见的选择。

   单击 **[!UICONTROL 添加项目]** ，以添加其他响应选项。

>[!NOTE]
>
>如果在“必需评级 ******** ”选项卡上输入的项目未在“允许的评级”选项卡上指定，则该项目不会包含在要评级的项目中。


在“审 **[!UICONTROL 阅]** ”选项卡下，指定如何处理审阅。

![chlimage_1-344](assets/chlimage_1-344.png)

* **[!UICONTROL 允许回复]**

   如果选中此项，则允许回复审阅。 默认为未选中。

* **[!UICONTROL 关闭]**

   如果选中此项，则审阅将不再向新审阅和回复发送。 默认为未选中。

* **[!UICONTROL 允许文件上传]**

   如果选中此项，则允许上传文件附件以供审阅。 默认为未选中。

* **最大文件大小&#x200B;**

   仅在选中“允许 **[!UICONTROL 文件上传]** ”时相关。 此字段限制已上载文件的大小（以字节为单位）。 默认为10 MB。

* **[!UICONTROL 最大消息长度]**

   可输入到文本框中的最大字符数。 默认为4096个字符。

* **[!UICONTROL 允许的文件类型]**

   仅在选中“允许 **[!UICONTROL 文件上传]** ”时相关。 以逗号分隔的文件扩展名列表（以“点”分隔）。 例如：.jpg、.jpeg、.png、.doc、.docx、.pdf。 如果指定了任何文件类型，则不允许指定那些未指定的文件类型。 默认值未指定，因此允许所有文件类型。

* **[!UICONTROL 富文本编辑器]**

   如果选中此项，则可以使用标记输入帖子。 默认为未选中。

* **[!UICONTROL 允许投票]**

   如果选中此项，则包含主题的投票功能。 默认为未选中。

在“用户 **[!UICONTROL 审核]** ”选项卡下，指定如何管理已发布的审阅。 有关详细信息，请参阅 [审核用户生成的内容](moderate-ugc.md)。

![chlimage_1-345](assets/chlimage_1-345.png)

* **[!UICONTROL 预审]**

   如果选中此项，则审阅必须经过批准，才能显示在发布站点上。 默认为未选中。

* **[!UICONTROL 删除审阅]**

   如果选中此项，则向发布审阅的成员提供删除该审阅的功能。 默认为未选中。

* **[!UICONTROL 拒绝审阅]**

   如果选中此项，则允许版主拒绝审阅。 默认为未选中。

* **[!UICONTROL 关闭／重新打开审阅]**

   如果选中此项，则允许版主关闭并重新打开审阅。 默认为未选中。

* **[!UICONTROL 标记审阅]**

   如果选中此项，允许成员将审阅标记为不合适。 默认为未选中。

* **[!UICONTROL 旗标原因列表]**

   如果选中此项，允许成员从下拉式列表中选择其将审阅标记为不适当的理由。 默认为未选中。

* **[!UICONTROL 自定义标志原因]**

   如果选中此项，则允许成员输入自己将审阅标记为不适当的原因。 默认为未选中。

* **[!UICONTROL 协调阈值]**

   输入在通知审核者之前必须由成员标记审阅的次数。 默认值是一次(1)。

* **[!UICONTROL 标记限制]**

   输入审核在隐藏于公共视图之前必须标出的次数。 此数字必须大于或等于审核 **[!UICONTROL 阈值]**。 默认为5。

### 向页面添加审阅摘要（显示） {#adding-a-review-summary-display-to-a-page}

要在创作模 `Reviews Summary (Display)` 式下将组件添加到页面，请找到该组件

* `Communities / Reviews Summary (Display)`

并将其拖动到要显示活动或已关闭审阅摘要的页面上的位置。

有关必要的信息，请访 [问社区组件基础](basics.md)。

当包含 [所需的客户端库时](reviews-basics.md#essentials-for-client-side) ，组件的显示 `Reviews Summary (Display)`方式为此。

![chlimage_1-346](assets/chlimage_1-346.png)

>[!NOTE]
>
>“平均值”反映摘要审阅的“允许的评级”选项卡上列出的第一个项目的投票情况。


### 配置审阅摘要（显示） {#configuring-reviews-summary-display}

选择要访问 `Reviews Summary (Display)` 的已放置组件，然后选择打 `Configure` 开编辑对话框的图标。

![chlimage_1-347](assets/chlimage_1-347.png)

在“审阅摘 **[!UICONTROL 要”选项卡下]** 。

![chlimage_1-348](assets/chlimage_1-348.png)

* `Review Path`

   输入或浏览至组件的已放置实例进行 `reviews`汇总，例如，如果添加到 [Geometrixx Engage站点的网页，则路径将为](getting-started.md) :

   `/content/sites/engage/en/page/jcr:content/content/primary/reviews`

* `Include histogram`

   如果选中此项，则显示条形图，指示摘要审阅中每个星级的数量。 默认为未选中。

### 更改为自定义审阅类型 {#changing-to-a-custom-review-type}

“审阅”组件使用评论系统。

通过更改“注释资源类型”，注释系统将不再使用默认值生成注释实例，而是生成由开发人员自定义（扩展）的注释实例。

在自定义资源类型已知后，进入 [设计模式](../../help/sites-authoring/default-components-designmode.md) ,多次单击放置的组件以打 `Comments` 开包含其他选项卡的对话框。

在“资 **[!UICONTROL 源类型]** ”选项卡下，为组件的新实例指定自定义resourceType `Comments or Voting`:

![chlimage_1-349](assets/chlimage_1-349.png)

* **[!UICONTROL 评论资源类型]**

   导航到/apps中扩展组件( `comment`单个注释)的resourceType。 For example, `/apps/social/commons/components/hbs/comments/comment`.

   此资源将标识访客发布评论时创建的UGC的resourceType。

* **[!UICONTROL 投票资源类型]**

   导航到/apps中扩展组件 `voting`的resourceType。 For example, `/apps/social/components/hbs/voting`.

   此资源将标识在访客投票时创建的UGC的资源类型。

* **[!UICONTROL 注释系统资源类型]**

   导航到/apps中扩展组件( `comments`评论系统)的resourceType。 除非页面模板在基础脚 [本中动态包含](scf.md#add-or-include-a-communities-component) “注释系统”，而不是作为资源（注释节点）添加到页面，否则将留空。 阅读有关 [{{include}}帮助程序的更多信息](handlebars-helpers.md#include)。

## 站点访客体验 {#site-visitor-experience}

### 版主和管理员 {#moderators-and-administrators}

当登录用户具有审查方或管理员权限时，他们可以执行组件配置所允许的审核任务，而不管是谁创作了审核。

### 成员 {#members}

站点访客登录后，根据配置的不同，可能会

* 发布新审阅。
* 编辑他们自己的审阅。
* 删除他们自己的审阅。
* 标记其他人的审阅注释。

每个成员只允许一个评级。 会员可随时更改其评级。

### 匿名 {#anonymous}

未登录的网站访客只能阅读已发布的审阅，翻译这些审阅（如果支持），但不能添加评级或审阅，也不能标记他人的审阅注释。

## 附加信息 {#additional-information}

有关详细信息，请参阅面向开 [发人员的](reviews-basics.md) Review Essentials页面。

有关审核已发布的注释，请参阅审核 [用户生成的内容](moderate-ugc.md)。

有关已发布注释的翻译，请参阅 [翻译用户生成的内容](translate-ugc.md)。
