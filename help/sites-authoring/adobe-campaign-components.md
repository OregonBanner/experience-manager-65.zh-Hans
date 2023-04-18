---
title: 与Adobe Campaign组件集成
description: 与Adobe Campaign集成后，在使用新闻稿和表单时，您会有可用的组件。
uuid: a858d5ca-aa6e-4bde-92db-a6dcd8b48ae6
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: personalization
discoiquuid: 9da34dab-7e89-4127-ab26-532687746b2a
docset: aem65
exl-id: d1132fcd-e6a0-44a2-8753-d250f68fbd78
source-git-commit: f4b6eb2ded17ec641f23a1fc3b977ce77169c8a1
workflow-type: tm+mt
source-wordcount: '2828'
ht-degree: 4%

---

# Adobe Campaign组件{#adobe-campaign-components}

与Adobe Campaign集成后，在使用新闻稿和表单时，您会有可用的组件。 本文档对这两种方法进行了描述。

>[!CAUTION]
>
>AEM电子邮件组件已弃用。 由于电子邮件的性质（将内容和样式合并在一起），AEM提供的现成电子邮件组件对客户的重复使用有限，因为需要在项目所需的任何组件中实施自定义样式。
>
>电子邮件组件可以在项目级别实施，已弃用的AEM电子邮件组件说明了如何实现这一点。 但是，不应在项目中使用这些已弃用的组件。

## Adobe Campaign新闻稿组件 {#adobe-campaign-newsletter-components}

所有营销活动组件都遵循 [电子邮件模板最佳实践](/help/sites-administering/best-practices-for-email-templates.md) 和基于Adobe标记语言 [HTL](https://helpx.adobe.com/cn/experience-manager/htl/using/overview.html).

当您打开配置为与Adobe Campaign集成的新闻稿/电子邮件时，您应会在 **Adobe Campaign新闻稿** 部分：

* 标题（营销活动）
* 图像（营销活动）
* 链接 (营销活动)
* Scene7 图像模板（营销活动）
* 目标引用（营销活动）
* 文本与图像（营销活动）
* 文本与个性化（营销活动）

以下部分介绍了这些组件。

这些组件如下所示：

![chlimage_1-43](assets/chlimage_1-43.png)

### 标题（营销活动） {#heading-campaign}

标题组件可以：

* 通过将 **标题** 字段。
* 显示您在 **标题** 字段。

您可以编辑 **标题（营销活动）** 组件。 留空将使用页面标题。

![chlimage_1-44](assets/chlimage_1-44.png)

您可以配置以下内容：

* **标题**
如果要使用页面标题以外的名称，请在此处输入该名称。

* **标题级别(1、2、3、4)**
基于HTML标题大小1-4的标题级别。

以下示例显示正在显示的标题（营销活动）组件。

![chlimage_1-45](assets/chlimage_1-45.png)

### 图像（营销活动） {#image-campaign}

图像（营销活动）组件根据指定的参数显示图像和随附文本。

您可以上传图像，然后对其进行编辑和处理（例如，裁剪、旋转、添加链接/标题/文本）。

您可以从 [资产浏览器](/help/sites-authoring/author-environment-tools.md#assetsbrowsertouchoptimizedui) 直接放到组件或其 [“配置”对话框](/help/sites-authoring/editing-content.md#editconfigurecopycutdeletepastetouchoptimizedui). 您还可以从“配置”对话框上传图像；此对话框还控制图像的所有定义和操作：

![chlimage_1-46](assets/chlimage_1-46.png)

>[!NOTE]
>
>您必须在 **替换文本** 字段，或无法保存图像。

上传图像后（而非之前），您可以使用 [就地编辑](/help/sites-authoring/editing-content.md#editcontenttouchoptimizedui) 要根据需要裁剪/旋转图像，请执行以下操作：

![](do-not-localize/chlimage_1-10.png)

>[!NOTE]
>
>就地编辑器在编辑时使用图像的原始大小和宽高比。 您还可以指定高度和宽度属性。 在保存编辑更改时，将应用属性中定义的任何大小和宽高比限制。
>
>根据您的实例，可能还会对 [页面设计](/help/sites-developing/designer.md);这些是在项目实施期间制定的。

在全屏编辑模式下，还有其他几个选项可供使用；例如，映射和缩放：

![](do-not-localize/chlimage_1-11.png)

加载图像后，您可以配置以下内容：

* **地图**
要映射图像，请选择“映射”。 您可以指定创建图像映射的方式（矩形、多边形等）以及区域应指向的位置。

* **裁切**
选择“裁剪”以裁剪图像。 使用鼠标裁剪图像。

* **旋转**
要旋转图像，请选择“旋转”。 反复使用，直到图像旋转到您想要的方式为止。

* **清除**
删除当前图像。

* 缩放栏（仅限经典选项）要放大和缩小图像，请使用图像下方的滑动栏（在“确定”和“取消”按钮上方）
* **标题**
图像的标题。

* **替换文本**
用于创建辅助内容时使用的替换文本。

* **链接到**
创建指向资产或您网站中其他页面的链接。

* **描述**
图像的描述。

* **大小**
设置图像的高度和宽度。

>[!NOTE]
>
>您必须在 **替换文本** 字段 **高级** 选项卡，或者无法保存图像，并且会看到以下错误消息：
>
>`Validation failed. Verify the values of the marked fields.`

以下示例展示了所显示的图像（营销活动）组件。

![chlimage_1-47](assets/chlimage_1-47.png)

### 链接 (营销活动) {#link-campaign}

链接（营销活动）组件允许您添加指向新闻稿的链接。

您可以在 **显示**, **URL信息**&#x200B;或 **高级** 选项卡：

* **链接标题**
链接的描述。 这是用户看到的文本。

* **链接工具提示**
添加有关如何使用链接的其他信息。

* **LinkType**
在下拉列表中，选择 
**自定义URL** 和 **自适应文档**. 此字段为必填字段. 如果选择自定义URL，则可以提供链接URL。 如果选择“自适应文档”，则可以提供文档路径。

* **其他URL参数**
添加任何其他URL参数。 单击添加项目可添加多个项目。

>[!NOTE]
>
>您必须在 **链接类型** 字段 **URL信息** 选项卡，或者无法保存组件，并且会看到以下错误消息：
>
>`Validation failed. Verify the values of the marked fields.`

以下示例展示了所显示的链接（营销活动）组件。

![chlimage_1-48](assets/chlimage_1-48.png)

### Dynamic Media Classic(Scene7)图像模板（营销活动） {#scene-image-template-campaign}

Dynamic Media Classic(Scene7)图像模板是分层的图像文件，其中的内容和属性可以参数化以实现可变性。 的 **[!UICONTROL 图像模板]** 组件允许您在新闻稿中使用Scene7模板，并更改模板参数的值。 此外，您还可以在参数中使用Adobe Campaign元数据变量，以便每个用户以个性化方式体验图像。

![chlimage_1-49](assets/chlimage_1-49.png)

单击 **编辑** 以配置组件。 您可以配置此部分中描述的设置。 此Scene7图像模板在 [Scene7图像模板组件](/help/assets/scene7.md#image-template).

此外，参数面板还列出了在Scene7中为模板定义的所有模板参数。 对于每个参数，您可以调整值、插入变量或将其重置为默认值。

![chlimage_1-50](assets/chlimage_1-50.png)

### 目标引用（营销活动） {#targeted-reference-campaign}

利用目标引用（营销活动）组件，可创建对目标段落的引用。

在此组件中，您导航到目标段落以将其选中。

单击文件夹图标可导航到要引用的段落。 完成后，单击复选标记。

### 文本与图像（营销活动） {#text-image-campaign}

文本与图像（营销活动）组件可添加文本块和图像。

单击以配置组件时，将选择文本或图像。

![chlimage_1-51](assets/chlimage_1-51.png)

选择 **文本** 显示内嵌编辑器：

![](do-not-localize/chlimage_1-12.png)

选择 **图像** 显示图像的就地编辑器：

![](do-not-localize/chlimage_1-13.png)

请参阅 [图像（营销活动）组件](#image-campaign) 以了解有关使用图像的更多信息。 请参阅 [文本与个性化（营销活动）组件](#text-personalization-campaign) 以了解有关使用文本的更多信息。

与文本与个性化（营销活动）和图像（营销活动）组件一样，您可以配置：

* **文本**
输入文本。 使用工具栏可修改格式、创建列表和添加链接。

* **图像**
从内容查找器中拖动图像，或单击以浏览到图像。 根据需要裁剪或旋转。

* **图像属性** (**高级图像属性**)允许您指定以下内容：

   * **标题**
块的标题；将由鼠标悬停显示。

   * **替换文本**
无法显示图像时要显示的替换文本。

   * **链接到**
创建指向资产或您网站中其他页面的链接。

   * **描述**
图像的描述。

   * **大小**
设置图像的高度和宽度。

>[!NOTE]
>
>的 **替换文本** 字段 **高级** 选项卡，或者组件无法保存，并且您会看到以下错误消息：
>
>`Validation failed. Verify the values of the marked fields.`

以下示例展示了所显示的文本与图像（营销活动）组件。

![chlimage_1-52](assets/chlimage_1-52.png)

### 文本与个性化（营销活动） {#text-personalization-campaign}

通过文本与个性化（营销活动）组件，您可以使用所见即所得(WYSIWYG)编辑器输入文本块，该编辑器的功能由 [富文本编辑器](/help/sites-authoring/rich-text-editor.md). 此外，此组件还允许您使用Adobe Campaign提供的上下文字段和个性化块；另请参阅 [插入个性化](/help/sites-authoring/campaign.md#inserting-personalization).

利用所选图标，可设置文本格式，包括字体特性、对齐方式、链接、列表和缩进。 在 [两个UI](/help/sites-authoring/editing-content.md)，但外观不同：

![chlimage_1-53](assets/chlimage_1-53.png)

在就地编辑器中，您可以添加文本、更改对齐方式、添加和删除链接、添加上下文字段或个性化块，以及进入全屏模式。 添加完文本/个性化后，选择复选标记以保存更改（或选择x以取消）。 请参阅 [就地编辑](/help/sites-authoring/editing-content.md#editcontenttouchoptimizedui) 以了解更多信息。

>[!NOTE]
>
>* 可用的个性化字段取决于您的新闻稿所链接到的Adobe Campaign模板。
>* 从ContextHub中选择角色后，个性化字段会自动替换为选定用户档案中的数据。
>
>请参阅 [插入个性化](/help/sites-authoring/campaign.md#inserting-personalization).

![chlimage_1-54](assets/chlimage_1-54.png)

>[!NOTE]
>
>仅在 **nms:seedMember** 架构或其某个扩展会被考虑在内。 链接到的表的属性 **nms:seedMember** 不可用。

## Adobe Campaign表单组件 {#adobe-campaign-form-components}

您可以使用Adobe Campaign组件创建用户填写的表单，以订阅新闻稿、取消订阅新闻稿，或更新其用户配置文件。 请参阅 [创建Adobe Campaign Forms](/help/sites-authoring/adobe-campaign-forms.md) 以了解更多信息。

每个组件字段都可以链接到Adobe Campaign数据库字段。 可用字段因其包含的数据类型而异，如部分所述 [组件和数据类型](#components-and-data-type). 如果在Adobe Campaign中扩展收件人架构，则数据类型匹配的组件中将提供新字段。

当您打开配置为与Adobe Campaign集成的表单时，您会在 **Adobe Campaign** 部分：

* 复选框（营销活动）
* 日期字段（营销活动）和日期字段/HTML5（营销活动）
* 已加密的主要密钥（营销活动）
* 错误显示（营销活动）
* 隐藏的对帐密钥（营销活动）
* 数字字段（营销活动）
* 选项字段（营销活动）
* 订阅核对清单（营销活动）
* 文本字段（营销活动）

这些组件如下所示：

![chlimage_1-55](assets/chlimage_1-55.png)

本节将详细介绍每个组件。

### 组件和数据类型 {#components-and-data-type}

下表介绍了可用于显示和修改Adobe Campaign配置文件数据的组件。 每个组件都可以映射到Adobe Campaign配置文件字段，以显示其值，并在提交表单时更新字段。 不同的组件只能匹配到相应数据类型的字段。

<table>
 <tbody>
  <tr>
   <td><p><strong>组件</strong></p> </td>
   <td><p><strong>Adobe Campaign字段的数据类型</strong></p> </td>
   <td><p><strong>示例字段</strong></p> </td>
  </tr>
  <tr>
   <td><p>复选框（营销活动）</p> </td>
   <td><p>布尔型</p> </td>
   <td><p>不再联系（通过任何渠道）</p> </td>
  </tr>
  <tr>
   <td><p>日期字段（营销活动）</p> <p>日期字段/HTML 5（营销活动）</p> </td>
   <td><p>日期</p> </td>
   <td><p>出生日期</p> </td>
  </tr>
  <tr>
   <td><p>数字字段（营销活动）</p> </td>
   <td><p>数字（字节、短、长、双）</p> </td>
   <td><p>年龄</p> </td>
  </tr>
  <tr>
   <td><p>选项字段（营销活动）</p> </td>
   <td><p>字节，关联值</p> </td>
   <td><p>性别</p> </td>
  </tr>
  <tr>
   <td><p>文本字段（营销活动）</p> </td>
   <td><p>字符串</p> </td>
   <td><p>电子邮件</p> </td>
  </tr>
 </tbody>
</table>

### 大多数组件通用的设置 {#settings-common-to-most-components}

Adobe Campaign组件具有所有组件（“已加密的主密钥”和“隐藏的对帐密钥”组件除外）中通用的设置。

在大多数组件中，您可以配置以下各项：

#### 标题与文本 {#title-and-text}

![chlimage_1-56](assets/chlimage_1-56.png)

* **标题**
如果要使用元素名称以外的名称，请在此处输入该名称。

* **隐藏标题**
如果您不希望显示标题，请选中此复选框。

* **描述**
向字段添加描述，以为用户提供更多信息。

* **仅显示值**
仅显示值（如果存在）

#### Adobe Campaign {#adobe-campaign}

您可以配置以下内容：

* **映射**
选择Adobe Campaign个性化字段（如果适用）。

* **协调键值**
如果此字段是协调键值的一部分，则选中此复选框。

![chlimage_1-57](assets/chlimage_1-57.png)

#### 约束 {#constraints}

* **必需** 选中此复选框可使此组件成为必需组件；即用户必须输入一个值。
* **必需消息** （可选）添加一条消息，说明字段为必填字段。

![chlimage_1-58](assets/chlimage_1-58.png)

#### 样式 {#styling}

* **CSS**
输入要用于此组件的CSS类。

![chlimage_1-59](assets/chlimage_1-59.png)

### 复选框（营销活动） {#checkbox-campaign}

通过复选框（营销活动）组件，用户可以修改具有布尔数据类型的Adobe Campaign配置文件字段。 例如，您可以有一个复选框（营销活动）组件，允许收件人指定不希望通过任何渠道联系他/她。

您可以 [配置大多数Adobe Campaign组件通用的设置](#settings-common-to-most-components) 复选框（营销活动）组件中。

以下示例显示正在显示的复选框（营销活动）组件。

![chlimage_1-60](assets/chlimage_1-60.png)

### 日期字段（营销活动）和日期字段/HTML5（营销活动） {#date-field-campaign-and-date-field-html-campaign}

使用日期字段允许收件人指定日期；例如，您可能希望收件人指定其出生日期。 日期格式与Adobe Campaign实例中使用的格式匹配。

除 [大多数Adobe Campaign组件通用的设置](#settings-common-to-most-components)，您可以配置以下内容：

* **约束 — 约束** 下拉列表您可以选择 —  **无** 或 **日期 —** 添加日期约束或不添加约束。 如果选择日期，则用户在字段中输入的答案必须采用日期格式。

* **约束消息** 此外，您还可以添加约束消息，以便用户了解如何正确设置其答案的格式。
* **样式 — 宽度** 通过单击或点按 **+** 和 **-** 图标或输入数字。

以下示例显示了显示调整了宽度的日期字段（营销活动）组件。

![chlimage_1-61](assets/chlimage_1-61.png)

### 已加密的主要密钥（营销活动） {#encrypted-primary-key-campaign}

此组件定义将包含Adobe Campaign配置文件标识符的URL参数的名称(**主资源标识符** 或 **已加密的主密钥** 在Adobe Campaign Standard和6.1中)。

显示和修改Adobe Campaign用户档案数据的每个表单 **必须** 包括已加密的主密钥组件。

您可以在已加密的主密钥（营销活动）组件中配置以下内容：

* **标题和文本 — 元素名称** 默认为encryptedPK。 仅当元素名称与表单上其他元素的名称冲突时，才需要更改该元素名称。 没有两个表单字段可以具有相同的元素名称。
* **Adobe Campaign - URL参数** 为EPK添加URL参数。 例如，您可以使用 **epk**.

以下示例显示正在显示的已加密的主密钥（营销活动）组件。

![chlimage_1-62](assets/chlimage_1-62.png)

### 错误显示（营销活动） {#error-display-campaign}

此组件允许您显示后端错误。 表单的错误处理需要设置为“转发”才能使组件正常工作。

以下示例展示了所显示的错误显示（营销活动）组件。

![chlimage_1-63](assets/chlimage_1-63.png)

### 隐藏的对帐密钥（营销活动） {#hidden-reconciliation-key-campaign}

隐藏的协调键值（营销活动）组件允许您将隐藏字段作为协调键值的一部分添加到表单。

您可以在隐藏的协调键值（营销活动）组件中配置以下内容：

* **标题和文本 — 元素名称** 默认为reconcilKey。 仅当元素名称与表单上其他元素的名称冲突时，才需要更改该元素名称。 没有两个表单字段可以具有相同的元素名称。
* **Adobe Campaign — 映射** 映射到Adobe Campaign个性化字段。

以下示例显示了所显示的隐藏的协调键值（营销活动）组件。

![chlimage_1-64](assets/chlimage_1-64.png)

### 数字字段（营销活动） {#numeric-field-campaign}

使用数字字段允许收件人输入数字，例如其年龄。

除 [大多数Adobe Campaign组件通用的设置](#settings-common-to-most-components)，您可以配置以下内容：

* **约束 — 约束** 下拉列表您可以选择 —  **无** 或 **数值 —** 添加数字约束或无约束。 如果选择数字，则用户在字段中输入的答案必须是数字。

* **约束消息** 此外，您还可以添加约束消息，以便用户了解如何正确设置其答案的格式。
* **样式 — 宽度** 通过单击或点按 **+** 和 **-** 图标或输入数字。

以下示例显示了配置了显示宽度的数字字段（营销活动）组件。

![chlimage_1-65](assets/chlimage_1-65.png)

### 选项字段（营销活动） {#option-field-campaign}

此下拉列表允许您选择一个选项；例如，收件人的性别或地位。

您可以 [配置大多数Adobe Campaign组件通用的设置](#settings-common-to-most-components) (在选项字段（营销活动）组件中)。 要填充下拉列表，请单击或点按Adobe Campaign个性化字段中的相应字段，然后导航到相应的字段。

![chlimage_1-66](assets/chlimage_1-66.png)

以下示例展示了所显示的选项字段（营销活动）组件。

![chlimage_1-67](assets/chlimage_1-67.png)

### 订阅核对清单（营销活动） {#subscriptions-checklist-campaign}

使用 **订阅核对清单（营销活动）** 用于修改与Adobe Campaign配置文件关联的订阅的组件。

添加到表单后，此组件会将所有可用的订阅显示为复选框，并允许用户选择所需的订阅。 用户提交表单时，此组件会根据表单操作类型(**Adobe Campaign:订阅服务** 或 **Adobe Campaign:取消订阅服务**)。

>[!NOTE]
>
>该组件不会检查用户已订阅/退订的服务。

您可以 [配置大多数Adobe Campaign组件通用的设置](#settings-common-to-most-components) (在订阅核对清单（营销活动）组件中)。 (没有可用于此组件的Adobe Campaign配置。)

以下示例展示了所显示的订阅核对清单（营销活动）组件。

![chlimage_1-68](assets/chlimage_1-68.png)

### 文本字段（营销活动） {#text-field-campaign}

用于输入字符串类型数据的文本字段（营销活动）组件，例如名字、姓氏、地址、电子邮件地址等。

除 [大多数Adobe Campaign组件通用的设置](#settings-common-to-most-components)，您可以配置以下内容：

* **约束 — 约束** 下拉列表您可以选择 —  **无，** **电子邮件**&#x200B;或 **名称** （无变音） — 添加电子邮件地址、名称或无约束的约束。 如果选择电子邮件，则用户在字段中输入的答案必须是电子邮件地址。 如果选择名称，则必须是名称（不允许变音）。

* **约束消息** 此外，您还可以添加约束消息，以便用户了解如何正确设置其答案的格式。
* **样式 — 宽度** 通过单击或点按 **+** 和 **-** 图标或输入数字。

以下示例显示正在显示的文本字段（营销活动）组件。

![chlimage_1-69](assets/chlimage_1-69.png)
