---
title: 将Dynamic Media Classic(Scene7)功能添加到您的页面
description: AdobeDynamic Media Classic(Scene7)是一个托管解决方案，用于管理、增强、发布富媒体资产并将其交付到Web、移动设备、电子邮件以及连接Internet的显示屏和打印设备。
uuid: dc463e2d-a452-490e-88af-f79bdaa3b089
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: authoring
content-type: reference
discoiquuid: dc0191d0-f181-4e1e-b3f4-73427aa22073
docset: aem65
exl-id: bc9c864b-8bc3-42b4-ba25-6c5108be4f65
source-git-commit: f4b7566abfa0a8dbb490baa0e849de6c355a3f06
workflow-type: tm+mt
source-wordcount: '3511'
ht-degree: 18%

---

# 将Dynamic Media Classic(Scene7)功能添加到您的页面{#adding-scene-features-to-your-page}

[AdobeDynamic Media Classic(Scene7)](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/home.html) 是一个托管解决方案，用于管理、增强、发布富媒体资产并将其交付到Web、移动设备、电子邮件以及连接Internet的显示屏和打印设备。

您可以在各种查看器中查看在Dynamic Media Classic(Scene7)中发布的Experience Manager资产：

* 缩放
* 弹出
* 视频
* 图像模板
* 图像

您可以将数字资产从Experience Manager直接发布到Dynamic Media Classic(Scene7)，也可以将数字资产从Dynamic Media Classic(Scene7)发布到Experience Manager。

本文档介绍如何将数字资产从Experience Manager发布到Dynamic Media Classic(Scene7)，以及如何将数字资产发布到Analytics。 此外，还详细介绍了各种查看器。有关为Dynamic Media Classic(Scene7)配置Experience Manager的信息，请参阅[将Dynamic Media Classic(Scene7)与Experience Manager集成](/help/sites-administering/scene7.md)。

另请参阅[添加图像映射](/help/assets/image-maps.md)。

有关将视频组件与Experience Manager结合使用的更多信息，请参阅以下内容：

* [视频](/help/sites-classic-ui-authoring/manage-assets-classic-s7-video.md)

>[!NOTE]
>
>如果Dynamic Media Classic(Scene7)资产无法正常显示，请确保Dynamic Media[disabled](/help/assets/config-dynamic.md#disabling-dynamic-media)，然后刷新页面。

## 从Assets手动发布到Dynamic Media Classic(Scene7) {#manually-publishing-to-scene-from-assets}

您可以从经典UI中的“资产”控制台或直接从资产将数字资产发布到Dynamic Media Classic(Scene7)。

>[!NOTE]
>
>Experience Manager会异步发布到Dynamic Media Classic(Scene7)。 选择&#x200B;**[!UICONTROL Publish]**&#x200B;后，您的资产可能需要几秒钟时间才能发布到Dynamic Media Classic(Scene7)。


### 从“资产”控制台发布 {#publishing-from-the-assets-console}

如果资产位于Dynamic Media Classic(Scene7)目标文件夹中，则可以从“资产”控制台发布到Dynamic Media Classic(Scene7)。

1. 在Experience Manager经典UI中，选择&#x200B;**[!UICONTROL 数字资产]**&#x200B;以访问数字资产管理器。

1. 从要发布到Dynamic Media Classic(Scene7)的目标文件夹中选择资产（或资产）或文件夹，然后右键单击并选择&#x200B;**[!UICONTROL 发布到Dynamic Media Classic(Scene7)]**。 或者，您也可以从&#x200B;**[!UICONTROL 工具]**&#x200B;菜单中选择&#x200B;**[!UICONTROL 发布到Dynamic Media Classic(Scene7)]**。

   ![chlimage_1-48](assets/chlimage_1-48.png)

1. 转到Dynamic Media Classic(Scene7)并确认资产可用。

   >[!NOTE]
   >
   >如果资产不在Dynamic Media Classic(Scene7)同步文件夹中，则会显示并禁用两个菜单中的&#x200B;**[!UICONTROL 发布到Dynamic Media Classic(Scene7)]** 。

### 从资产发布 {#publishing-from-an-asset}

您可以手动发布资产，但前提是该资产位于已同步的Dynamic Media Classic(Scene7)文件夹中。

>[!NOTE]
>
>如果资产不在Dynamic Media Classic(Scene7)同步文件夹中，则不会显示指向&#x200B;**[!UICONTROL 发布到Dynamic Media Classic(Scene7)]**&#x200B;的链接。

要直接从数字资产发布到Dynamic Media Classic(Scene7)，请执行以下操作：

1. 在Experience Manager中，选择&#x200B;**[!UICONTROL 数字资产]**&#x200B;以访问数字资产管理器。

1. 双击以打开某个资产。

1. 在资产详细信息窗格中，选择&#x200B;**[!UICONTROL 发布到Dynamic Media Classic(Scene7)]**。

   ![screen_shot_2012-02-22at34828pm](assets/screen_shot_2012-02-22at34828pm.png)

1. 该链接随即会变为&#x200B;**[!UICONTROL 正在发布...]**，之后又变为&#x200B;**[!UICONTROL 已发布]**。转到Dynamic Media Classic(Scene7)并确认资产可用。

   >[!NOTE]
   >
   >如果资产未正确发布到Dynamic Media Classic(Scene7)，则链接将更改为&#x200B;**[!UICONTROL 发布失败]**。 如果资产已发布到Dynamic Media Classic(Scene7)，则该链接会显示&#x200B;**[!UICONTROL Re-Publish to Dynamic Media Classic(Scene7)]**。 通过重新发布，您可以更改Experience Manager中的资产并重新发布它们。

### 从CQ目标文件夹外部发布资产 {#publishing-assets-from-outside-the-cq-target-folder}

Adobe建议您仅从Dynamic Media Classic(Scene7)目标文件夹中的资产将资产发布到Dynamic Media Classic(Scene7)。 但是，如果您必须从目标文件夹以外的文件夹上传资产，您仍然可以这样做，方法是将资产上传到Dynamic Media Classic(Scene7)上的按需文件夹。 首先，为要显示资产的页面配置云配置。 然后，将Dynamic Media Classic(Scene7)组件添加到页面，并将资产拖放到该组件上。 为该页面设置页面属性后，会显示&#x200B;**[!UICONTROL 发布到Dynamic Media Classic(Scene7)]**&#x200B;链接，在选择该链接后，该链接会触发上传到Dynamic Media Classic(Scene7)的操作。

>[!NOTE]
>
>位于按需文件夹中的资产不会显示在Dynamic Media Classic(Scene7)内容浏览器中。

**要从CQ目标文件夹外部发布资产，请执行以下操作：**

1. 在经典UI的Experience Manager中，选择&#x200B;**[!UICONTROL 网站]**，然后导航到要将数字资产添加到尚未发布到Dynamic Media Classic(Scene7)的网页。 （普通页面继承规则适用。）

1. 在Sidekick中，选择&#x200B;**[!UICONTROL 页面]**&#x200B;图标，然后选择&#x200B;**[!UICONTROL 页面属性]**。

1. 选择&#x200B;**[!UICONTROL Cloud Services]**。
1. 选择&#x200B;**[!UICONTROL 添加服务]**。
1. 选择&#x200B;**[!UICONTROL Dynamic Media Classic(Scene7)]**。
1. 在&#x200B;**[!UICONTROL AdobeDynamic Media Classic(Scene7)]**&#x200B;下拉列表中，选择所需的配置，然后选择&#x200B;**[!UICONTROL 确定]**。

   ![chlimage_1-49](assets/chlimage_1-49.png)

1. 在网页上，将Dynamic Media Classic(Scene7)组件添加到页面上的所需位置。
1. 从内容查找器中，将相应的数字资产拖放到该组件中。您会看到一个指向&#x200B;**[!UICONTROL 检查Dynamic Media Classic(Scene7)发布状态]**&#x200B;的链接。

   >[!NOTE]
   >
   >如果数字资产位于CQ目标文件夹中，则不会显示指向&#x200B;**[!UICONTROL 检查Dynamic Media Classic(Scene7)发布状态]**&#x200B;的链接。 资产会放置在组件中。

   ![chlimage_1-50](assets/chlimage_1-50.png)

1. 选择&#x200B;**[!UICONTROL 检查Dynamic Media Classic(Scene7)发布状态]**。 如果资产未发布，则Experience Manager会将资产发布到Dynamic Media Classic(Scene7)。 上传资产后，即会在按需文件夹中找到资产。 默认情况下，按需文件夹位于&#x200B;**[!UICONTROL name_of_the_company/CQ5_adhoc]**&#x200B;中。 如果需要，您可以[配置按需文件夹](#configuringtheadhocfolder)。

   >[!NOTE]
   >
   >如果资产不在Dynamic Media Classic(Scene7)同步文件夹中，并且当前页面没有关联的Dynamic Media Classic(Scene7)云配置，则上传会失败。

## Dynamic Media Classic(Scene7)组件 {#scene-components}

以下Dynamic Media Classic(Scene7)组件在Experience Manager中可用：

* 缩放
* 弹出（缩放）
* 图像模板
* 图像
* 视频

>[!NOTE]
>
>默认情况下，这些组件不可用，在使用之前必须在设计模式下选择这些组件。

在设计模式下使组件可用后，您可以像任何其他Experience Manager组件一样将组件添加到页面。 尚未发布到Dynamic Media Classic(Scene7)的资产，如果位于同步文件夹、页面或Dynamic Media Classic(Scene7)云配置中，则会发布到Dynamic Media Classic(Scene7)。

>[!NOTE]
>
>如果要创建和开发自定义S7查看器，并使用内容查找器，则必须明确添加`allowfullscreen`参数。

### Flash 查看器生命周期终止通知 {#flash-viewers-end-of-life-notice}

自2017年1月31日起，AdobeDynamic Media Classic(Scene7)正式终止对Flash查看器平台的支持。

### 将Dynamic Media Classic(Scene7)组件添加到页面 {#adding-a-scene-component-to-a-page}

将Dynamic Media Classic(Scene7)组件添加到页面的方法与将组件添加到任何页面的方法相同。 Dynamic Media Classic(Scene7)组件在以下部分中进行了详细描述。

要在经典UI中将Dynamic Media Classic(Scene7)组件/查看器添加到页面，请执行以下操作：

1. 在Experience Manager中，打开要添加Dynamic Media Classic(Scene7)组件的页面。

1. 如果没有可用的Dynamic Media Classic(Scene7)组件，请在Sidekick中选择标尺以进入&#x200B;**设计**&#x200B;模式，选择&#x200B;**[!UICONTROL 编辑]** parsys，然后选择所有&#x200B;**[!UICONTROL Dynamic Media Classic(Scene7)]**&#x200B;组件以使其可用。

1. 通过在Sidekick中选择铅笔，返回到&#x200B;**编辑**&#x200B;模式。

1. 将Sidekick中&#x200B;**[!UICONTROL Dynamic Media Classic(Scene7)]**&#x200B;组的组件拖动到页面上所需位置。

1. 选择***[!UICONTROL 编辑]**&#x200B;以便打开组件。

1. 根据需要编辑组件，然后选择&#x200B;**[!UICONTROL OK]**&#x200B;以保存更改。

### 向响应式网站添加交互式查看体验 {#adding-interactive-viewing-experiences-to-a-responsive-website}

资产的响应式设计意味着资产会根据资产的显示位置进行相应调整。 利用响应式设计，可以在多种设备上有效地显示同一资产。

在经典 UI 中，要在响应式网站中添加交互式查看体验，请执行以下操作：

1. 登录到Experience Manager，并确保已配置[AdobeDynamic Media Classic(Scene7)Cloud Services](/help/sites-administering/scene7.md#configuring-scene-integration)，并且Dynamic Media Classic(Scene7)组件可用。

   >[!NOTE]
   >
   >如果Dynamic Media Classic(Scene7)WCM组件不可用，请确保通过设计模式启用它们。

1. 在启用了Dynamic Media Classic(Scene7)组件的网站中，将&#x200B;**[!UICONTROL Image]**&#x200B;查看器拖至页面。
1. 编辑组件并在&#x200B;**[!UICONTROL Dynamic Media Classic(Scene7)设置]**&#x200B;选项卡中调整断点。

   ![chlimage_1-51](assets/chlimage_1-51.png)

1. 确认查看器可实现响应式大小调整，并且所有交互已针对台式机、平板电脑和移动设备进行了优化。

### 所有Dynamic Media Classic(Scene7)组件通用的设置 {#settings-common-to-all-scene-components}

尽管配置选项有所不同，但以下选项在所有Dynamic Media Classic(Scene7)组件中是通用的：

* **文件引用** - 浏览到要引用的文件。文件引用会显示资产URL，但不一定会显示完整的Dynamic Media Classic(Scene7)URL，包括URL命令和参数。 您无法在此字段中添加Dynamic Media Classic(Scene7)URL命令和参数。 而是必须通过组件中的相应功能添加它们。
* **宽度** - 允许您设置宽度。
* **高度** - 允许您设置高度。

您可以通过打开（双击）Dynamic Media Classic(Scene7)组件来设置这些配置选项，例如，在您打开&#x200B;**Zoom**&#x200B;组件时：

![chlimage_1-52](assets/chlimage_1-52.png)

### 缩放 {#zoom}

按下 + 按钮时，HTML5 缩放组件会显示放大的图像。

缩放工具位于资产底部。选择&#x200B;**[!UICONTROL +]**&#x200B;放大。 选择&#x200B;**[!UICONTROL -]**&#x200B;以减少。 选择&#x200B;**[!UICONTROL x]**&#x200B;或重置缩放箭头可将图像恢复到导入时的原始大小。 选择对角线箭头，以使其全屏显示。 选择&#x200B;**[!UICONTROL 编辑]**&#x200B;以便您可以配置组件。 使用此组件，您可以配置所有Dynamic Media Classic(Scene7)组件通用的[设置](#settings-common-to-all-scene-components)。

![](do-not-localize/chlimage_1-3.png)

### 弹出 {#flyout}

在 HTML5 弹出组件中，资产会分屏显示；左侧屏幕以指定大小显示资产；右侧屏幕则显示缩放部分。选择&#x200B;**[!UICONTROL 编辑]**&#x200B;以便您可以配置组件。 使用此组件，您可以配置所有Dynamic Media Classic(Scene7)组件通用的[设置](/help/sites-administering/scene7.md#settingscommontoallscene7components)。

>[!NOTE]
>
>如果弹出组件使用自定义大小，则系统会使用该自定义大小，并禁用该组件的响应设置。
>
>如果您的弹出组件使用设计视图中设置的默认大小，则会使用默认大小。 组件在启用了组件的响应设置的情况下，可延展以适应页面布局大小。 但是，请注意，组件的响应设置存在限制。 在响应设置中使用弹出组件时，不应将其用于整个页面延伸。 否则，弹出窗口可能会超出页面的右边框。

![chlimage_1-53](assets/chlimage_1-53.png)

### 图像 {#image}

通过Dynamic Media Classic(Scene7)图像组件，您可以向图像中添加Dynamic Media Classic(Scene7)功能，如Dynamic Media Classic(Scene7)修饰符、图像或查看器预设，以及锐化。 Dynamic Media Classic(Scene7)图像组件与Experience Manager中具有特殊Dynamic Media Classic(Scene7)功能的其他图像组件类似。 在此示例中，图像应用了Dynamic Media Classic(Scene7)URL修饰符`&op_invert=1`。

![](do-not-localize/chlimage_1-4.png)

**标题、替代文本**  — 在高级选项卡中，为图像添加标题，并为关闭了图形的用户添加替换文本。

**URL，在中打开**  — 您可以设置资产以从中打开链接。设置 URL，并在打开方式中指示是要在同一窗口中还是在新窗口中打开该 URL。

![chlimage_1-54](assets/chlimage_1-54.png)

**查看器预设**  — 从下拉菜单中选择一个现有的查看器预设。如果您要查找的查看器预设不可见，则必须使其可见。 请参阅管理查看器预设。如果您使用的是图像预设，则无法选择查看器预设，反之，则无法选择查看器预设。

**Dynamic Media Classic(Scene7)配置**  — 选择要从SPS中获取活动图像预设的Dynamic Media Classic(Scene7)配置。

**图像预设**  — 从下拉菜单中选择一个现有的图像预设。如果您要查找的图像预设不可见，则必须使其可见。 请参阅管理图像预设。如果您使用的是图像预设，则无法选择查看器预设，反之，则无法选择查看器预设。

**输出格式**  — 选择图像的输出格式，例如jpeg。根据所选的输出格式，您可能会有额外的配置选项。请参阅图像预设最佳实践。

**锐化**  — 选择要锐化图像的方式。图像预设最佳实践和锐化最佳实践中详细介绍了锐化。

**URL修饰符**  — 您可以通过提供其他S7图像命令来更改图像效果。这些命令在图像预设和命令参考中有介绍。

**断点**  — 如果您的网站是响应式的，您需要调整断点。断点之间必须使用逗号 (,) 分隔。

### 图像模板 {#image-template}

Dynamic Media Classic(Scene7)图像模板是已导入到Dynamic Media Classic(Scene7)的分层Photoshop内容，其中内容和属性已进行参数化，以便进行可变性。 **[!UICONTROL 图像模板]**&#x200B;组件允许您导入图像并在Experience Manager中动态更改文本。 此外，您还可以配置&#x200B;**[!UICONTROL 图像模板]**&#x200B;组件，以使用 Client Context 中的值，从而让每个客户获取个性化的图像体验。

选择&#x200B;**[!UICONTROL 编辑]** — 以配置组件。 您可以配置所有Dynamic Media Classic(Scene7)组件通用的[设置以及本节中介绍的其他设置。](/help/sites-administering/scene7.md#settingscommontoallscene7components)

![chlimage_1-55](assets/chlimage_1-55.png)

**文件引用、宽度、高度**  — 请参阅所 [有Dynamic Media Classic(Scene7)组件通用的设置](/help/sites-administering/scene7.md#settingscommontoallscene7components)。

>[!NOTE]
>
>Dynamic Media Classic(Scene7)URL命令和参数不能直接添加到文件引用URL中。 只能在组件 UI 的&#x200B;**[!UICONTROL 参数]**&#x200B;面板中定义这些命令和参数。

**标题、替代文本**  — 在Dynamic Media Classic(Scene7)图像模板选项卡中，为图像添加标题，并为关闭了图形的用户添加替换文本。

**URL，在中打开**  — 您可以设置资产以从中打开链接。设置 URL，并在打开方式中指示是要在同一窗口中还是在新窗口中打开该 URL。

![chlimage_1-56](assets/chlimage_1-56.png)

**参数面板**  — 导入图像时，会使用图像中的信息预填充这些参数。如果没有可以动态更改的内容，则此窗口将是空的。

![chlimage_1-57](assets/chlimage_1-57.png)

#### 动态更改文本 {#changing-text-dynamically}

要动态更改文本，请在字段中输入新文本，然后选择&#x200B;**[!UICONTROL OK]**。 在此示例中，**价格**&#x200B;现在为 50 美元，运费为 99 美分。

![chlimage_1-58](assets/chlimage_1-58.png)

图像中的文本发生了更改。通过选择字段旁边的&#x200B;**[!UICONTROL 重置]**，可将文本重置为原始值。

![chlimage_1-59](assets/chlimage_1-59.png)

#### 更改文本以反映客户端上下文值的值 {#changing-text-to-reflect-the-value-of-a-client-context-value}

要将字段链接到客户端上下文值，请选择&#x200B;**[!UICONTROL 选择]**&#x200B;以打开客户端上下文菜单，选择客户端上下文，然后选择&#x200B;**[!UICONTROL 确定]**。 在此示例中，由于已将名称与个人资料中设置的格式化名称链接在一起，因此名称会相应地发生更改。

![chlimage_1-60](assets/chlimage_1-60.png)

文本反映了当前已登录用户的名称。通过选择字段旁边的&#x200B;**[!UICONTROL 重置]**，可将文本重置为原始值。

![chlimage_1-61](assets/chlimage_1-61.png)

#### 将Dynamic Media Classic(Scene7)图像模板设为链接 {#making-the-scene-image-template-a-link}

您可以将Dynamic Media Classic(Scene7)图像模板组件设为可单击的链接。

1. 在具有Dynamic Media Classic(Scene7)图像模板组件的页面上，选择&#x200B;**[!UICONTROL 编辑]**。
1. 在 **[!UICONTROL URL]** 字段中，输入用户单击图像后所转到的 URL。在&#x200B;**[!UICONTROL 打开方式]**&#x200B;字段中，选择您希望在新窗口中还是在同一窗口中打开目标。

   ![chlimage_1-62](assets/chlimage_1-62.png)

1. 选择&#x200B;**[!UICONTROL 确定]**。

### 视频组件 {#video-component}

Dynamic Media Classic(Scene7)**[!UICONTROL 视频]**&#x200B;组件(可从Sidekick的Dynamic Media Classic(Scene7)部分获取)使用设备和带宽检测为每个屏幕提供正确的视频。 此组件是一种 HTML5 视频播放器，它是可以跨渠道使用的单一查看器。

它可用于自适应视频集、单个MP4视频或单个F4V视频。

请参阅[视频](/help/sites-classic-ui-authoring/manage-assets-classic-s7-video.md) ，以了解有关视频如何与Dynamic Media Classic(Scene7)集成一起使用的更多信息。 此外，请参阅[**Dynamic Media Classic(Scene7)视频**&#x200B;组件与基础&#x200B;**视频**&#x200B;组件](/help/sites-classic-ui-authoring/manage-assets-classic-s7-video.md)的比较情况。

![chlimage_1-63](assets/chlimage_1-63.png)

### 视频组件的已知限制 {#known-limitations-for-the-video-component}

AdobeDAM和WCM显示是否上传了主源视频。 但它们不会显示以下代理资产：

* Dynamic Media Classic(Scene7)编码演绎版
* Dynamic Media Classic(Scene7)自适应视频集

在Dynamic Media Classic(Scene7)视频组件中使用自适应视频集时，必须调整该组件的大小以适合视频的尺寸。

## Dynamic Media Classic(Scene7)内容浏览器 {#scene-content-browser}

通过Dynamic Media Classic(Scene7)内容浏览器，您可以直接在Experience Manager中查看Dynamic Media Classic(Scene7)中的内容。 要访问内容浏览器，请在内容查找器中，选择触屏优化用户界面中的&#x200B;**Dynamic Media Classic(Scene7)**&#x200B;或经典用户界面中的&#x200B;**S7**&#x200B;图标。 这两种用户界面的功能是相同的。

如果您有多个配置，则默认情况下Experience Manager会显示[默认配置](/help/sites-administering/scene7.md#configuring-a-default-configuration)。 您可以在Dynamic Media Classic(Scene7)内容浏览器的下拉菜单中直接选择不同的配置。

>[!NOTE]
>
>* 按需文件夹中的资产不会显示在Dynamic Media Classic(Scene7)内容浏览器中。
>* 启用[安全预览](/help/sites-administering/scene7.md#configuring-the-state-published-unpublished-of-assets-pushed-to-scene)后，在Dynamic Media Classic(Scene7)上已发布和未发布的资产都会显示在Dynamic Media Classic(Scene7)内容浏览器中。
>* 如果在内容浏览器中没有看到&#x200B;**[!UICONTROL Dynamic Media Classic(Scene7)]**&#x200B;或&#x200B;**[!UICONTROL S7]**&#x200B;图标作为选项，则必须[配置Dynamic Media Classic(Scene7)才能与Experience Manager](/help/sites-administering/scene7.md)一起使用。
>* 对于视频，Dynamic Media Classic(Scene7)内容浏览器支持：
   >   * 自适应视频集：一种容器，包含在多种屏幕上实现无缝播放所需的所有视频呈现
   >   * 单个 MP4 视频
   >   * 单个F4V视频


### 浏览内容 {#browsing-content-in-the-classic-ui}

通过选择&#x200B;**[!UICONTROL S7]**&#x200B;选项卡，浏览Dynamic Media Classic(Scene7)中的内容。

您可以通过选择配置来更改您正在访问的配置。 文件夹会根据您选择的配置而发生更改。

![chlimage_1-64](assets/chlimage_1-64.png)

与资产的内容查找器一样，您也可以搜索资产并筛选结果。但是，与资产查找器不同的是，在 **S7** 选项卡中输入关键字时，文件名是以您输入的字符串&#x200B;**开头**，而不是将关键字&#x200B;**包含**&#x200B;在文件名中。

默认情况下，资产会按文件名显示。但是，您也可以按资产类型过滤结果。

>[!NOTE]
>
>对于视频，WCM的Dynamic Media Classic(Scene7)内容浏览器支持：
>
>* 自适应视频集：一种容器，包含在多种屏幕上实现无缝播放所需的所有视频呈现
>* 单个 MP4 视频
>* 单个F4V视频

>



### 使用内容浏览器搜索Dynamic Media Classic(Scene7)资产 {#searching-for-scene-assets-with-the-content-browser}

搜索Dynamic Media Classic(Scene7)资产与搜索Experience Manager资产类似。 但存在的例外是，在搜索时，您实际上会在Dynamic Media Classic(Scene7)系统中看到资产的远程视图，而不是直接将它们导入Experience Manager。

您可以使用经典 UI 或触屏优化 UI 来查看和搜索资产。根据所用的界面，搜索方式会略有不同。

在任一 UI 中进行搜索时，您都可以按以下条件进行筛选（此处显示的是触屏优化 UI）：

**输入关键字**  — 您可以按名称搜索资产。搜索关键词时，输入的是文件名的开头。 例如，键入“swimming”一词后，将在该文件夹中查找任何以这些字母开头的资产文件名。在键入要查找资产的术语后，请务必选择enter。

![chlimage_1-65](assets/chlimage_1-65.png)

**文件夹/路径**  — 文件夹的名称基于您选择的配置。您可以通过以下方式向下展开到较低级别：选择文件夹图标，选择子文件夹，然后选择复选标记以将其选中。

如果输入关键字并选择文件夹，则Experience Manager会搜索该文件夹及其所有子文件夹。 但是，如果您在搜索时未输入任何关键字，则选择文件夹只会显示该文件夹中的资产，而不包含任何子文件夹。

默认情况下，Experience Manager会搜索选定的文件夹和所有子文件夹。

![chlimage_1-66](assets/chlimage_1-66.png)

**资产类型**  — 选择Dynamic Media Classic(Scene7)以浏览Dynamic Media Classic(Scene7)内容。仅当配置了Dynamic Media Classic(Scene7)时，此选项才可用。

![chlimage_1-67](assets/chlimage_1-67.png)

**配置**  — 如果您在Cloud Services中定义了多个Dynamic Media Classic(Scene7)配置，则可以在此处选择该配置。因此，文件夹会根据您选择的配置进行更改。

![chlimage_1-68](assets/chlimage_1-68.png)

**资产类型**  — 在Dynamic Media Classic(Scene7)浏览器中，您可以筛选结果以包含以下任意内容：图像、模板、视频和自适应视频集。如果您未选择任何资产类型，则默认情况下，Experience Manager会搜索所有资产类型。

![chlimage_1-69](assets/chlimage_1-69.png)

>[!NOTE]
>
>* 在经典 UI 中，您还可以搜索 **Flash** 和 **FXG**。不支持在触屏优化UI中过滤这两个术语。
   >
   >
* 搜索视频时，您搜索的是单个视频呈现。结果会返回原始视频呈现（仅限 *.mp4）以及编码视频呈现。
* 搜索自适应视频集时，您正在搜索文件夹及所有子文件夹，但前提是您向搜索添加了关键字。 如果您未添加关键词，则Experience Manager不会搜索子文件夹。



**发布状态**  — 您可以根据发布状态筛选资产：已取消发布或已发布。如果未选择任何发布状态，则默认情况下，Experience Manager会搜索所有发布状态。

![chlimage_1-70](assets/chlimage_1-70.png)
