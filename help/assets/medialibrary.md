---
title: 比较Adobe Experience Manager资产和媒体库产品。
description: 比较Experience Manager资产和媒体库产品，了解差异。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 566add37d6dd7efe22a99fc234ca42878f050aee
workflow-type: tm+mt
source-wordcount: '656'
ht-degree: 2%

---


# Experience Manager Assets与Experience Manager Media Library {#aem-assets-vs-aem-medialibrary}

Adobe Experience Manager资产是Experience Manager平台不可或缺的一部分。 这种顺畅的集成被视为Experience Manager的一个主要优势，可确保内容作者的内容管理一致性和高工作效率。

## 常见问题 {#frequently-asked-questions}

### 什么是资产？ {#what-is-aem-assets}

资产是Experience Manager的一项功能，它允许用户在基于Web的存储库中管理其数字资产(图像、视频、文档和音频剪辑)。 资产包括元数据支持、演绎版、查找器和管理界面。

### 什么是Experience Manager Media Library? {#what-is-the-aem-media-library}

Experience Manager媒体库是Experience Manager WCM内容存储库的指定部分，存储图像和其他共享资源。 媒体库为WCM提供基本的数字资产管理功能。

### 不属于WCM的资产会为我带来什么？ {#what-do-i-get-from-aem-assets-that-is-not-part-of-aem-wcm}

只有资产客户才能使用的独特功能有：

* 能够提取和编辑除标题、标记和描述之外的元数据。
* 欢迎屏幕中提供资产管理员。
* 与数字资产管理相关的所有工作流步骤，如摄取、资产删除、子资产处理、元数据提取。
* 包空间 `dam` 中的库。

使用这些功能需要获得资产的有效许可。

### 资产是否可作为单独的包提供？ {#is-aem-assets-available-as-a-separate-package}

否. 为了简化安装和部署，所有Experience Manager应用程序和加载项都通过一个包提供，其中包含所有功能。 这并不表示您有权使用包中的所有功能。

### 我想编辑数字资产的元数据。 我需要资产吗？ {#i-want-to-edit-metadata-of-digital-assets-do-i-need-aem-assets}

如果您计划编辑除标题、描述和标记以外的元数据，则需要为资产授予许可。

### 我想在我的网站上使用类别谓词。 我需要资产吗？ {#i-want-to-use-the-category-predicate-on-my-website-do-i-need-aem-assets}

是的，此类别谓词是资产的一部分，需要资产许可证。

### 我想在导入时自动调整图像大小。 我需要资产吗？ {#i-want-to-automatically-resize-images-upon-import-do-i-need-aem-assets}

否. 调整静态图像的大小和自动工作流程驱动的转换以及管理再现的能力是Experience Manager Media Library的一部分。 这些功能不需要资产许可。

### 我想使用自定义的图像组件调整图像大小。 我需要资产吗？ {#i-want-to-resize-images-using-a-customized-image-component-do-i-need-aem-assets}

图像组件是WCM的一部分。 图像组件（也由Assets）使用的图形库是Experience Manager平台的一部分，不需要Assets许可证。

### 如果我未授权使用资产，如何阻止我的用户使用资产？ {#how-can-i-prevent-my-users-from-using-aem-assets-if-i-did-not-license-aem-assets}

您可以从Experience Manager中删除所有特定于资产的工作流、组件、分类、选项和资产管理员。 这样做可防止用户意外使用您未授权的资产功能。

### 我要向页面添加图像，并要裁切和调整这些图像的大小。 我需要资产吗？ {#i-want-to-add-images-to-a-page-and-want-to-crop-and-resize-these-images-do-i-need-aem-assets}

在此用例中，无需购买资产，即使使用媒体库也无需在网站上使用图像，因为智能图像组件允许将图像直接上传到页面。

### 资产与媒体库中可用功能的详细列表 {#listoffeatures}

**Experience Manager Assets**

* 收藏集和Lightbox
* 高级元数据属性和管理
* Adobe Asset Link（连接到适用于企业的Creative Cloud）
* Experience Manager 桌面应用程序
* 处理配置文件
* [!DNL Adobe InDesign Server] 集成
* 资产模板和目录制作者框架
* [!DNL Adobe Photoshop]、 [!DNL Adobe Illustrator]和集 [!DNL Adobe InDesign] 成
* 多语言资产管理
* PIM集成
* 权限管理
* 相机RAW支持
* 搜索彩块化管理和配置
* 预建的DAM工作流（例如，照片拍摄）
* 称为“洞察”的资产报告和分析
* 3D资源管理
* 连接的资产
* Brand Portal
* 自助访问
* 浏览、搜索和下载
* 集合和文件夹共享
* 管理工具和界面
* 智能标记
* 视觉搜索

**媒体库**

* 基本元数据属性
* 标签管理
* 版本控制
* 静态演绎版
* 项目，任务，工作流创作
* 活动流（时间轴）
* 查询生成器(API)
* Marketing Cloud集成
* UI自定义和扩展
* 注释和注释
