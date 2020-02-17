---
title: Catalog Producer
seo-title: Catalog Producer
seo-description: 了解如何在AEM资产中使用Catalog Producer来使用数字资产生成产品目录。
uuid: da822d83-8b99-4089-ae1b-11d897d4044e
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 90e36522-3af1-4a8a-b044-1c828c52974e
translation-type: tm+mt
source-git-commit: 684d2d5f73d571a15c8155e7870134c28dc892b7

---


# Catalog Producer{#catalog-producer}

了解如何在AEM资产中使用Catalog Producer来使用数字资产生成产品目录。

借助Adobe Experience Manager(AEM)Assets Catalog Producer，您可以使用从InDesign应用程序导入的InDesign模板为品牌产品创建目录。 要导入InDesign模板，请首先将AEM资产与InDesign服务器集成。

## Integrating with InDesign server {#integrating-with-indesign-server}

在集成过程中，配置 **DAM更新资产工作流程** ，该工作流程适合与InDesign集成。 此外，为InDesign服务器配置代理Worker。 有关详细信息，请 [参阅将AEM资产与InDesign server集成](/help/assets/indesign.md)。

>[!NOTE]
>
>在将InDesign文件导入AEM资产之前，您可以从InDesign文件生成InDesign模板。 有关详细信息，请 [参阅使用文件和模板](https://helpx.adobe.com/indesign/using/files-templates.html)。
>
>您可以将InDesign模板中的元素映射到XML标签。 在Catalog Producer中将产品属性与模板属性映射时，映射的标记将显示为属性。 要了解InDesign文件中的XML标记，请参阅为XML [标记内容](https://helpx.adobe.com/indesign/using/tagging-content-xml.html)。

>[!NOTE]
>
>只有InDesign文件(.indd)用作模板。 不支持扩展名为。indt的文件。

## 创建目录 {#creating-a-catalog}

Catalog Producer使用产品信息管理(PIM)数据将产品属性与模板中显示的XML属性映射。 要创建目录，请执行以下步骤：

1. 在资产用户界面中，点按／单击 **AEM徽标**，然后转到资产 **>目录**。
1. 在“目 **录** ”页面中，点按／单 **击工具栏中的创建** ，然后从列表中 **选择目录** 。
1. 在“创 **建目录** ”页面中，输入目录的名称和说明（可选），然后指定标记（如果有）。 您还可以为目录添加缩略图。

   ![create_catalog](assets/create_catalog.png)

1. Tap/click **Save**. 将显示一个确认对话框，通知已创建目录。 点按／单击 **完成** ，关闭对话框。
1. 要打开您创建的目录，请在“目录”页面点按／单 **击** 。

   >[!NOTE]
   >
   >要打开目录，您还可以点按／单击上一步中提 **及的确认** 对话框中的打开。

1. 要向目录中添加页面，请点按／单击工 **具栏中的** “创建”，然后选择“ **新建页面** ”选项。
1. 从向导中，为页面选择InDesign模板。 然后，点按／单击下 **一步**。
1. 指定页面的名称和可选说明。 指定标记（如果有）。
1. Tap/click the **Create** from the toolbar. 然后，点按／单击对 **话框中** 的打开。 产品的属性显示在左侧窗格中。 InDesign模板的预定义属性显示在右侧窗格中。
1. 从左侧窗格中，将产品属性拖动到InDesign模板属性，并在它们之间创建映射。

   要实时查看页面的显示方式，请点按／单击右侧窗 **格上的** “预览”选项卡。

1. 要创建更多页面，请重复步骤6-9。 要为其他产品创建类似页面，请选择该页面，然后点按／单击工 **具栏中的创建类似页面** 图标。

   ![create_similar_pages](assets/create_similar_pages.png)

   >[!NOTE]
   >
   >您只能为结构相似的产品创建类似的页面。

   点按／单击添加图标，从产品选取器中选择产品，然后点按／单击工 **具栏中** 的选择。

   ![select_product](assets/select_product.png)

1. 在工具栏中，单击／点按 **创建**。 点按／单击 **完成** ，关闭对话框。 类似的页面包含在您的目录中。
1. 要将任何现有InDesign文件添加到目录，请点按／单击工具栏中的 **创建** ，然后选择添加到现 **有页面选项** 。
1. 选择InDesign文件，然后点按／单击工 **具栏中** 的添加。 然后，点按／单 **击确** 定以关闭对话框。

   如果您在目录页面中引用的产品的元数据发生更改，则更改不会自动反映在目录页面中。 在引用目 **录页面中** ，产品图像上会显示标有“过时”的横幅，指示引用产品的元数据不是最新的。

   ![chlimage_1-117](assets/chlimage_1-117a.png)

   要确保产品图像反映最新的元数据更改，请在“目录”控制台中选择页面，然后单击／点按工具栏中的 **更新页面** 图标。

   ![chlimage_1-118](assets/chlimage_1-118a.png)

   >[!NOTE]
   >
   >要更改引用产品的元数据，请导航到产品控制台(**AEM Logo** > **Commerce** > **Products**)，然后选择产品。 然后，单击／点按工具 **栏中的查看属性** 图标，并在资产的属性页面中编辑元数据。

1. 要重新排列目录中的页面，请点按／单击工 **具栏中的** “创建”图标，然后从菜单中 **选择** “合并”。 在向导中，顶部的传送允许您通过拖动页面来重新排序页面。 您还可以删除页面。

1. Tap/click **Next**. 要将现有InDesign文件添加为封面页，请点按／单击“选择封面页 **”框旁边的****** “浏览”，然后指定封面模板的路径。
1. 点按／单 **击保存**，然后点按／单 **击完成** ，关闭确认对话框。
在选择“完 **成** ”选项时，将打开一个对话框来选择是否要。pdf再现。
   ![如果选择](assets/CatalogPDF.png)了“导出到PDF”选项，则除了Indesign再现外，还会在 **/jcr:content/renditions中创建PDF再现** 。 您可以通过在下载对话框中选中“演绎版”复选框来下载所有演绎版。

1. 要为您创建的目录生成预览，请在“目录”控制台中选 **择它** ，然后单击工具栏中的“ **预览** ”图标。

   ![chlimage_1-119](assets/chlimage_1-119a.png)

   在预览中查看目录中的页面。 点按／单击 **关闭** ，以关闭预览。

