---
title: 登录页面
seo-title: Landing Pages
description: 利用登陆页面功能，可以快速轻松地将设计和内容直接导入AEM页面。 Web开发人员可以准备HTML和其他资源，这些资源可以导入为完整页面或仅页面的一部分。
seo-description: The landing pages feature allows quick and easy importing of a design and content right into an AEM page. A web developer can prepare the HTML and additional assets that can be imported as a full page or only a part of a page.
uuid: b294c43f-63ae-4b5b-bef0-04566e350b63
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: 061dee36-a3bb-4166-a9c1-3ab7e4de1d1d
docset: aem65
exl-id: 0f1014a7-b0ba-4455-b3a4-5023bcd4c5a1
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '3335'
ht-degree: 1%

---

# 登录页面{#landing-pages}

利用登陆页面功能，可以快速轻松地将设计和内容直接导入AEM页面。 Web开发人员可以准备HTML和其他资源，这些资源可以导入为完整页面或仅页面的一部分。 功能对于创建仅在有限的时间内处于活动状态且需要快速创建的营销登陆页面非常有用。

本页介绍以下内容：

* AEM中的登陆页面（包括可用组件）外观
* 如何创建登陆页面以及如何导入设计包
* 如何在AEM中使用登陆页面
* 如何设置移动登陆页面

中介绍了如何准备设计包以进行导入 [扩展和配置设计导入程序](/help/sites-administering/extending-the-design-importer-for-landingpages.md). 中介绍了与Adobe Analytics集成 [将登陆页面与Adobe Analytics集成。](/help/sites-administering/integrating-landing-pages-with-adobe-analytics.md)

>[!CAUTION]
>
>设计导入器，用于导入登陆页面， [已在AEM 6.5中弃用](/help/release-notes/deprecated-removed-features.md#deprecated-features).

>[!CAUTION]
>
>因为设计导入程序需要访问 `/apps`，它无法在容器化的云环境中工作，其中 `/apps` 不可变。

## 什么是登陆页面？ {#what-are-landing-pages}

登陆页面是作为营销推广“端点”的单页面或多页面网站 — 例如，电子邮件、广告词/横幅、社交媒体。 登陆页面有多种用途，但都有一个共同点 — 访客应完成一项任务，并定义登陆页面成功与否。

利用AEM中的登陆页面功能，营销人员可与代理机构或内部创意团队的Web设计人员合作，创建可轻松导入AEM且仍可由营销人员编辑的页面设计，并在与其他AEM支持的网站相同的治理下发布。

在AEM中，您可以通过执行以下步骤来创建登陆页面：

1. 在AEM中创建一个包含登陆页面画布的页面。 AEM附带了一个示例，名为 **导入程序页面**.

1. [准备HTML和资源。](/help/sites-administering/extending-the-design-importer-for-landingpages.md)
1. 将资源打包到一个ZIP文件中，此处称为设计包。
1. 在导入程序页面上导入设计包。
1. 修改并发布页面。

### 桌面登陆页面 {#desktop-landing-pages}

AEM中的示例登陆页面如下所示：

![chlimage_1-2](assets/chlimage_1-2.jpeg)

### 移动设备登陆页面 {#mobile-landing-pages}

登陆页面也可以具有页面的移动版本。 要获得单独的登陆页面移动版本，导入设计必须具有两个html文件： *index.htm(l)* 和 *mobile.index.htm(l)*.

登陆页面的导入过程与正常登陆页面的导入过程相同，登陆页面设计还有一个与移动登陆页面对应的附加html文件。 此html文件也必须具有画布 `div` 替换为 `id=cqcanvas` 与桌面登陆页面html一样，它支持针对桌面登陆页面描述的所有可编辑组件。

移动设备登陆页面作为桌面登陆页面的子页面创建。 要打开它，请导航到网站中的登陆页面，然后打开子页面。

![chlimage_1-22](assets/chlimage_1-22.png)

>[!NOTE]
>
>如果删除或停用桌面登陆页面，则移动登陆页面将随桌面登陆页面一起删除/停用。

## 登陆页面组件 {#landing-page-components}

要使导入的HTML部分在AEM中可编辑，您可以将“登陆页面”HTML中的内容直接映射到AEM组件。 设计导入程序了解以下组件（默认情况下）：

* 文本，用于任何文本
* 标题，用于H1-6标记中的内容
* 图像，用于应该可替换的图像
* 行动号召：

   * 点进链接
   * 图形链接

* CTA潜在客户表单，用于捕获用户信息
* 段落系统(Parsys)，允许添加任何组件，或转换上述组件

此外，还可以扩展此功能并支持自定义组件。 本节详细介绍了这些组件。

### 文本 {#text}

文本组件允许您使用WYSIWYG编辑器输入文本块。 参见 [文本组件](/help/sites-authoring/default-components.md#text) 了解更多信息。

![chlimage_1-23](assets/chlimage_1-23.png)

以下是登陆页面上的文本组件示例：

![chlimage_1-24](assets/chlimage_1-24.png)

#### 标题 {#title}

利用标题组件，可显示标题并配置大小(h1-6)。 参见 [标题组件](/help/sites-authoring/default-components.md#title) 了解更多信息。

![chlimage_1-25](assets/chlimage_1-25.png)

以下是登陆页面上的标题组件示例：

![chlimage_1-26](assets/chlimage_1-26.png)

#### 图像 {#image}

图像组件显示一个图像，您可以从内容查找器拖放或单击该图像以上传。 参见 [图像组件](/help/sites-authoring/default-components.md) 了解更多信息。

![chlimage_1-27](assets/chlimage_1-27.png)

以下是登陆页面上的图像组件示例：

![chlimage_1-28](assets/chlimage_1-28.png)

#### 行动号召(CTA) {#call-to-action-cta}

登陆页面设计可能具有多个链接 — 其中一些链接可能旨在作为“行动号召”。

行动号召(CTA)用于让访客在登陆页面上立即采取行动，例如“立即订阅”、“查看此视频”、“仅限定时间”等。

* 点进链接 — 允许您添加文本链接，单击该链接会将访客转到目标URL。
* 图形链接 — 允许您添加图像，单击该图像可将访客转到目标URL。

两个CTA组件具有类似的选项。 点进链接具有其他富文本选项。 以下段落详细介绍了这些组件。

#### 点进链接 {#click-through-link}

此CTA组件可用于在登陆页面上添加文本链接。 可以单击该链接以将用户转到组件属性中指定的目标URL。 它是“行动号召”小组的一部分。

![chlimage_1-29](assets/chlimage_1-29.png)

**标签** 用户看到的文本。 您可以使用富文本编辑器修改格式。

**目标URL** 输入用户单击文本时要访问的URI。

**渲染选项** 描述渲染选项。 您可以从以下选项中进行选择：

* 在新浏览器窗口中加载页面
* 在当前窗口中加载页面
* 在父框架中加载页面
* 取消所有框架，并在整个浏览器窗口中加载页面

**CSS** 在“样式”选项卡上，输入CSS样式表的路径。

**ID** 在样式选项卡上，输入组件的ID以对其进行唯一标识。

以下是点进链接的示例：

![chlimage_1-30](assets/chlimage_1-30.png)

#### 图形链接 {#graphical-link}

此CTA组件可用于添加登陆页面上带有链接的任何图形图像。 图像可以是简单的按钮或任何图形图像作为背景。 单击图像时，用户将被转到组件属性中指定的目标URL。 它是 **行动号召** 组。

![chlimage_1-31](assets/chlimage_1-31.png)

**标签** 用户在图形中看到的文本。 您可以使用富文本编辑器修改格式。

**目标URL** 输入用户单击图像时要访问的URI。

**渲染选项** 描述渲染选项。 您可以从以下选项中进行选择：

* 在新浏览器窗口中加载页面
* 在当前窗口中加载页面
* 在父框架中加载页面
* 取消所有框架，并在整个浏览器窗口中加载页面

**CSS** 在“样式”选项卡上，输入CSS样式表的路径。

**ID** 在样式选项卡上，输入组件的ID以对其进行唯一标识。

以下是示例图形链接：

![chlimage_1-32](assets/chlimage_1-32.png)

### 行动动员(CTA)潜在客户表单 {#call-to-action-cta-lead-form}

商机表单是用于收集访客/商机的配置文件信息的表单。 此信息可以存储并用于以后根据此信息执行有效的营销。 此信息通常包括标题、姓名、电子邮件、出生日期、地址、兴趣等。 它是 **CTA潜在客户表单** 组。

CTA潜在客户表单的示例如下所示：

![chlimage_1-33](assets/chlimage_1-33.png)

CTA潜在客户表单由多个不同的组件组成：

* **潜在客户表单**
商机表单组件定义页面上新商机表单的开始和结束。 然后，其他组件可以置于这些元素之间，例如电子邮件ID、名字等。

* **表单字段和元素**
表单字段和元素可以包括文本框、单选按钮、图像等。 用户通常会在表单字段中完成一项操作，例如键入文本。 有关更多信息，请参阅各个表单元素。

* **配置文件组件**
配置文件组件与用于社交协作和需要访客个性化的其他领域的访客配置文件相关。

前文显示了一个示例表单；它由 **潜在客户表单** 组件（开始和结束），带 **名字** 和 **电子邮件ID** 用于输入和的字段 **提交** 字段

在sidekick中，以下组件可用于CTA潜在客户表单：

![chlimage_1-34](assets/chlimage_1-34.png)

#### 许多潜在客户表单组件的通用设置 {#settings-common-to-many-lead-form-components}

尽管每个潜在客户表单组件的用途各不相同，但许多表单组件由类似的选项和参数组成。

配置任何表单组件时，对话框中提供了以下选项卡：

* **标题和文本**
在此，您需要指定基本信息，例如组件的标题和任何随附文本。 在适当的情况下，它还允许您定义其他关键信息，例如字段是否可多选，以及是否可供选择的项。

* **初始值**
用于指定默认值。

* **约束**
您可以在此指定是否需要字段并将约束放置在该字段上（例如，必须为数字等）。

* **样式**
指示字段的大小和样式。

>[!NOTE]
>
>您看到的字段因各个组件而异。
>
>并非所有选项都可用于所有潜在客户表单组件。 请参阅Forms以了解关于这些方面的更多信息 [通用设置](/help/sites-authoring/default-components.md#formsgroup).

#### 潜在客户表单组件 {#lead-form-components}

以下部分介绍了可用于行动号召潜在客户表单的组件。

**关于** 允许用户添加关于信息。

![chlimage_1-35](assets/chlimage_1-35.png)

**地址字段** 允许用户输入地址信息。 配置此组件时，必须在对话框中输入元素名称。 元素名称是表单元素的名称。 这指示数据存储到存储库中的什么位置。

![chlimage_1-36](assets/chlimage_1-36.png)

**出生日期** 用户可以输入出生日期信息。

![chlimage_1-37](assets/chlimage_1-37.png)

**电子邮件ID** 允许用户输入电子邮件地址（标识）。

![chlimage_1-38](assets/chlimage_1-38.png)

**名字** 提供一个字段，供用户输入其名字。

![chlimage_1-39](assets/chlimage_1-39.png)

**性别** 用户可以从下拉列表中选择其性别。

![chlimage_1-40](assets/chlimage_1-40.png)

**姓氏** 用户可以输入姓氏信息。

![chlimage_1-41](assets/chlimage_1-41.png)

**潜在客户表单** 添加此组件以将潜在客户表单添加到登陆页面。 潜在客户表单自动包含“潜在客户表单的开始”和“潜在客户表单的结束”字段。 在中，您添加本节中介绍的Lead Form组件。

![chlimage_1-42](assets/chlimage_1-42.png)

Lead Form组件使用 **表单开始** 和 **表单结尾** 元素。 它们始终是配对的，以确保正确定义了表单。

添加潜在客户表单后，您可以通过单击配置表单的开头或结尾 **编辑** 在相应的栏中。

**潜在客户表单的开头**

两个选项卡可用于配置 **表单** 和 **高级**：

![chlimage_1-43](assets/chlimage_1-43.png)

**感谢页面** 要引用以感谢访客提供其输入的页面。 如果留空，表单会在提交后重新显示。

**启动工作流** 确定在提交潜在客户表单后触发的工作流。

![chlimage_1-44](assets/chlimage_1-44.png)

**帖子选项** 以下帖子选项可用：

* 创建潜在客户
* 电子邮件服务：创建订阅者并添加到列表 — 如果您使用的是ExactTarget等电子邮件服务提供程序，则使用。
* 电子邮件服务：发送自动回复电子邮件 — 如果您使用的是ExactTarget等电子邮件服务提供程序，则使用。
* 电子邮件服务：从列表中取消订阅用户 — 如果您使用的是ExactTarget等电子邮件服务提供程序，则使用。
* 取消订阅用户

**表单标识符** 表单标识符唯一地标识潜在客户表单。 如果单个页面上有多个表单，请使用表单标识符；请确保它们具有不同的标识符。

**加载路径** 是节点属性的路径，用于将预定义值加载到潜在客户表单字段中。

这是一个可选字段，用于指定存储库中节点的路径。 如果此节点具有匹配字段名称的属性，则表单上的相应字段将预加载这些属性的值。 如果不存在匹配项，则字段包含默认值。

**客户端验证** 指示此表单是否需要客户端验证（始终进行服务器验证）。 这可以与Forms Captcha组件一起实现。

**验证资源类型** 如果要验证整个潜在客户表单（而不是单个字段），请定义表单验证资源类型。

如果您要验证完整的表单，还应包括以下内容之一：

* 用于客户端验证的脚本：
   ` /apps/<myApp>/form/<myValidation>/formclientvalidation.jsp`

* 用于服务器端验证的脚本：
   ` /apps/<myApp>/form/<myValidation>/formservervalidation.jsp`

**操作配置** 根据“发布选项”中的选择，操作配置会发生变化。 例如，如果选择Create Lead ，则可以配置要将Lead添加到哪个列表中。

![chlimage_1-45](assets/chlimage_1-45.png)

* **显示提交按钮**
指示是否显示提交按钮。

* **提交名称**
标识符（如果您在表单中使用多个提交按钮）。

* **提交标题**
按钮上显示的名称，如“提交”或“发送”。

* **显示重置按钮**
选中此复选框可使“重置”按钮可见。

* **重置标题**
“重置”按钮上显示的名称。

* **描述**
按钮下方显示的信息。

## 创建登陆页面 {#creating-a-landing-page}

创建登陆页面时，您需要执行三个步骤：

1. 创建导入程序页面。
1. [准备要导入的HTML。](/help/sites-administering/extending-the-design-importer-for-landingpages.md)
1. 导入设计包。

### 使用设计导入程序 {#use-of-the-design-importer}

由于导入页面涉及准备HTML、验证和测试页面，因此导入登陆页面是一项管理员任务。 作为管理员，执行导入的用户需要拥有对的读取、写入、创建和删除权限 `/apps`. 如果用户没有这些权限，导入将失败。

>[!NOTE]
>
>由于设计导入程序旨在作为管理工具，需要对进行读取、写入、创建和删除 `/apps`，Adobe建议不要在生产中使用设计导入程序。

Adobe建议在暂存实例上使用设计导入程序。 在暂存实例上，可以由开发人员测试和验证导入，然后开发人员负责将代码部署到生产实例。

### 创建导入程序页面 {#creating-an-importer-page}

在导入登陆页面设计之前，您需要创建一个导入程序页面，例如在营销策划下。 通过“导入者页面”模板，您可以导入完整的HTML登录页面。 该页面包含一个拖放框，可在其中使用拖放功能导入登陆页面设计包。

>[!NOTE]
>
>默认情况下，导入程序页面只能在营销活动下创建，但您也可以叠加此模板以在下创建登陆页面 `/content/mysite`.

要创建新登陆页面，请执行以下操作：

1. 转到 **网站** 控制台。
1. 在左窗格中选择您的营销策划。
1. 单击 **新** 以打开 **创建页面** 窗口。
1. 选择 **导入程序页面** 模板，添加标题和（可选）名称，然后单击 **创建**.

   ![chlimage_1-1-1](assets/chlimage_1-1-1.png)

   此时将显示您的新导入程序页面。

### 准备HTML以进行导入 {#preparing-the-html-for-import}

在导入设计包之前，需要准备HTML。 参见 [扩展和配置设计导入](/help/sites-administering/extending-the-design-importer-for-landingpages.md) 了解更多信息。

### 导入设计包 {#importing-the-design-package}

创建导入程序页面后，您可以在其上导入设计包。 有关创建设计包及其推荐结构的详细信息，请参阅 [扩展和配置设计导入](/help/sites-administering/extending-the-design-importer-for-landingpages.md).

假定设计包已准备就绪，则以下步骤将描述如何将设计包导入到导入程序页面。

1. 打开导入程序页面，您可以 [创建时间较早](#creatingablankcanvaspage).

   ![chlimage_1-46](assets/chlimage_1-46.png)

1. 将设计包拖放到投箱上。 请注意，当将包拖动到上面时，箭头会改变方向。
1. 拖放后，您会看到登陆页面来代替导入程序页面。 您的HTML登录页面已成功导入。

   ![chlimage_1-2-1](assets/chlimage_1-2-1.png)

>[!NOTE]
>
>在导入时，出于安全原因并且为了避免导入和发布无效标记，将清除标记。 这假定仅HTML标记以及所有其他形式的元素(例如内联SVG或Web组件)将被过滤掉。

>[!NOTE]
>
>如果您在导入设计包时遇到问题，请参阅 [疑难解答](/help/sites-administering/extending-the-design-importer-for-landingpages.md#troubleshooting).

## 使用登陆页面 {#working-with-landing-pages}

登陆页面的设计和资产通常由设计人员通过他们常用的工具(如Adobe Photoshop或Adobe Dreamweaver)在代理商处创建。 设计完成后，设计人员会向营销人员发送一个包含所有资产的zip文件。 随后，营销中的联系人负责将zip文件放入AEM中并发布内容。

此外，设计者可能需要在导入登陆页面后对其进行修改，方法是编辑或删除内容并配置行动号召组件。 最后，营销人员将需要预览登陆页面，然后激活营销活动以确保发布登陆页面。

本节介绍如何执行以下操作：

* 删除登陆页面
* 下载设计包
* 查看导入信息
* 重置登陆页面
* [配置CTA组件并将内容添加到页面](#call-to-action-cta)
* 预览登陆页面
* 激活/发布登陆页面

导入设计包时， **清除设计** 和 **下载导入的压缩文件** 在页面的设置菜单中提供：

![chlimage_1-3-1](assets/chlimage_1-3-1.png)

### 下载导入的设计包 {#downloading-the-imported-design-package}

通过下载zip文件，您可以记录使用特定登陆页面导入的zip文件。 请注意，对页面所做的更改不会添加到zip文件中。

要下载导入的设计包，请单击 **下载Zip** （在登陆页面工具栏中）。

### 查看导入信息 {#viewing-import-information}

您可以随时在经典用户界面中单击登陆页面顶部的蓝色感叹号，以查看有关上次导入的信息。

![chlimage_1-47](assets/chlimage_1-47.png)

如果导入的设计包存在一些问题，例如，如果它引用的图像/脚本在包中不存在，等等，则设计导入程序会以列表的形式显示此类问题。 要查看问题列表，请在经典的用户界面中，单击登陆页面工具栏中的问题链接。 在下图中，单击 **问题** 链接将打开“导入问题”窗口。

![chlimage_1-3](assets/chlimage_1-3.jpeg)

### 重置登陆页面 {#resetting-a-landing-page}

如果您在对登陆页面设计包进行某些更改后想要重新导入该设计包，则可以通过单击 **清除** ，或者单击触控优化用户界面中设置菜单中的清除。 这样做会删除导入的登陆页面并创建一个空白的导入程序页面。

清除登陆页面时，您可以删除内容更改。 如果您单击 **否**，则保留内容更改，即下的结构 `jcr:content/importer`将保留，并且只保留导入程序页面组件和中的资源 `etc/design` 将被删除。 但是，如果您单击 **是**，则 `jcr:content/importer` 也会被删除。

>[!NOTE]
>
>如果决定删除内容更改，则您在导入的登陆页面上所做的所有更改以及所有页面属性都将在单击时丢失 **清除**.

### 在登陆页面上修改和添加组件 {#modifying-and-adding-components-on-a-landing-page}

要在登陆页面上修改组件，请双击组件以打开它们，然后像编辑任何其他组件一样进行编辑。

要在登陆页面上添加组件，请将组件拖放到登陆页面（从经典用户界面中的Sidekick或从触屏优化用户界面中的“组件”窗格），然后进行相应编辑。

>[!NOTE]
>
>如果登陆页面上的某个组件无法编辑，则需要在以下时间后重新导入zip文件 [修改HTML文件。](/help/sites-administering/extending-the-design-importer-for-landingpages.md) 这意味着在导入期间，不可编辑的部件未转换为AEM组件。

### 删除登陆页面 {#deleting-a-landing-page}

删除登陆页面的操作与删除普通AEM页面的操作类似。

唯一的例外是，当您删除桌面登陆页面时，它也会删除相应的移动设备登陆页面（如果存在），但反之则不会。

### 发布登陆页面 {#publishing-a-landing-page}

您可以发布登陆页面及其所有依赖项，就像发布普通页面一样。

>[!NOTE]
>
>发布桌面登陆页面时，还会发布其相应的移动设备版本（如果有）。 但是，发布移动设备登陆页面不会发布桌面版本。
