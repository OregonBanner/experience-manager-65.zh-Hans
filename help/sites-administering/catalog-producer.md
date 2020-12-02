---
title: Catalog Producer
seo-title: Catalog Producer
seo-description: 了解如何使用AEM Assets的Catalog Producer使用您的数字资产生成产品目录。
uuid: da822d83-8b99-4089-ae1b-11d897d4044e
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 90e36522-3af1-4a8a-b044-1c828c52974e
translation-type: tm+mt
source-git-commit: 684d2d5f73d571a15c8155e7870134c28dc892b7
workflow-type: tm+mt
source-wordcount: '899'
ht-degree: 0%

---


# Catalog Producer{#catalog-producer}

了解如何使用AEM Assets的Catalog Producer使用您的数字资产生成产品目录。

借助Adobe Experience Manager(AEM)Assets Catalog Producer，您可以使用从InDesign应用程序导入的InDesign模板为您的品牌产品创建目录。 要导入InDesign模板，请首先将AEM Assets与InDesign服务器集成。

## 与InDesign服务器{#integrating-with-indesign-server}集成

在集成过程中，配置&#x200B;**DAM更新资产**&#x200B;工作流，该工作流适合与InDesign集成。 此外，为InDesign服务器配置代理工作器。 有关详细信息，请参阅[将AEM Assets与InDesign Server集成](/help/assets/indesign.md)。

>[!NOTE]
>
>在将InDesign文件导入AEM Assets之前，您可以从InDesign文件中生成这些模板。 有关详细信息，请参阅[使用文件和模板](https://helpx.adobe.com/indesign/using/files-templates.html)。
>
>您可以将InDesign模板中的元素映射到XML标签。 在Catalog Producer中将产品属性与模板属性进行映射时，映射的标记将显示为属性。 要了解InDesign文件中的XML标记，请参阅[标记XML的内容](https://helpx.adobe.com/indesign/using/tagging-content-xml.html)。

>[!NOTE]
>
>仅InDesign文件(.indd)用作模板。 不支持扩展名为。indt的文件。

## 创建目录{#creating-a-catalog}

Catalog Producer使用产品信息管理(PIM)数据将产品属性与模板中显示的XML属性进行映射。 要创建目录，请执行以下步骤：

1. 在“资产”用户界面中，点按／单击&#x200B;**AEM徽标**，然后转至&#x200B;**资产>目录**。
1. 在&#x200B;**目录**&#x200B;页面中，点按／单击工具栏中的&#x200B;**创建**，然后从列表中选择&#x200B;**目录**。
1. 在&#x200B;**创建目录**&#x200B;页面中，输入目录的名称和说明（可选）并指定标记（如果有）。 您还可以为目录添加缩略图。

   ![create_catalog](assets/create_catalog.png)

1. 点按／单击&#x200B;**保存**。 将显示确认对话框，通知已创建目录。 点按／单击&#x200B;**完成**&#x200B;以关闭对话框。
1. 要打开您创建的目录，请从&#x200B;**目录**&#x200B;页面点按／单击它。

   >[!NOTE]
   >
   >要打开目录，您还可以点按／单击上一步中提到的确认对话框中的&#x200B;**打开**。

1. 要向目录中添加页面，请点按／单击工具栏中的&#x200B;**创建**，然后选择&#x200B;**新建页面**&#x200B;选项。
1. 从向导中，为页面选择InDesign模板。 然后，点按／单击&#x200B;**下一步**。
1. 指定页面的名称和可选说明。 指定标记（如果有）。
1. 点按／单击工具栏中的&#x200B;**创建**。 然后，点按／单击对话框中的&#x200B;**打开**。 产品的属性显示在左窗格中。 InDesign模板的预定义属性显示在右侧窗格中。
1. 从左窗格中，将产品属性拖动到InDesign模板属性，并在它们之间创建映射。

   要实时视图页面的显示方式，请点按／单击右窗格上的&#x200B;**预览**&#x200B;选项卡。

1. 要创建更多页面，请重复步骤6-9。 要为其他产品创建类似页面，请选择该页面，然后点按／单击工具栏中的&#x200B;**创建类似页面**&#x200B;图标。

   ![create_similar_pages](assets/create_similar_pages.png)

   >[!NOTE]
   >
   >您只能为结构相似的产品创建类似页面。

   点按／单击添加图标，从产品选取器中选择产品，然后点按／单击工具栏中的&#x200B;**选择**。

   ![select_product](assets/select_product.png)

1. 在工具栏中，单击／点按&#x200B;**创建**。 点按／单击&#x200B;**完成**&#x200B;以关闭对话框。 类似页面包含在您的目录中。
1. 要将任何现有InDesign文件添加到目录，请点按／单击工具栏中的&#x200B;**创建**，然后选择&#x200B;**添加到现有页面**&#x200B;选项。
1. 选择InDesign文件，然后点按／单击工具栏中的&#x200B;**添加**。 然后，点按／单击&#x200B;**确定**&#x200B;以关闭对话框。

   如果您在目录页面中引用的产品的元数据已更改，则更改不会自动反映在目录页面中。 引用目录页面中的产品图像上会显示标有&#x200B;**Stale**&#x200B;的横幅，指示引用产品的元数据不是最新的。

   ![chlimage_1-117](assets/chlimage_1-117a.png)

   要确保产品图像反映最新的元数据更改，请在“目录”控制台中选择页面，然后单击／点按工具栏中的&#x200B;**更新页面**&#x200B;图标。

   ![chlimage_1-118](assets/chlimage_1-118a.png)

   >[!NOTE]
   >
   >要更改引用产品的元数据，请导航到“产品”控制台(**AEM徽标** > **Commerce** > **Products**)，然后选择产品。 然后，单击／点按工具栏中的&#x200B;**视图属性**&#x200B;图标，并在资产的属性页面中编辑元数据。

1. 要重新排列目录中的页面，请点按／单击工具栏中的&#x200B;**创建**&#x200B;图标，然后从菜单中选择&#x200B;**合并**。 在向导中，顶部的传送允许您通过拖动页面来重新排序页面。 您还可以删除页面。

1. 点按／单击&#x200B;**下一步**。 要将现有InDesign文件添加为封面，请点按／单击&#x200B;**选择封面**&#x200B;框旁边的&#x200B;**浏览**，然后指定封面模板的路径。
1. 点按／单击&#x200B;**保存**，然后点按／单击&#x200B;**完成**以关闭确认对话框。
选择**完成**选项时，将打开一个对话框，以选择是否要。pdf再现。
   ![导出至](assets/CatalogPDF.png)
pdf如果选择了“Acrobat(PDF)”选项，则除indesign再现外，还将  **在/jcr:content/** rendition中创建pdf再现。您可以通过在下载对话框中选中“演绎版”复选框来下载所有演绎版。

1. 要为您创建的目录生成预览，请在&#x200B;**目录**&#x200B;控制台中选择它，然后单击工具栏中的&#x200B;**预览**&#x200B;图标。

   ![chlimage_1-119](assets/chlimage_1-119a.png)

   在预览中查看目录中的页面。 点按／单击&#x200B;**关闭**&#x200B;以关闭预览。

