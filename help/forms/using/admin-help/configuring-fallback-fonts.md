---
title: 配置回退字体
description: 了解如何为AEM Forms配置后备字体。 可以使用FontManagerResources.properties文件将默认字体手动映射到回退字体。
uuid: 2745541c-8c6d-4bb4-aa14-ec19afd6bc35
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: d997a268-a40a-462d-badd-94f0731f7ba4
feature: PDF Generator
exl-id: 76dd2b0c-9f16-47bf-a565-99277be750fb
source-git-commit: 22d9b22a0fc0bc5f753f2e11ca66e2627e1a8405
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 0%

---

# 配置回退字体 {#configuring-fallback-fonts}

您可以手动配置FontManagerResources.properties文件，以便在服务器上没有默认字体时，将默认AEM Forms字体映射到回退（或替换）。 此属性文件位于adobe-fontmanager.jar文件中。

>[!NOTE]
>
>回退字体配置也适用于汇编程序服务。

1. 导航到adobe-livecycle-*`[appserver]`*&#x200B;中的.ear文件 *`[aem-forms root]`*/configurationManager/export目录，创建备份副本，然后取消打包原始文件。
1. 找到adobe-fontmanager.jar文件并将其解包。
1. 找到FontManagerResources.properties文件并在文本编辑器中将其打开。
1. 根据需要修改“通用”和“后备”字体位置和名称，并保存文件。

   FontManagerResources.properties文件中的字体条目相对于 *`[aem-forms root]`*/fonts目录。 如果指定的字体不是默认的AEM Forms字体，则必须在此目录结构（在现有目录或新创建的目录中）中安装这些字体。

   >[!NOTE]
   >
   >如果指定的字体或默认字体不包含特定的Unicode字符，或者该字符不可用，则根据以下优先级从回退字体中获取该字符：

   * 区域设置特定的字体
   * 如果未设置区域设置，则为ROOT字体
   * 通用字体，按回退表中的顺序集搜索

1. 重新打包adobe-fontmanager.jar文件。
1. 重新打包adobe-livecycle-*`[appserver]`*.ear文件，然后手动或通过运行Configuration Manager重新部署该文件。

>[!NOTE]
>
>请勿使用Configuration Manager重新打包adobe-livecycle-`[appserver]`.ear文件，因为它将使用AEM forms默认值覆盖您的修改。
