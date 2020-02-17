---
title: 登陆页面
seo-title: 登陆页面
description: 登陆页面功能可轻松快捷地将设计和内容准确地导入 AEM 页面。Web 开发人员可准备能够以完整页面或部分网页导入的 HTML 和额外资产。
seo-description: 登陆页面功能可轻松快捷地将设计和内容准确地导入 AEM 页面。Web 开发人员可准备能够以完整页面或部分网页导入的 HTML 和额外资产。
uuid: b294c43f-63ae-4b5b-bef0-04566e350b63
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: 061dee36-a3bb-4166-a9c1-3ab7e4de1d1d
docset: aem65
translation-type: tm+mt
source-git-commit: 016c705230dffec052c200b058a36cdbe0520fc4

---


# 登陆页面{#landing-pages}

登陆页面功能可轻松快捷地将设计和内容准确地导入 AEM 页面。Web 开发人员可准备能够以完整页面或部分网页导入的 HTML 和额外资产。该功能可有效地用于创建只在限定时段处于激活状态且需要快速创建的营销活动登录页面。

该页面讨论以下问题：

* 登陆页面（包括可用组件）在 AEM 中的外观
* 如何创建登陆页面，以及如何导入设计包
* 如何在 AEM 中处理登陆页面
* 如何设置移动登陆页面

有关如何准备要导入的设计包，请参阅[扩展和配置设计导入程序](/help/sites-administering/extending-the-design-importer-for-landingpages.md)中的相关介绍。有关如何与 Adobe Analytics 集成，请参阅[将登陆页面与 Adobe Analytics 集成](/help/sites-administering/integrating-landing-pages-with-adobe-analytics.md)中的相关介绍。

>[!CAUTION]
>
>[AEM 6.5](/help/release-notes/deprecated-removed-features.md#deprecated-features) 弃用了用于导入登陆页面的设计导入程序。

>[!CAUTION]
>
>Because the Design Importer requires access to `/apps`, it will not work in containerized cloud environments where `/apps` is immutable.

## What are Landing Pages? {#what-are-landing-pages}

登陆页面是作为营销推广活动“端点”的单页或多页站点 - 例如电子邮件、广告标语/横幅、社交媒体等。登陆页面具有多种用途，但所有这些用途都有一个共同点，那就是只有让访客完成某一项任务，才算是登陆页面的成功。

AEM 中的登陆页面功能允许营销人员与各代理商的 Web 开发人员或内部创意团队共同合作，来创建可被轻松导入 AEM 的页面设计，并且它们仍然可由营销人员编辑，并根据与其余 AEM 支持站点相同的管理规定进行发布。

在 AEM 中，可通过执行以下步骤来创建登陆页面。

1. 在 AEM 中创建包含登陆页面画布的页面。AEM 附带一个名为&#x200B;**导入程序页面**&#x200B;的示例。

1. [准备 HTML 和资产。](/help/sites-administering/extending-the-design-importer-for-landingpages.md)
1. 将相关资源打包为一个 ZIP 文件，这里我们将其称之为“设计包”。
1. 将设计包导入到导入程序页面中。
1. 修改并发布页面。

### 桌面登录页面 {#desktop-landing-pages}

AEM 中的示例登陆页面如下所示：

![chlimage_1-2](assets/chlimage_1-2.jpeg)

### 移动登陆页面 {#mobile-landing-pages}

登陆页面也可具有移动版本。To have a separate mobile version of the landing page the import design has to have two html files: *index.htm(l)* and *mobile.index.htm(l)*.

登陆页面导入过程与普通登陆页面相同，登陆页面设计另有一个对应移动登陆页面的 html 文件。与桌面登陆页面 html 文件一样，该 html 文件也必须具有画布 `div` 及 `id=cqcanvas`，并且支持桌面登陆页面对应的所有可编辑组件。

移动登陆页面可创建为桌面登陆页面的子页面。若要打开它，请在网站中导航至登陆页面，然后打开子页面。

![chlimage_1-22](assets/chlimage_1-22.png)

>[!NOTE]
>
>如果桌面登陆页面被删除或取消激活，则移动登陆页面也会随之一起被删除或取消激活。

## 登陆页面组件 {#landing-page-components}

要使导入的 HTML 部分可在 AEM 内编辑，您可以将登陆页面 HTML 里的内容直接映射至 AEM 组件。设计导入程序可根据默认设置理解以下组件：

* 文本，即任何文本
* 标题，即 H1-6 标记中的内容
* 图像，即应当可以调换的图像
* 行动动员：

   * 点进率链接
   * 图形链接

* CTA 潜在客户表单，用于捕捉用户信息
* 段落系统 (Parsys)，用于添加任意组件，或以上经过转换的组件

此外，还能扩展此组件，并支持自定义组件。本节详细介绍相关组件。

### 文本 {#text}

通过文本组件可以使用 WYSIWYG 编辑器输入文本块。有关更多信息，请参阅[文本组件](/help/sites-authoring/default-components.md#text)。

![chlimage_1-23](assets/chlimage_1-23.png)

以下是关于登陆页面上的文本组件示例。

![chlimage_1-24](assets/chlimage_1-24.png)

#### 标题 {#title}

该标题组件允许您显示一个标题，并配置其大小 (h1-6)。有关更多信息，请参阅[标题组件](/help/sites-authoring/default-components.md#title)。

![chlimage_1-25](assets/chlimage_1-25.png)

以下是关于登陆页面上的标题组件示例：

![chlimage_1-26](assets/chlimage_1-26.png)

#### 图像 {#image}

该图像组件显示可在内容查找器中进行拖放或通过单击上传的图像。有关更多信息，请参阅[图像组件](/help/sites-authoring/default-components.md)。

![chlimage_1-27](assets/chlimage_1-27.png)

以下是关于登陆页面上的图像组件示例：

![chlimage_1-28](assets/chlimage_1-28.png)

#### 行动动员 (CTA) {#call-to-action-cta}

一个登陆页面设计可以包含多个链接 - 其中部分链接可能用作“行动动员”。

行动动员 (CTA) 用于促使访客立即在登陆页面上采取操作，例如“立即订阅”、“观看此视频”、“时间有限”等等。

* 点进率链接 - 允许您添加一个文本链接，当访客单击这个链接时即被引向目标 URL。
* 图像链接 - 允许您添加一个图像链接，当访客单击这个链接时即被引向目标 URL。

两个 CTA 组件都具有相似的选项。点进率链接另有富文本选项。这些组件将在以下段落中加以详细介绍。

#### 点进率链接 {#click-through-link}

该 CTA 组件可用于在登陆页面上添加文本链接。当用户单击该链接时即被引向组件属性中指定的目标 URL。它是“行动动员”组的一部分。

![chlimage_1-29](assets/chlimage_1-29.png)

**标签** 用户看到的文本。 您可以使用富文本编辑器来修改格式设置。

**目标URL** 输入用户单击文本后要访问的URI。

**渲染选项** 描述渲染选项。 选项如下：

* 在新浏览器窗口中加载页面
* 在当前窗口中加载页面
* 在父框架中加载页面
* 取消所有框架，并在完整的浏览器窗口中加载页面

**CSS** 在“样式”选项卡上，输入CSS样式表的路径。

**ID** 在“样式”选项卡上，输入组件的ID以唯一标识它。

以下是一个点进率链接示例：

![chlimage_1-30](assets/chlimage_1-30.png)

#### 图形链接 {#graphical-link}

该 CTA 组件可用于在登陆页面上添加任何带链接的图像。该图像可以是一个简单的按钮，也可以是任何用作背景的图像。当用户单击此图像时，即被引向组件属性中指定的目标 URL。它是&#x200B;**行动动员**&#x200B;组的一部分。

![chlimage_1-31](assets/chlimage_1-31.png)

**标签** 用户在图形中看到的文本。 您可以使用富文本编辑器来修改格式设置。

**目标URL** 输入用户单击图像后要访问的URI。

**渲染选项** 描述渲染选项。 选项如下：

* 在新浏览器窗口中加载页面
* 在当前窗口中加载页面
* 在父框架中加载页面
* 取消所有框架，并在完整的浏览器窗口中加载页面

**CSS** 在“样式”选项卡上，输入CSS样式表的路径。

**ID** 在“样式”选项卡上，输入组件的ID以唯一标识它。

以下是一个图形链接示例：

![chlimage_1-32](assets/chlimage_1-32.png)

### 行动动员 (CTA) 潜在客户表单 {#call-to-action-cta-lead-form}

潜在客户表单是一种用于搜集访客/潜在客户个人资料信息的表单。这类信息可被存储起来，以供以后进行有针对性的营销活动。这类信息通常包含头衔、姓名、电子邮件、出生日期、地址、兴趣等内容。它是 **CTA 潜在客户表单**&#x200B;的一部分。

以下是一个 CTA 潜在客户表单示例：

![chlimage_1-33](assets/chlimage_1-33.png)

CTA 潜在客户表单是由多个不同组件构成的：

* **潜在客户表单**&#x200B;潜在客户表单组件定义页面上新的潜在客户表单的开头和结尾。其他组件稍后可放置在这些元素之间，例如电子邮件 ID，名字等。

* **表单字段和元素**
表单字段和元素可以包括文本框、单选按钮、图像等。用户通常在表单字段中完成操作，例如键入文本。有关更多信息，请参见单个表单元素。

* **个人资料组**&#x200B;件与访客个人资料相关的个人资料组件用于社交协作以及需要访客个人信息的其他区域。

The preceding shows an example form; it is comprised of the **Lead Form** component (start and end), with **First Name** and **Email Id** fields used for input and a **Submit** field

在 Sidekick 中，有以下可供 CTA 潜在客户表单使用的组件：

![chlimage_1-34](assets/chlimage_1-34.png)

#### 许多潜在客户表单组件的常规设置 {#settings-common-to-many-lead-form-components}

尽管每个潜在客户表单组件都具有不同的用途，但许多表单组件都由相似的选项和参数构成。

配置任意表单组件时，对话框中都提供有下列选项卡：

* **标题与文本**&#x200B;您需要在此指定基本信息，例如组件的标题以及任何附带的文本。在适当情况下，该选项卡还允许您定义其他重要信息，例如字段是否可多选以及可供选择的项目。

* **初始值**
允许您指定默认值。

* **约束**
您可以在此处指定字段是否为必填字段以及是否对该字段进行约束（例如，必须为数字等）。

* **样式**
指示字段的大小和样式。

>[!NOTE]
>
>您看到的字段差别很大，具体差别取决于单个不同的组件。
>
>并非所有选项对所有潜在客户表单组件均可用。有关这些[常用设置](/help/sites-authoring/default-components.md#formsgroup)的更多信息，请参阅“表单”。

#### 潜在客户表单组件 {#lead-form-components}

下节介绍行动动员潜在客户表单的可用组件。

**“关于** ”允许用户添加“关于”信息。

![chlimage_1-35](assets/chlimage_1-35.png)

**地址字段** 允许用户输入地址信息。 在配置该组件时，您必须在对话框中输入元素名称。元素名称即是表单元素的名称。该选项卡指示数据在存储库中的存储位置。

![chlimage_1-36](assets/chlimage_1-36.png)

**“出生日期** ”用户可以输入出生日期信息。

![chlimage_1-37](assets/chlimage_1-37.png)

**电子邮件ID** 允许用户输入电子邮件地址（标识）。

![chlimage_1-38](assets/chlimage_1-38.png)

**名字** -为用户提供一个输入其名字的字段。

![chlimage_1-39](assets/chlimage_1-39.png)

**“性别** ”用户可以从下拉列表中选择其性别。

![chlimage_1-40](assets/chlimage_1-40.png)

**姓氏用户** 可以输入姓氏信息。

![chlimage_1-41](assets/chlimage_1-41.png)

**潜在客户表单** 添加此组件可向登录页面添加潜在客户表单。 潜在客户表单会自动包含一个潜在客户表单的开头和潜在客户表单的结尾字段。其间，您还可以添加本节中介绍的潜在客户表单组件。

![chlimage_1-42](assets/chlimage_1-42.png)

The Lead Form component defines both the start and end of a form using the **Form Start** and **Form End** elements. 它们始终是成对的，以确保正确定义表单。

在添加了潜在客户表单之后，即可以配置表单的开头或结尾，方法是单击相应工具栏中的&#x200B;**编辑**。

**潜在客户表单的开头**

可供配置的两个选项卡为：**表单**&#x200B;和&#x200B;**高级**：

![chlimage_1-43](assets/chlimage_1-43.png)

**感谢页面**
为感谢访客提供其意见而引用的页面。如果留空，表单将在提交后重新显示。

**启动工作流** -确定提交潜在客户表单后将触发哪个工作流。

![chlimage_1-44](assets/chlimage_1-44.png)

**发布选项** ：提供以下发布选项：

* 创建潜在客户
* 电子邮件服务: 创建订阅者并添加到列表 - 如果您当前使用的是 ExactTarget 之类的电子邮件服务提供商，则可以使用此选项。
* 电子邮件服务：发送自动回复的电子邮件——如果您使用的是ExactTarget等电子邮件服务提供商，请使用此功能。
* 电子邮件服务：将用户从列表中取消订阅——如果您使用的是ExactTarget等电子邮件服务提供商，则可使用。
* 使用户取消订阅

**表单标识符** 表单标识符可唯一标识潜在客户表单。 单个页面上具有多个表单时，应使用表单标识符；请确保它们具有不同的标识符。

**加载路径** -用于将预定义值加载到潜在客户表单字段的节点属性的路径。

这是指定库中节点的路径的可选字段。如果此节点具有与字段名称相匹配的属性，则表单上的相应字段将随这些属性的值预加载。如果不存在任何匹配，则字段将包含默认值。

**客户端验证** 指示此表单是否需要客户端验证（始终进行服务器验证）。 这可以与表单Captcha组件结合实现。

**验证资源类型** 如果您要验证整个潜在客户表单（而非单个字段），则定义表单验证资源类型。

如果您要验证完整表单，还应包含以下任一内容：

* 客户端验证的脚本：
   ` /apps/<myApp>/form/<myValidation>/formclientvalidation.jsp`

* 服务器端验证的脚本：
   ` /apps/<myApp>/form/<myValidation>/formservervalidation.jsp`

**操作配置** 根据在发布选项中的选择，操作配置会发生更改。 例如，如果您选择创建潜在客户，则可以配置要将潜在客户添加到哪个列表。

![chlimage_1-45](assets/chlimage_1-45.png)

* **显示提交按钮**
指示是否应显示提交按钮。

* **提交名**
在表单中使用多个提交按钮时的标识符。

* **提交标题**
按钮上显示的名称，例如“提交”或“发送”。

* **显示重设按钮**
选中该复选框可使重置按钮可见。

* **重置标题**
重置按钮上显示的名称。

* **说明**
按钮下方显示的信息。

## 创建登陆页面 {#creating-a-landing-page}

在创建登陆页面时，需要执行以下三个步骤：

1. 创建导入程序页面。
1. [准备要导入的 HTML。](/help/sites-administering/extending-the-design-importer-for-landingpages.md)
1. 导入设计包。

### 使用设计导入程序 {#use-of-the-design-importer}

由于页面导入涉及 HTML 准备、验证和页面测试，因此导入登陆页面应该是一项管理员任务。As an admin, the users performing the import need read, write, create, and delete permissions on `/apps`. 如果用户没有这些权限，则导入将失败。

>[!NOTE]
>
>Because the design importer is intended as an admin tool requiring read, write, create, and delete permissions on `/apps`, Adobe does not recommend using the design importer in production.

Adobe 建议在暂存实例上使用设计导入程序。在暂存实例上，可以由开发人员对导入进行测试和验证，并负责将代码部署到生产实例。

### 创建导入程序页面 {#creating-an-importer-page}

您需要先创建一个导入程序页面（例如在营销活动下），然后才能导入登陆页面设计。使用导入程序页面模板，可以导入完整的 HTML 登陆页面。该页面包含一个拖放框，可以在此框内使用拖放操作导入登陆页面设计包。

>[!NOTE]
>
>By default, an Importer Page can only be created under campaigns, but you can also overlay this template in order to create a landing page under `/content/mysite`.

要创建新的登陆页面，请执行以下操作：

1. 转至&#x200B;**网站**&#x200B;控制台。
1. 在左窗格中选择您的营销活动。
1. 单击&#x200B;**新建**&#x200B;以打开&#x200B;**创建页面**&#x200B;窗口。
1. 选择&#x200B;**导入程序页面**&#x200B;模板，添加标题和（可选）名称，然后单击&#x200B;**创建**。

   ![chlimage_1-1-1](assets/chlimage_1-1-1.png)

   随即会显示您的新导入程序页面。

### 准备要导入的 HTML {#preparing-the-html-for-import}

在导入设计包之前，需要准备 HTML。有关更多信息，请参阅[扩展和配置设计导入](/help/sites-administering/extending-the-design-importer-for-landingpages.md)。

### 导入设计包 {#importing-the-design-package}

创建导入程序页面后，即可将设计包导入其中。有关创建设计包及其推荐结构的详细信息，请参阅[扩展和配置设计导入](/help/sites-administering/extending-the-design-importer-for-landingpages.md)中的说明。

如果您的设计包已准备就绪，请参阅以下步骤说明，将设计包导入到导入程序页面。

1. 打开您[之前创建](#creatingablankcanvaspage)的导入程序页面。

   ![chlimage_1-46](assets/chlimage_1-46.png)

1. 将设计包拖放到拖放框中。请注意，当设计包被拖放到其上方时，箭头方向会发生更改。
1. 执行拖放操作后，您会看到登陆页面替代了导入程序页面。您的HTML登录页面已成功导入。

   ![chlimage_1-2-1](assets/chlimage_1-2-1.png)

>[!NOTE]
>
>导入时，出于安全原因会对标记进行清理，以避免导入和发布无效标记。这种情况会假定只有 HTML 标记；所有其他形式的元素，例如内联 SVG 或 Web 组件等，都会被筛选掉。

>[!NOTE]
>
>如果您在导入设计包时遇到问题，请参阅[疑难排解](/help/sites-administering/extending-the-design-importer-for-landingpages.md#troubleshooting)。

## 处理登陆页面 {#working-with-landing-pages}

登陆页面的设计和资产通常是由代理商的设计人员使用其惯用的工具创建的，如 Adobe Photoshop 或 Adobe Dreamweaver。在设计完成后，设计人员会向营销部门发送一个包含所有资产的 zip 文件。随后即由营销部门的联系人负责将 zip 文件放入 AEM，并发布相关内容。

此外，导入登陆页面后，设计人员可能还需要对其进行修改：编辑或删除内容，以及配置行动动员组件。最后，该营销人员还需要预览登陆页面并激活营销活动，以确保登陆页面已发布。

本节介绍如何执行以下操作：

* 删除登陆页面
* 下载设计包
* 查看导入信息
* 重置登陆页面
* [配置 CTA 组件并向页面中添加内容](#call-to-action-cta)
* 预览登陆页面
* 激活/发布登陆页面

导入设计包时，页面设置菜单中的&#x200B;**清除设计**&#x200B;和&#x200B;**下载导入的 Zip 文件**&#x200B;这两个选项可用：

![chlimage_1-3-1](assets/chlimage_1-3-1.png)

### 下载导入的设计包 {#downloading-the-imported-design-package}

下载 zip 文件，可让您记录随特定登陆页面导入了哪个 zip。请注意，页面上所做的更改并未添加到 zip 文件。

要下载导入的设计包，请单击登陆页面工具栏中的&#x200B;**下载 Zip**。

### 查看导入信息 {#viewing-import-information}

在经典用户界面中，您可以随时单击登陆页面顶部的蓝色感叹号来查看有关上次导入的信息。

![chlimage_1-47](assets/chlimage_1-47.png)

如果导入的设计包存在某些问题，例如是关于某些包中并不存在的图像/脚本，或诸如此类的问题，则设计导入程序会以列表形式显示这些问题。在经典用户界面中，要查看问题列表，请单击登陆页面工具栏中的问题链接。In the following image, clicking on **Issues** link opens the Import Issues window.

![chlimage_1-3](assets/chlimage_1-3.jpeg)

### 重置登陆页面 {#resetting-a-landing-page}

如果您想要在对登陆页面设计包进行更改后重新将其导入，则可以“清除”登陆页面，方法是在经典用户界面中单击登陆页面顶部的&#x200B;**清除**，或在触屏优化用户界面中单击设置菜单中的“清除”。这样做会删除导入的登录页面，并创建空的导入程序页面。

在清除登陆页面时，您可以删除内容更改。If you click **No**, then the content changes are preserved, that is, the structure under `jcr:content/importer`is preserved and only the importer page component and the resources in `etc/design` are removed. Whereas, if you click **Yes**, the `jcr:content/importer` is also removed.

>[!NOTE]
>
>如果您决定删除内容更改，那么只需单击&#x200B;**清除**，则您在已导入登录页面上所做的所有更改以及所有页面属性即会全部丢失。

### 在登陆页面上修改和添加组件 {#modifying-and-adding-components-on-a-landing-page}

要在登陆页面上修改组件，请双击它们将其打开，并像编辑其他组件那样对它们进行编辑。

要在登陆页面上添加组件，请将组件拖放到登陆页面上（从经典用户界面中的 Sidekick 或从触屏优化用户界面中的“组件”窗格进行拖放），然后根据需要进行编辑。

>[!NOTE]
>
>如果登陆页面上的组件无法编辑，则需要在[修改 HTML 文件](/help/sites-administering/extending-the-design-importer-for-landingpages.md)之后重新导入 zip 文件。这意味着在导入期间，不可编辑的部分不会转换为 AEM 组件。

### 删除登陆页面 {#deleting-a-landing-page}

删除登陆页面的过程与删除普通 AEM 页面类似。

唯一的例外是在删除桌面登陆页面时，也会删除对应的移动登陆页面（如果有），但反之则不然。

### 发布登陆页面 {#publishing-a-landing-page}

您可以像发布普通页面一样发布登陆页面及其所有依赖关系。

>[!NOTE]
>
>发布桌面登陆页面的同时，也会发布与其对应的移动版本（如果有）。但发布移动登陆页面，并不会同时发布其桌面版本。
