---
title: 配置文件类型设置
seo-title: 配置文件类型设置
description: 了解如何配置文件类型设置。
seo-description: 了解如何配置文件类型设置。
uuid: d01f430b-9637-4a5f-b3a7-d5ef3e5ecbc5
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: adbe8416-c8d7-4581-940b-df62eadf0e26
source-git-commit: 80b8571bf745b9e7d22d7d858cff9c62e9f8ed1e
workflow-type: tm+mt
source-wordcount: '6178'
ht-degree: 0%

---


# 配置文件类型设置{#configuring-file-type-settings}

在PDF生成器中，您可以为支持的文件类型设置应用程序设置。 在Windows上，您可以为每个受支持的文件类型设置应用程序设置。 在UNIX和Linux上，您可以设置HTML到PDF和OpenOffice的应用程序设置。

在“文件类型设置”页面上，您可以执行以下任务：

* [创建或编辑文件类型设置](#create-or-edit-file-type-settings)
* 指定默认使用的文件类型设置（请参阅[导入和导出PDF生成器配置文件](https://helpx.adobe.com/aem-forms/6-2/admin-help/importing-exporting-pdf-generator-configuration.html)）
* [更改默认设置](/help/forms/using/admin-help/configuring-file-type-settings2.md#change-the-default-settings)
* [启用PDF/A支持](https://helpx.adobe.com/aem-forms/6-2/admin-help/enable-pdf-a-support.html)
* [删除文件类型设置](https://helpx.adobe.com/aem-forms/6-2/admin-help/enable-pdf-a-support.html)

>[!NOTE]
>
>文件类型设置不适用于回退转换器，例如用于HTML到PDF转换的Acrobat、Microsoft PowerPoint、Microsoft Word和Microsoft Excel。

## 创建或编辑文件类型设置{#create-or-edit-file-type-settings}

创建或编辑文件类型设置，以指定应用程序如何处理支持的文件类型转换。 在Windows上，您可以为每个受支持的文件类型设置应用程序设置。 在UNIX和Linux上，您可以设置HTML到PDF和OpenOffice的应用程序设置。

1. 在管理控制台中，单击&#x200B;**[!UICONTROL 服务]** > **[!UICONTROL PDF生成器]** > **[!UICONTROL 文件类型设置]**。
1. 单击“新建”或单击设置的名称。
1. 在“文件扩展名”框中，为此应用程序接受的文件类型键入以逗号分隔的文件扩展名。 请勿在扩展之前包含句点或之间添加空格。 默认为 `bmp,gif,jpeg,jpg,tif,tiff,png`.
1. （可选）要在图形或图像中对文本使用光学代码识别(OCR)，请选择使用OCR并设置以下选项：

**主要OCR语言：** OCR引擎用于识别字符的语言。默认为英语（美国）。

**PDF输出样式：** 选择“可搜索图像”，将页面在前景中的位图图像以及扫描的文本放置在下方的不可见图层上。页面外观不会更改，但文本会变得可选和可读。 选择“格式化的文本和图形”，以使用识别的文本、字体、图片和其他图形元素来重构原始页面。 默认为可搜索图像（精确）。

**缩减图像采样：** 减少彩色、灰度和单色图像中的像素数。在OCR完成后，将对扫描的图像执行缩减采样。 默认为最低(600 dpi)。 如果将PDF输出样式设置为“可搜索图像（精确）”，则此选项不可用。

1. 完成以下部分中的必需信息：

   [导入和导出PDF生成器配置文件](https://helpx.adobe.com/aem-forms/6-2/admin-help/importing-exporting-pdf-generator-configuration.html)

[Adobe PDF导出设置（仅限Windows）](#adobe-pdf-export-settings-windows-only)

[HTML到PDF设置](#html-to-pdf-settings)

[Flash视频到PDF设置](#flash-videos-to-pdf-settings)

[XPS到PDF设置](#xps-to-pdf-settings)

[PDF优化程序设置](#pdf-optimizer-settings)

[Microsoft Excel设置（仅限Windows）](/help/forms/using/admin-help/configuring-file-type-settings2.md#microsoft-excel-settings-windows-only)

[Microsoft PowerPoint设置（仅限Windows）](/help/forms/using/admin-help/configuring-file-type-settings2.md#microsoft-powerpoint-settings-windows-only)

[Microsoft Project设置（仅限Windows）](/help/forms/using/admin-help/configuring-file-type-settings2.md#microsoft-project-settings-windows-only)

[Microsoft Word设置（仅限Windows）](/help/forms/using/admin-help/configuring-file-type-settings2.md#microsoft-word-settings-windows-only)

[Microsoft Visio设置（仅限Windows）](#visio)

[Microsoft Publisher设置（仅限Windows）](/help/forms/using/admin-help/configuring-file-type-settings2.md#microsoft-publisher-settings-windows-only)

[AutoCAD设置（仅限Windows）](/help/forms/using/admin-help/configuring-file-type-settings2.md#autocad-settings-windows-only)

[OpenOffice设置](/help/forms/using/admin-help/configuring-file-type-settings2.md#openoffice-settings)

[其他应用程序的设置（仅限Windows）](/help/forms/using/admin-help/configuring-file-type-settings2.md#other-applications-settings-windows-only)

   要转到其他部分，请单击其网页上的链接，或使用**[!UICONTROL Next]**或&#x200B;**[!UICONTROL Previous]**&#x200B;按钮。

1. 完成所有部分后，单击&#x200B;**[!UICONTROL Save]**&#x200B;或&#x200B;**[!UICONTROL Save As]**&#x200B;并提供设置的名称。

可以自定义对各种文件类型的支持。 (请参阅[使用AEM Forms](https://www.adobe.com/go/learn_lc_programming_11)进行编程中的“ [添加对其他本机文件格式的支持](https://help.adobe.com/en_US/AEMForms/6.1/ProgramLC/WS624e3cba99b79e12e69a9941333732bac8-7756.2.html)”。)

## 更改默认设置{#change-the-default-settings}

您可以更改应用于新创建源的Adobe PDF设置、安全设置和文件类型设置的默认值。 更改默认值不会影响现有源的设置。

1. 在管理控制台中，单击&#x200B;**[!UICONTROL 服务> PDF生成器]**。
1. 在&#x200B;**[!UICONTROL Adobe PDF设置]**、**[!UICONTROL 文件类型设置]**&#x200B;或&#x200B;**[!UICONTROL 安全设置]**&#x200B;页面上，单击&#x200B;**[!UICONTROL 设置默认设置]**。
1. 选择首选的默认设置。 “设置默认设置”页面上提供了以下一个或多个设置：

   **[!UICONTROL Adobe PDF设置]**:原始默认值为Standard(Acrobat 6)。

   **[!UICONTROL 安全设置]**:原始默认值为无安全性(Acrobat 5)。

   **[!UICONTROL 文件类型设置]**:原始默认值为“标准”。

1. 单击&#x200B;**[!UICONTROL 保存]**。

## 删除文件类型设置{#delete-a-file-type-setting}

您可以删除不再使用的文件类型设置。

1. 在管理控制台中，单击&#x200B;**[!UICONTROL 服务> PDF生成器>文件类型设置]**。
1. 选中要删除的设置旁边的复选框。 您可以选择多个源。 没有复选框的设置将始终包含在PDF生成器中，且无法删除。
1. 单击&#x200B;**[!UICONTROL Delete]**，然后在“删除确认”页上单击&#x200B;**[!UICONTROL Delete]**。

## 图像到PDF设置{#image-to-pdf-settings}

以下选项可确定图像文件如何转换为PDF。 有关访问这些设置的说明，请参阅[创建或编辑文件类型设置](configuring-file-type-settings.md#create-or-edit-file-type-settings)。

**文件扩展名：** 可转换的文件扩展名列表（以逗号分隔）。

**尝试回退转换器：** PDF生成器可以使用Java™或Acrobat将图像文件转换为PDF。当选择此选项并且转换失败或达到指定的超时限制时，PDF生成器会尝试使用替代方法进行转换。 如果替代方法失败或达到指定的超时限制，则会向日志文件写入异常。

>[!NOTE]
>
>JPEG 2000文件只能使用Acrobat进行转换。

**使用OCR:** 指定是否将OCR（光学字符识别）应用到PDF。OCR软件可让您搜索、更正和复制PDF中的文本。

***注意&#x200B;**:仅Microsoft Windows支持OCR PDF（可搜索的PDF）功能。*

**主要OCR语言：** 指定OCR引擎用于识别字符的语言。

**PDF输出样式：** 确定要生成的PDF类型。所有格式都会对文本图像应用OCR和字体以及页面识别，并将它们转换为普通文本。

**可搜索图像：** 确保可搜索和选择文本。此选项会保留原始图像，根据需要对其进行描述，并在其上放置一个不可见的文本层。 “缩减像素采样图像”选项可确定是否对图像进行缩减像素采样以及缩减到什么程度。

**可搜索图像（精确）：** 确保可搜索和选择文本。此选项会保留原始图像，并在其上放置一个不可见的文本层。 建议在要求原始图像具有最大保真度的情况下使用。

**ClearScan:** 合成与原始字体接近的新Type 3字体，并使用低分辨率副本保留页面背景。

**缩减图像采样：** 在OCR完成后，减少彩色、灰度和单色图像中的像素数。选择要应用的缩减采样程度。 编号越高的选项缩减采样次数就越少，这会生成分辨率更高的PDF。

## Adobe PDF导出设置（仅限Windows）{#adobe-pdf-export-settings-windows-only}

“Adobe PDF导出设置”部分中的“导出文件类型”设置用于将PDF文件转换为其他格式。 默认为HTML 4.01，带有级联样式表(CSS)1.0(*.htm， *.html)。

有关访问此设置的说明，请参阅[创建或编辑文件类型设置](configuring-file-type-settings.md#create-or-edit-file-type-settings)。

## HTML到PDF设置{#html-to-pdf-settings}

以下选项可确定如何将HTML文件转换为PDF。 有关访问这些选项的说明，请参阅[创建或编辑文件类型设置](configuring-file-type-settings.md#create-or-edit-file-type-settings)。

**尝试回退转换器：** PDF生成器可以使用Java™或Acrobat将HTML文件转换为PDF。当选择此选项并且转换失败或达到指定的超时限制时，PDF生成器会尝试使用替代方法进行转换。 如果替代方法失败或达到指定的超时限制，则会向日志文件写入异常。

**默认编码：** 从操作系统和字母的菜单设置文件文本的输入编码。仅当HTML源文件未指定编码类型时，才使用“默认编码”选项中显示的选择。

**强制选定编码：** 忽略HTML源文件中指定的任何编码，并使用“默认编码”选项中显示的选定内容。

### 插入设置{#spidering-settings}

** Spidering会扫描网页，以查找指向其他网页的链接。当遇到指向其他网页的链接时，将获取目标页面，并将其包含在所生成的PDF文档中。 启用以下选项可设置要获取并转换为PDF的级别数：

**仅获取X级别：** 蜘蛛程序和从基本页面URL将页面转换到指定级别的深度。值1仅转换提供的URL。

**获取整个网站：** 从提供的URL开始转换整个网站。

**保留在同一路径上：** 任何指向与基本URL不在同一相对路径上的页面的链接，在拼合过程中不会进行转换。

**停留在同一服务器上：** 指向不同服务器上页面的任何链接在插入期间不会进行转换。只转换指向与指定URL相同的服务器的链接。

### 页面转换设置{#page-conversion-settings}

启用这些选项可指定HTML页面的转换方式。 根据页面大小，宽度、高度和边距值会相应地进行调整。

**页面大小：** 选择自定义并指定宽度和高度，或选择预定义的维度。

**方向：** 为转换的PDF文档选择纵向或横向。

**边距：** 指定生成的PDF文档中的边距（上、下、左和右）。

**将书签添加到PDF:** 将书签添加到PDF文档。

**启用带标签的PDF:** 在PDF文档中嵌入标签。

**设置初始视图设置：** 允许您配置“文档选项”、“窗口选项”和“用户界面选项”。这些设置决定了内容最初的显示方式。

### 文档选项{#document-options}

启用这些选项可指定如何显示内容、如何在PDF文档中显示页面以及如何指定放大级别：

**显示：** 选择打开PDF文档时要在Acrobat中打开的窗格。

**页面布局：** 选择PDF文档的页面布局类型。

**放大率：** 为PDF文档的初始视图选择预设的放大率，或选择一个自定义值。选择默认设置表示将使用默认的Acrobat放大率。

**打开到页码：** 指定PDF打开到的页码。

### 窗口选项{#window-options}

启用这些选项以指定窗口的大小和显示方式。

**将窗口大小调整为初始页面：** 将Acrobat窗口大小调整为初始页面的大小。

**屏幕上的居中窗口：** 在屏幕的中心打开窗口。

**以全屏模式打开：** 以全屏模式打开窗口。

**显示：** 在窗口中显示文档标题或文件名。

### 用户界面选项{#user-interface-options}

启用以下选项以指定窗口外观：

**隐藏菜单栏：** 隐藏PDF文档中的菜单栏。

**隐藏工具栏：** 隐藏PDF文档中的工具栏。

**隐藏窗口控件：** 隐藏PDF文档中的窗口控件。

## Flash视频到PDF设置{#flash-videos-to-pdf-settings}

PDF生成器支持提交视频以进行AdobeFlash（SWF或FLV文件），并创建包含视频的PDF文件以在其中嵌入AdobeFlash。 此转换不要求在表单服务器上安装AdobeFlash Player。 有关访问此选项的说明，请参阅[创建或编辑文件类型设置](configuring-file-type-settings.md#create-or-edit-file-type-settings)。

**文件扩展名：** 可转换的文件扩展名列表（以逗号分隔）。

## XPS到PDF设置{#xps-to-pdf-settings}

XML纸张规范(XPS)在Windows打印机中使用。 这是Microsoft格式，可从任何Microsoft Office应用程序创建。 AEM forms提供了转换XPS文件PDF的功能。

**文件扩展名：** 以逗号分隔的列表，其中包含可转换的所有XPS文件扩展名。目前有一种格式：.xps。

## PDF优化程序设置{#pdf-optimizer-settings}

PDF生成器支持减小PDF文件大小的功能。 您是使用所有这些设置，还是仅使用一些设置，取决于您打算如何使用这些文件以及文件必须具有的基本属性。 在大多数情况下，默认设置是最大效率的，即通过删除嵌入的字体、压缩图像以及从不再需要的文件中删除项目来节省空间。

>[!NOTE]
>
>优化数字签名文档会删除并使数字签名失效。

有关访问此设置的说明，请参阅[创建或编辑文件类型设置](configuring-file-type-settings.md#create-or-edit-file-type-settings)。

**Target PDF版本：** 指定与PDF兼容的Acrobat版本。

### 字体 {#fonts}

1. 选择&#x200B;**字体。**
1. 选择以下选项之一：

   **取消嵌入所有字体：** 取消嵌入所有嵌入的字体。

   **请勿取消嵌入任何字体：** 不取消嵌入任何字体。

   **取消嵌入某些字体：** 仅取消嵌入指定的字体。请按照以下步骤指定要取消嵌入的字体：

   * 如有必要，请从&#x200B;**字体源**&#x200B;下拉菜单中选择其他字体目录。 此下拉菜单列出了在&#x200B;**Home > Settings > Core System > Core Configurations**&#x200B;中指定的字体目录。
   * 从&#x200B;**可用字体**&#x200B;列表中选择一个或多个字体，然后单击&#x200B;**添加**。 这些字体将添加到&#x200B;**Fonts to Unembed**&#x200B;列表中。
   * 如果要取消嵌入某些表单服务器上不存在的字体，请在&#x200B;**Add fonts to unembed**&#x200B;框中输入这些字体的名称。 单击&#x200B;**添加**。

   >[!NOTE]
   >
   >*如果要取消嵌入某些其子集已嵌入文档中的字体，请在字体名称前添加+符号。例如，“+Helvetica”。*

1. 如果只想嵌入嵌入字体的在用子集，请选择&#x200B;**子集化所有嵌入字体**。

   >[!NOTE]
   >
   >*如果您将此选项与“取消嵌入某些字体”****结合使用，则“将字体添加到取消嵌入”**列表中**的字体仍将完全取消嵌入。*

   >[!NOTE]
   >
   >*字体子设置是仅嵌入部分字体的技术。字体子集仅包含文档中使用的字符。*

### 透明度 {#transparency}

如果您的PDF文档包含包含透明度的图稿，则可以使用PDF优化器设置来拼合透明度并减小文件大小。

>[!NOTE]
>
>如果选择Acrobat 4.0及更高版本作为Target PDF版本，则所有透明对象都会被扁平化。 对于其他Target PDF版本，支持透明度，您可以配置透明度设置。

选择&#x200B;**透明度**&#x200B;以在优化PDF文档时配置透明度设置。

**透** 明度级别指定要保留的矢量信息量。设置越高，矢量对象就越多，设置越低，矢量对象就越多；中间设置将以矢量形式保留简单区域并栅格化复杂区域。 选择最低设置以栅格化所有图稿。

>[!NOTE]
>
>发生的光栅化量取决于页面的复杂性和重叠对象的类型。

**线条图和文** 本分辨率，所有对象（包括图像、矢量图稿、文本和渐变）都将栅格化到线条图和文本分辨率。支持的值为1像素/英寸(ppi)到9600 ppi。

>[!NOTE]
>
>线条艺术和文本分辨率通常应设置为600-1200 ppi，以提供高质量的光栅化，特别是对衬线或小点大小的字体。

**渐变和网** 格分辨率渐变和网格栅格化到的分辨率。支持的值为1 ppi到1200 ppi。

>[!NOTE]
>
>渐变和网格分辨率通常应设置为150-300 ppi，因为渐变、投影和羽化的质量不会随着分辨率的提高而提高，但打印时间和文件大小会增加。

**将所有文本转换为** 轮廓将所有类型对象（点类型、区域类型和路径类型）转换为轮廓并丢弃包含透明度的页面上的所有类型字形信息。此选项可确保文本的宽度在拼合期间保持一致。 请注意，启用此选项将导致小字体在Acrobat中查看或在低分辨率桌面打印机上打印时显示得略厚。 它不影响在高分辨率打印机或照相机上打印的类型的质量。

**将所有描边转换为轮** 廓将所有描边转换为包含透明度的页面上的简单填充路径。此选项可确保在拼合期间，笔触的宽度保持一致。 请注意，启用此选项会导致细描边显示得略厚，并可能降低拼合性能。

**剪辑复** 杂区域确保矢量图稿和栅格化图稿之间的边界沿对象路径落下。此选项可减少在日志的一部分时导致的拼合工件

<!--
NOTE to WRITER: Unfinished sentence above.
-->

>[!NOTE]
>
>某些打印驱动程序会以不同方式处理光栅和矢量图，有时会导致颜色拼合。 您可以通过禁用某些打印驱动程序特定的颜色管理设置来最大限度地减少拼合问题。 这些设置因每台打印机而异，因此请参阅打印机随附的文档以了解详细信息。

保留叠印：将透明图稿的颜色与背景颜色混合以创建叠印效果。

下表显示了常见的打印机类型及其分辨率（以dpi衡量）、默认屏幕规则(以每英寸线数(lpi)衡量)以及以每英寸像素数(ppi)衡量的图像的重新取样分辨率。 例如，如果打印到600 dpi激光打印机，则输入170作为图像重新采样的分辨率。

**** 图像选择“图像”可为彩色、灰度和单色图像指定压缩和重新取样选项。您可能希望尝试使用这些选项来在文件大小和图像质量之间找到适当的平衡。彩色和灰度图像的分辨率设置应是打印文件的行屏幕规则的1.5到2倍。 单色图像的分辨率应与输出设备相同，但请注意，将单色图像保存的分辨率高于1500 dpi会增加文件大小，而不会显着提高图像质量。 将被放大的图像（如地图）可能需要更高的分辨率。

>[!NOTE]
>
>重新取样单色图像可能会产生意外的查看结果，例如没有图像显示。 如果发生这种情况，请关闭重新取样并再次转换文件。 子采样最有可能出现此问题，而双立方缩减采样最不可能出现此问题。

<table>
 <tbody>
  <tr>
   <th><p><strong>打印机分辨率</strong></p> </th>
   <th><p><strong>默认行屏幕</strong></p> </th>
   <th><p><strong>图像分辨率</strong></p> </th>
  </tr>
  <tr>
   <td><p>300 dpi（激光打印机）</p> </td>
   <td><p>60lpi</p> </td>
   <td><p>120 ppi</p> </td>
  </tr>
  <tr>
   <td><p>600 dpi（激光打印机）</p> </td>
   <td><p>85lpi</p> </td>
   <td><p>170 ppi</p> </td>
  </tr>
  <tr>
   <td><p>1200 dpi（照排机）</p> </td>
   <td><p>120 lpi</p> </td>
   <td><p>240 ppi</p> </td>
  </tr>
  <tr>
   <td><p>2400 dpi（照排机）</p> </td>
   <td><p>150 lpi</p> </td>
   <td><p>300 ppi</p> </td>
  </tr>
 </tbody>
</table>

#### 放弃对象{#discard-objects}

* 选择&#x200B;**放弃对象**&#x200B;以指定要从PDF中删除的对象，并优化CAD绘图中的曲线。
* **放弃所有表单提交、导入和重置操作**:禁用与提交或导入表单数据相关的所有操作，并重置表单字段。此选项保留操作链接到的表单对象。
* **放弃所有JavaScript操作**:从PDF中删除任何使用JavaScript的操作。
* **放弃嵌入的页面缩略图**:删除嵌入的页面缩略图。此选项对于大型文档非常有用，在单击“页面”按钮后，需要较长时间才能绘制页面缩略图。
* **将平滑线转换为曲线**:减少在CAD绘图中用于构建曲线的控制点数，这样可以缩小PDF文件并加快屏幕渲染速度。
* **放弃嵌入的打印设置**:从文档中删除嵌入的打印设置，如页面缩放和双工模式。
* **放弃书签**:从文档中删除所有书签。
* **拼合表单字段**:使表单字段不可用，且外观无变化。表单数据会与页面合并，以成为页面内容。
* **放弃所有替代图像**:删除图像的所有版本，但以屏幕查看为目的的版本除外。某些PDF包含同一图像的多个版本以用于不同目的，例如低分辨率屏幕查看和高分辨率打印。
* **放弃文档标记**:从文档中删除标记，这也会删除文本的辅助功能和重排功能。
* **检测和合并图像片段**:查找碎片化为薄片的图像或蒙版，并尝试将这些切片合并到单个图像或蒙版中。
* **放弃嵌入的搜索索引**:删除嵌入的搜索索引，这会减小文件大小。

#### 放弃用户数据{#discard-user-data}

选择&#x200B;**放弃用户数据**&#x200B;可删除您不希望分发或与其他用户共享的任何个人信息。

* **放弃所有评论、Forms和多媒体**:从PDF中删除所有注释、表单、表单字段和多媒体。
* **放弃所有对象数据**:从PDF中删除所有对象。
* **放弃外部交叉引用**:删除指向其他文档的链接。跳转到PDF中其他位置的链接不会被删除。
* **放弃隐藏图层内容并拼合可见图层**:减小文件大小。优化的文档看起来与原始PDF类似，但不包含图层信息。
* **放弃文档信息和元数据**:删除文档信息字典和所有元数据流中的信息。（使用“另存为”命令将元数据流恢复为PDF的副本。）
* **放弃文件附件**:删除所有文件附件，包括作为注释添加到PDF的附件。（PDF Optimizer不优化附加的文件。）
* **放弃其他应用程序的专用数据**:从PDF文档中剥离仅对创建文档的应用程序有用的信息。此设置不会影响PDF的功能，但会减小文件大小。

### 清理{#clean-up}

选择&#x200B;**Clean Up**以从文档中删除不必要的项目。
这些项目包括对文档的预定用途而言过时或不必要的元素。 删除某些元素可能会严重影响PDF的功能。 默认情况下，只会选择不影响功能的元素。 如果不确定删除其他选项的影响，请使用默认选项。

**压缩**

从下拉菜单中选择以下任意一个Flate压缩选项：

* 压缩整个文件
* 压缩文档结构
* 删除压缩
* 保持压缩不变

**使用Flate对未编码的流进行编码**:对所有未编码的流应用Flate压缩。

**放弃无效书签**:删除指向文档中已删除页面的书签。

**放弃未引用的命名目标**:删除未在PDF文档内部引用的命名目标。此选项不检查来自其他PDF文件或网站的链接。

**优化PDF以实现快速Web查看**:重新构建PDF文档，以便从Web服务器进行逐页下载（字节提供）。

**在使用LZW编码的流中，请改用Flate**:对使用LZW编码的所有内容流和图像应用全压缩。

**放弃无效链接**:删除跳转到无效目标的链接。

**优化页面内容**:将所有行尾字符转换为空格字符，从而改进了Flate压缩。

## Microsoft Excel设置（仅限Windows）{#microsoft-excel-settings-windows-only}

这些选项可确定Microsoft Excel文件的转换方式。 有关访问这些选项的说明，请参阅[创建或编辑文件类型设置](#create-or-edit-file-type-settings)。

**尝试使用OpenOffice作为回退转换器**:如果选择此选项，并且使用Microsoft Excel的转换失败或达到指定的超时限制，PDF生成器将尝试使用OpenOffice进行转换。如果使用OpenOffice的转换失败或达到指定的超时限制，则会向日志文件中写入异常。

**文件扩展名**:指定此应用程序接受的文件类型的文件扩展名（以逗号分隔）。默认为 `xls,xlsx`. 请勿在扩展之前添加句点或在扩展之间添加空格。

**创建符合PDF/A-1a规范的文件**:强制使用PDF/A-1b:2005 RGB Adobe PDF设置。

**将书签添加到Adobe PDF**:将Excel工作表名称转换为书签。默认情况下，此选项处于选中状态。

**将工作表调整为单个页面**:减小文本大小，以适合单个页面上的工作表。

**转换整个工作簿**:转换Excel文件中的所有工作表。如果未选择此选项，则仅转换当前页面。

**自动运行宏**:在转换文档之前，在Excel文档中运行任何宏（例如插入当前时间的宏）。

**转换文档信息**:根据源文件中的文档信息添加PDF文档属性。这包括文档标题、作者、主题和关键词等信息。

**添加指向Adobe PDF的链接**:将源文件中的超链接转换为PDF文档中的超链接。

**将源文件附加到Adobe PDF**:选择此选项后，原始Excel电子表格将作为附件插入到生成的PDF文档中。

**启用辅助功能和带有标记的Reflow**:在PDF文档中嵌入标记以启用辅助功能和重排。

**要加载的Excel加载项列表**:默认情况下（出于安全考虑），将Excel文件转换为PDF后，不会运行Excel加载项。要允许某些Excel加载项在转换期间运行，请提供以逗号分隔的加载项名称列表。

**要转换的工作表列表**:当此框为空时，Excel电子表格中的所有工作表都将包含在生成的PDF中。要有选择地转换工作表的子集，请提供以逗号分隔的工作表名称列表。

## Microsoft PowerPoint设置（仅限Windows）{#microsoft-powerpoint-settings-windows-only}

这些选项决定了Microsoft PowerPoint文件的转换方式。 有关访问这些选项的说明，请参阅[创建或编辑文件类型设置](/help/forms/using/admin-help/configuring-file-type-settings2.md#create-or-edit-file-type-settings)。

**[!UICONTROL 尝试使用OpenOffice作为回退转换器]**:如果选择此选项，并且使用Microsoft PowerPoint的转换失败或达到指定的超时限制，则PDF生成器会尝试使用OpenOffice进行转换。如果使用OpenOffice的转换失败或达到指定的超时限制，则会向日志文件中写入异常。

**[!UICONTROL 文件扩展名]**:指定此应用程序接受的文件类型的文件扩展名（以逗号分隔）。默认值为ppt，pptx。 请勿在扩展之前添加句点或在扩展之间添加空格。

**[!UICONTROL 转换文档信息]**:从源文件的“属性”对话框添加文档信息，包括标题、主题、作者、关键字、经理、公司、类别和注释。默认情况下，此选项处于选中状态。

**[!UICONTROL 将书签添加到Adobe PDF]**:将PowerPoint标题转换为书签。默认情况下，此选项处于选中状态。

**[!UICONTROL 将源文件附加到Adobe PDF]**:将源文件作为附件添加到PDF文件中。默认情况下，此选项处于取消选中状态。

**[!UICONTROL 启用辅助功能和带有标记的Reflow]**:将标记嵌入到PDF文件中。默认情况下，此选项处于取消选中状态。

**[!UICONTROL 将多媒体转换为PDF多媒体]**:尽可能将多媒体转换为PDF多媒体。默认情况下，此选项处于选中状态。

**[!UICONTROL 转换扬声器注释]**:将扬声器注释转换为PDF。

**[!UICONTROL 自动运行宏]**:在转换文档之前，在PowerPoint文档中运行任何宏（例如插入当前时间的宏）。

**[!UICONTROL 基于PowerPoint打印机设置的PDF布局]**:使用PowerPoint打印机设置来布局PDF文档。

**[!UICONTROL 添加指向Adobe PDF的链接]**:在转换文件时保留现有链接。链接的外观通常保持不变。 仅当还选中启用辅助功能选项时，才能创建链接。 默认情况下，此选项处于取消选中状态。

**[!UICONTROL 在Adobe PDF中保存幻灯片过渡]**:转换幻灯片过渡。默认情况下，此选项处于选中状态。

**[!UICONTROL 在Adobe PDF中保存动画]**:将转换后的动画保存在PDF文件中。

**[!UICONTROL 将隐藏的幻灯片转换为PDF页面]**:转换隐藏的幻灯片。

**[!UICONTROL 创建符合PDF/A-1a规范的文件]**:强制使用PDF/A-1b:2005 RGB Adobe PDF设置。生成PDF文件时，不会转换一些PowerPoint功能。 如果PowerPoint过渡在Acrobat中没有等效过渡，则会替换类似过渡。 如果多个动画效果位于同一幻灯片中，则使用单个效果。 页面过渡和项目符号动态消息将进行转换。

## Microsoft Project设置（仅限Windows）{#microsoft-project-settings-windows-only}

这些选项可确定Microsoft Project文件的转换方式。 有关访问这些选项的说明，请参阅[创建或编辑文件类型设置](#create-or-edit-file-type-settings)。

1. **[!UICONTROL 文件扩展名：]** 指定此应用程序接受的文件类型的文件扩展名（以逗号分隔）。默认为 `mpp`. 请勿在扩展之前添加句点或在扩展之间添加空格。

1. **[!UICONTROL 转换文档信息]**:从源文件的“属性”对话框添加文档信息，包括标题、主题、作者、关键字、经理、公司、类别和注释。默认情况下，此选项处于选中状态。
1. **[!UICONTROL 将源文件附加到Adobe PDF]**:将源文件作为附件添加到PDF文件中。
1. **[!UICONTROL 创建符合PDF/A-1a规范的文件]**:强制使用PDF/A-1b:2005 RGB Adobe PDF设置。
1. **[!UICONTROL 自动运行宏]**:在转换文档之前，在Microsoft Project文档中运行任何宏（例如插入当前时间的宏）。

## Microsoft Word设置（仅限Windows）{#microsoft-word-settings-windows-only}

这些选项可确定Microsoft Word文件的转换方式。 有关访问这些选项的说明，请参阅[创建或编辑文件类型设置](#create-or-edit-file-type-settings)。

**[!UICONTROL 尝试使用OpenOffice作为回退转换器]**:如果选择此选项，并且使用Microsoft Word的转换失败或达到指定的超时限制，PDF生成器将尝试使用OpenOffice进行转换。如果使用OpenOffice的转换失败或达到指定的超时限制，则会向日志文件中写入异常。

**[!UICONTROL 文件扩展名]**:指定此应用程序接受的文件类型的文件扩展名（以逗号分隔）。默认为 `doc,docx,rtf,txt`. 请勿在扩展之前添加句点或在扩展之间添加空格。

**[!UICONTROL 转换文档信息]**:从源文件的“属性”对话框添加文档信息，包括标题、主题、作者、关键字、经理、公司、类别和注释。默认情况下，此选项处于选中状态。

**[!UICONTROL 将书签添加到Adobe PDF]**:将标题转换为书签。默认情况下，此选项处于选中状态。

**[!UICONTROL 将源文件附加到Adobe PDF]**:将源文件作为附件添加到PDF文件中。

**[!UICONTROL 将交叉引用和目录转换为链接]**:将所有交叉引用和目录条目转换为链接。默认情况下，此选项处于选中状态。

**[!UICONTROL 启用辅助功能和带有标记的Reflow]**:将标记嵌入到PDF文件中。默认情况下，此选项处于选中状态。

**[!UICONTROL 创建符合PDF/A-1a规范的文件]**:如果选中，则强制使用PDF/A-1b:2005 RGB Adobe PDF设置。

**[!UICONTROL 自动运行宏]**:在转换文档之前，在Word文档中运行任何宏（例如插入当前时间的宏）。

**[!UICONTROL 在Adobe PDF中保留文档标记]**:将Word文档中的标记转换为PDF文件中的批注。

**[!UICONTROL 添加指向Adobe PDF的链接]**:将源文件中的超链接转换为PDF文档中的超链接。

**[!UICONTROL 转换脚注和尾注链接]**:从脚注和尾注引用创建指向PDF文档中注释的链接。

**[!UICONTROL 在Adobe PDF中将显示的注释转换为注释]**:将Word文档中的注释转换为PDF文档中的文本注释。

**[!UICONTROL 启用高级标记]**:添加高级标记以增强辅助功能。

**[!UICONTROL 将所有样式转换为书签]**:将Word文档中的所有样式转换为PDF文档中的书签。

**[!UICONTROL 具有级别的样式]**:指定Word文档中的哪些样式将转换为PDF文档中的书签。还指定书签的级别。 要使用此功能，请取消选择&#x200B;**[!UICONTROL 将所有样式转换为书签]**&#x200B;选项，并以下列格式指定样式名称：

styleName1=level1[,styleName2=level2...]

如果Microsoft Word样式名称包含逗号(,)或等号(=)，请在特殊字符前面加转义字符(&quot;\_)。 例如，指定名为“标题，1”的样式作为“标题\,1”。

## Microsoft Visio设置（仅限Windows） {#visio}

**转换文档信息**:从源文件的“属性”对话框添加文档信息，包括标题、主题、作者、关键字、经理、公司、类别和注释。默认情况下，此选项处于选中状态。 默认情况下，此选项处于启用状态。

**添加指向Adobe PDF的链接**:保留所有链接。默认情况下，此选项处于选中状态。

**将书签添加到Adobe PDF**:将标题转换为书签。默认情况下，此选项处于选中状态。

**将源文件附加到Adobe PDF**:将源文件作为附件添加到PDF文件中。

**始终在Adobe PDF中拼合图层**:拼合所有Visio图层。

**转换所有页面**:转换Visio文件的所有页面。

**在Adobe Acrobat中查看时，打开“图层”面板**:如果Visio图层没有扁平化，则打开一个窗口，在该窗口中，您可以指定在使用Acrobat打开时保留在PDF文件中的图层。默认情况下，此选项处于选中状态。

**创建符合PDF/A-1b规范的文件**:强制使用Adobe PDF设置PDF/A-1b:2005(RGB)。

**将评论转换为Adobe PDF评论**:将Visio注释转换为PDF注释。

## Microsoft Publisher设置（仅限Windows）{#microsoft-publisher-settings-windows-only}

这些选项可确定Microsoft Publisher文件的转换方式。 有关访问这些选项的说明，请参阅[创建或编辑文件类型设置](#create-or-edit-file-type-settings)。

**[!UICONTROL 文件扩展名]**:指定此应用程序接受的文件类型的文件扩展名（以逗号分隔）。默认为 `pub`. 请勿在扩展之前添加句点或在扩展之间添加空格。

## AutoCAD设置（仅限Windows）{#autocad-settings-windows-only}

这些选项可确定AutoCAD文件的转换方式。 有关访问这些选项的说明，请参阅[创建或编辑文件类型设置](/help/forms/using/admin-help/configuring-file-type-settings2.md#create-or-edit-file-type-settings)。

**[!UICONTROL 文件扩展名]**:指定此应用程序接受的文件类型的文件扩展名（以逗号分隔）。默认为 `dwg`. 请勿在扩展之前添加句点或在扩展之间添加空格。

**[!UICONTROL 转换文档信息]**:从源文件的“属性”对话框添加文档信息，包括标题、主题、作者、关键字、经理、公司、类别和注释。默认情况下，此选项处于选中状态。

**[!UICONTROL 将书签添加到Adobe PDF]**:将标题转换为书签。

**[!UICONTROL 始终在Adobe PDF中拼合图层]**:拼合所有AutoCAD层。

**[!UICONTROL 在Adobe Acrobat中查看时打开“层”窗格]**:在Acrobat中打开PDF时显示图层结构。

**[!UICONTROL 创建符合PDF/E-1规范的文件]**:创建符合PDF/E-1规范的文件。PDF/E是用于交换工程和技术文档的ISO标准。 有关PDF/E-1的更多信息，请参阅[Adobe和行业标准](https://www.adobe.com/enterprise/standards/index.html)。

**[!UICONTROL 转换所有布局]**:包含PDF中的所有布局。

**[!UICONTROL 将模型空间转换为3D]**:选择后，模型空间布局将转换为PDF中的3D批注。

**[!UICONTROL 添加指向Adobe PDF的链接]**:如果选中，则保留所有链接。

**[!UICONTROL 将源文件附加到Adobe PDF]**:将源文件作为附件添加到PDF文件中。

**[!UICONTROL 创建符合PDF/A-1b规范的文件]**:强制使用PDF/A-1b Adobe PDF设置。

**[!UICONTROL 转换所有图层]**:默认情况下，PDF生成器仅将AutoCAD文件的默认层转换为PDF，而不是文件中的所有层。选择此选项可转换文件的所有层。

**[!UICONTROL 嵌入比例信息]**:保留绘图比例信息。

**[!UICONTROL 转换当前布局]**:仅包含PDF中的当前布局。

**[!UICONTROL 要转换的AutoCAD布局列表]**:AutoCAD绘图可以有多个布局。当此框为空时，AutoCAD绘图中的所有布局都将包含在生成的PDF文档中。 要有选择地转换布局的子集，请提供以逗号分隔的布局名称列表。

## OpenOffice设置{#openoffice-settings}

这些选项可确定OpenOffice文件的转换方式。 有关访问这些选项的说明，请参阅[创建或编辑文件类型设置](/help/forms/using/admin-help/configuring-file-type-settings2.md#create-or-edit-file-type-settings)。

**尝试将PDFMaker用作回退转换器**:如果选择此选项，并且使用OpenOffice的转换失败或达到指定的超时限制，则PDF生成器会尝试使用PDFMaker进行转换。如果使用PDFMaker的转换失败或达到指定的超时限制，则会向日志文件中写入异常。

**文件扩展名**:指定此应用程序接受的文件类型的文件扩展名（以逗号分隔）。默认为 `odt,odp,ods,odg,odf,sxw,sxi,sxd`. 请勿在扩展之前添加句点或在扩展之间添加空格。

**范围**:转换所有页面或指定特定页面或页面范围。如果未定义页面范围，则会转换所有页面。 要导出一系列页面，请使用3-6格式。 要导出单个页面，请使用格式7;9;11。 您可以使用3-6;8;10;12等格式导出页面范围和单页的组合。

**页面方向**:（仅限纯文本文件）为转换的PDF文档选择纵向或横向。

**图像**:配置图像的转换方式。具有嵌入预览的EPS图像仅导出为预览。 未嵌入预览的EPS图像将导出为空占位符。 通过无损压缩图像，可保留所有像素。 借助图像的JPEG压缩和高质量级别，几乎所有像素都会保留。 在低质量级别下，某些像素会丢失并引入伪影，但文件大小会减小。

**常规**:启用选项以将带标签的PDF转换为PDF，或将Writer和FormCalc文档注释、Impress幻灯片过渡效果或空白页面导出为PDF。导出标记后，文件大小可能会大量增加。 某些导出的标记是目录、超链接和控件。

您还可以指定表单的提交方式。 选项包括XML、FDF、PDF或HTML。 此设置将覆盖您在文档中设置的控件的URL属性。 只能为PDF文档选择一个常用设置：

* PDF（发送整个文档）
* FDF（发送控制内容）
* HTML
* XML

**加标签的PDF**:允许从OpenOffice文档创建带标签的PDF。带标签的PDF包含有关文档内容结构的信息。 在具有不同屏幕的设备上显示文档以及使用屏幕阅读器软件时，这会有所帮助。 它还有助于辅助功能软件对PDF文档执行各种有用操作，例如朗读PDF文档的内容。

**导出说明**:将OpenOffice文档中的注释转换为生成的PDF文档中的注释。

**使用过渡效果**:将OpenOffice演示文稿中的幻灯片转换效果转换为相应的PDF转换效果。

**以格式提交Forms**:创建PDF表单，该表单可由PDF文档的用户填写和打印。

**导出自动插入的空白页面**:选择此选项后，自动插入的空白页面将包含在生成的PDF文档中。如果要双面打印PDF文档，此功能非常有用。 例如，可以配置一本书，以便章节的第一页始终从奇数页开始。 如果上一章在奇数页结束，OpenOffice将设置一个空白偶数页。 此选项控制是否在生成的PDF中包含该偶数编号的页面。

## 其他应用程序设置（仅限Windows）{#other-applications-settings-windows-only}

不能通过管理控制台更改其他应用程序的设置；它们显示支持文件类型的文件扩展名。 有关访问这些设置的说明，请参阅[创建或编辑文件类型设置](https://help.adobe.com/en_US/AEMForms/6.1/AdminHelp/WS92d06802c76abadb-5145d5d12905ce07e7-7e42.2.html)。

* Corel WordPerfect:`wpd`
* AdobePageMaker:`pmd, pm6, p65, pm`
* Adobe FrameMaker:`fm`
* Adobe Photoshop: `psd`

可能需要自定义对这些文件类型的支持。 有关更多信息，请参阅[使用AEM Forms](https://www.adobe.com/go/learn_aemforms_programming_62)编程中的“添加对其他本机文件格式的支持”。

有关配置PDFG网络打印机的帮助，请参阅[设置PDFG网络打印机（仅限Windows）](/help/forms/using/admin-help/setting-pdfg-network-printer-windows.md)。
