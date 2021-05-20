---
title: 导入和导出PDF生成器配置文件
seo-title: 导入和导出PDF生成器配置文件
description: 了解如何导入和导出PDF生成器配置文件。
seo-description: 了解如何导入和导出PDF生成器配置文件。
uuid: 3367253b-d222-4c5f-9455-a1810d96112e
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e25c1b35-73eb-4353-8e39-a2d4cdccd101
feature: PDF 生成器
exl-id: b363b23a-29bb-4ea4-a8f2-5ba9fe3c7b27
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '397'
ht-degree: 0%

---

# 导入和导出PDF生成器配置文件{#importing-and-exporting-pdf-generator-configuration-files}

配置文件包含PDF生成器转换信息，包括PDF、文件类型和安全设置。

>[!NOTE]
>
>您无法通过导入自定义native2pdfconfig.xml文件来更改PDF生成器的超时设置。 该文件中的超时设置仅供参考，并在PDF生成器中显示当前设置。 要更改超时设置，请参阅[安装和部署AEM表单](https://www.adobe.com/go/learn_aemforms_installJBoss_63)中的“设置PDF生成器性能参数”。

## 导出当前配置文件{#export-your-current-configuration-file}

1. 在管理控制台中，单击“服务”>“PDF生成器”>“配置文件”>“导出配置”。
1. 要导出设置，请选择相应的选项：

   * 要导出所有命名设置，请选择“下载整个配置”。
   * 要仅导出一个Adobe PDF设置、安全设置或文件类型设置，请选择“下载最小配置”。

      如果要导出最小配置，请选择要导出的Adobe PDF、安全和文件类型设置。

1. 单击下载，并将XML文件保存到适当的位置。

## 导入配置文件{#import-a-configuration-file}

>[!NOTE]
>
>系统将根据导入文件中的信息进行重新配置。

1. 在管理控制台中，单击“服务”>“PDF生成器”>“配置文件”>“导入配置”。
1. 选择导入现有配置文件。
1. 要在“配置文件”框中指定文件位置，请单击“浏览”以查找并选择文件，然后单击&#x200B;**Import**。

## 转换AutoCAD文件{#convert-all-layers-within-autocad-files}中的所有层

默认情况下，PDF生成器仅将AutoCAD文件的默认层转换为PDF，而不是文件中的所有层。 要转换所有层，请按照此步骤操作。

1. 在管理控制台中，单击“服务”>“PDF生成器”>“配置文件”>“导出配置”。
1. 选择“下载整个配置”并单击“下载”。
1. 在文本编辑器中，打开下载的文件，并在`PDFMaker`标记的`AutoCAD`标记下，添加文本`convertAllPages="true"`。
1. 在管理控制台中，单击“服务”>“PDF生成器”>“配置文件”>“导入配置”。
1. 选择“导入现有配置文件”，指定更新的文件，然后单击“导入”。

   使用修改的配置文件转换的任何AutoCAD文件都将转换所有层。

## 将配置重置为随PDF生成器{#reset-your-configuration-to-the-original-settings-installed-with-pdf-generator}一起安装的原始设置

1. 在管理控制台中，单击“服务”>“PDF生成器”>“配置文件”>“导入配置”。
1. 选择“将配置重置为默认设置”，然后单击“导入”。
