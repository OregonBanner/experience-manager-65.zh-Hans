---
title: Compare [!DNL Adobe Experience Manager Assets] 和媒体库产品。
description: 比较 [!DNL Experience Manager Assets] 和媒体库产品并了解不同之处。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 9fc1201db83ae0d3bb902d4dc3ab6d78cc1dc251
workflow-type: tm+mt
source-wordcount: '594'
ht-degree: 2%

---


# [!DNL Experience Manager Assets] 与媒 [!DNL Experience Manager] 体库 {#aem-assets-vs-aem-medialibrary}

[!DNL Adobe Experience Manager Assets] 是平台的一部分 [!DNL Experience Manager] 。 这种顺畅的集成被视为内容作者的一个主要优 [!DNL Experience Manager] 势，并确保内容管理的一致性和高效率。

## 常见问题 {#frequently-asked-questions}

### What is [!DNL Assets]? {#what-is-aem-assets}

[!DNL Assets] 是一种功能， [!DNL Experience Manager] 允许用户在基于Web的存储库中管理其数字资产(图像、视频、文档和音频剪辑)。 [!DNL Assets] 包括元数据支持、再现、查找器和管理界面。

### 什么是媒 [!DNL Experience Manager] 体库？ {#what-is-the-aem-media-library}

媒 [!DNL Experience Manager] 体库是WCM内容存储库的指定部 [!DNL Experience Manager] 分，存储图像和其他共享资源。 媒体库为WCM提供基本的数字资产管理功能。

### 这不属于WCM [!DNL Assets] 的部分，我还能得到什么？ {#what-do-i-get-from-aem-assets-that-is-not-part-of-aem-wcm}

只有以下客户才能使用的独特 [!DNL Assets] 功能：

* 能够提取和编辑除标题、标记和描述之外的元数据。
* 管理 [!DNL Assets] 员，可从欢迎屏幕中访问。
* 与数字资产管理相关的所有工作流步骤，如摄取、资产删除、子资产处理、元数据提取。
* 包空间 `dam` 中的库。

使用这些功能需要有效的许可证 [!DNL Assets]。

### 是否 [!DNL Assets] 可作为单独的包提供？ {#is-aem-assets-available-as-a-separate-package}

否. 为了简化安装和部署，所 [!DNL Experience Manager] 有应用程序和加载项都在一个包中提供，并包含所有功能。 这并不表示您有权使用包中的所有功能。

### 我想编辑数字资产的元数据。 我需要吗 [!DNL Assets]? {#i-want-to-edit-metadata-of-digital-assets-do-i-need-aem-assets}

如果您计划编辑除标题、描述和标记之外的元数据，则需要获得许可 [!DNL Assets]。

### 我想在我的网站上使用类别谓词。 我需要吗 [!DNL Assets]? {#i-want-to-use-the-category-predicate-on-my-website-do-i-need-aem-assets}

是，类别谓词是谓词的一 [!DNL Assets] 部分，需要许 [!DNL Assets] 可证。

### 我想在导入时自动调整图像大小。 我需要吗 [!DNL Assets]? {#i-want-to-automatically-resize-images-upon-import-do-i-need-aem-assets}

否. 调整静态图像的大小和自动工作流程驱动的转换以及管理再现的能力是媒体库的 [!DNL Experience Manager] 一部分。 这些功能不需要许 [!DNL Assets] 可证。

### 我想使用自定义的图像组件调整图像大小。 我需要吗 [!DNL Assets]? {#i-want-to-resize-images-using-a-customized-image-component-do-i-need-aem-assets}

图像组件是WCM的一部分。 图像组件（但也由）使用的图形库是平 [!DNL Assets]台的一部分， [!DNL Experience Manager] 不需要许可 [!DNL Assets] 证。

### 如果我未获得许可，如何 [!DNL Assets] 阻止我的用户使用 [!DNL Assets]? {#how-can-i-prevent-my-users-from-using-aem-assets-if-i-did-not-license-aem-assets}

您可以从中删除 [!DNL Assets]所有特定工作流、组件、分类、选项和管 [!DNL Assets] 理员 [!DNL Experience Manager]。 这样做可防止用户意外使用您 [!DNL Assets] 未授权的功能。

### 我要向页面添加图像，并要裁切和调整这些图像的大小。 我需要资产吗？ {#i-want-to-add-images-to-a-page-and-want-to-crop-and-resize-these-images-do-i-need-aem-assets}

在此用例中，无需购买，即 [!DNL Assets]使使用媒体库，也无需在网站上使用图像，因为智能图像组件允许将图像直接上传到页面。

### 详细的媒体库功 [!DNL Assets] 能列表 {#listoffeatures}

**Experience Manager Assets**

* 收藏集和Lightbox
* 高级元数据属性和管理
* Adobe资产链接(连接到企业Creative Cloud)
* [!DNL Experience Manager] 桌面应用程序
* 处理配置文件
* [!DNL Adobe InDesign Server] 集成
* 资产模板和目录制作者框架
* [!DNL Adobe Photoshop]、 [!DNL Adobe Illustrator]和集 [!DNL Adobe InDesign] 成
* 多语言资产管理
* PIM集成
* 权限管理
* Camera Raw支持
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
