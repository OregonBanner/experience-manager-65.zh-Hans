---
title: 配置备用字体
seo-title: 配置备用字体
description: 了解如何配置备用字体。
seo-description: 了解如何配置备用字体。
uuid: 2745541c-8c6d-4bb4-aa14-ec19afd6bc35
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: d997a268-a40a-462d-badd-94f0731f7ba4
translation-type: tm+mt
source-git-commit: d3719a9ce2fbb066f99445475af8e1f1e7476f4e

---


# 配置备用字体 {#configuring-fallback-fonts}

您可以手动配置FontManagerResources.properties文件，将默认AEM表单字体映射到回退（或替换）（如果服务器上没有默认字体）。 此属性文件位于adobe-fontmanager.jar文件中。

>[!NOTE]
>
>回退字体配置也适用于汇编器服务。

1. 导览至/configurationManager/export目录中的adobe-livecycle-*`[appserver]`**`[aem-forms root]`*.ear文件，制作备份副本，然后解压原始文件。
1. 找到adobe-fontmanager.jar文件并将其解包。
1. 找到FontManagerResources.properties文件，并在文本编辑器中将其打开。
1. 根据需要修改通用字体和备用字体位置和名称并保存文件。

   FontManagerResources.properties文件中的字体条目是相对于 *`[aem-forms root]`*/fonts目录的。 如果指定的字体不是默认的AEM表单字体，则必须在此目录结构中（在现有目录中或新创建的目录中）安装这些字体。

   >[!NOTE]
   >
   >如果指定的字体或默认字体不包含特定的Unicode字符，或者如果该字符不可用，则根据以下优先级从备用字体中取用该字符：

   * 区域设置特定字体
   * 如果未设置区域设置，则为ROOT字体
   * 通用字体，按回退表中的顺序集搜索

1. 重新打包adobe-fontmanager.jar文件。
1. 重新打包adobe-livecycle-*`[appserver]`*.ear文件，然后手动或通过运行Configuration Manager重新部署它。

>[!NOTE]
>
>请勿使用Configuration manager重新打包adobe-livecycle-`[appserver]`.ear文件，因为它将用AEM表单默认值覆盖您的修改。

