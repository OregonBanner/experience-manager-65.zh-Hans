---
title: 参考信模板
seo-title: 参考信模板
description: 'AEM Forms提供了“对应管理”字母布局模板，您可以使用这些模板快速创建字母。 '
seo-description: 'AEM Forms提供了“对应管理”字母布局模板，您可以使用这些模板快速创建字母。 '
uuid: 3b2312d9-daa0-435b-976f-4969b54c5056
products: SG_EXPERIENCEMANAGER/6.3/FORMS
content-type: reference
topic-tags: correspondence-management
discoiquuid: afeb9f4d-3feb-4a0e-8884-e3ec1309b33b
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f

---


# 参考信模板 {#reference-letter-templates}

在“对应管理”中，字母模板包含典型的表单字段、页眉和页脚等布局功能以及用于放置内容的空“目标区域”。

对应管理在AEM Forms包 [AEM-FORMS.-REFERENCE-LAYOUT-TEMPLATES中提供字母模板](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq630/fd/AEM-FORMS-6.3-REFERENCE-LAYOUT-TEMPLATES)。 有关安装包的信息，请参 [阅如何使用包](/help/sites-administering/package-manager.md)。 您可以根据品牌和业务需求在Designer中自定义模板。 该包包含以下模板：

* 经典
* 经典Simple
* 平衡左
* 平衡右
* 可视左侧
* 视觉效果
* 视觉顶部——经典

安装包后，布局模板(XDP)列在templates-folder中的以下位置：

`https://'[server]:[port]'/[context-root]/aem/forms.html/content/dam/formsanddocuments/templates-folder`

以下是此包中所有模板中的常用字段：

* 日期
* 致敬
* 关闭文本
* 签名文本

![列出所有CM字母模板](assets/templatescorrespondence.png)

安装AEM-FORMS-6.3-REFERENCE-LAYOUT-TEMPLATES包后，模板将列在templates-folder中

## 经典 {#classic}

Classic模板顶部有标志，适合用于简朴的专业字母。

![经典](assets/classic.png)

PDF预览使用经典模板创建的字母

## 经典Simple {#classic-simple}

包括用于捕获电话号码和电子邮件地址的字段。 经典简单模板与经典模板类似，只是它没有可以输入收件人地址的字段。

![联系信息片段](assets/classicsimple.png)

PDF预览使用经典简单模板创建的字母

## 平衡左 {#balanced-left}

“平衡左侧”模板在字母左侧包含徽标。

![平衡左](assets/balancedleft.png)

使用“平衡左”模板创建的字母的PDF预览

## 平衡右 {#balanced-right}

“平衡右侧”模板左侧有公司徽标，并为在字母本身上输入收件人地址提供了空间。 “平衡右侧”模板还包括一个页脚，当您的字母有多个页面时，该页脚会重排。

![平衡](assets/balancedright.png)

使用“平衡右侧”模板创建的字母的PDF预览

## 可视左侧 {#visual-left}

“可视左侧”模板的左侧有一个侧标题，侧标题上方放置有公司标志。 Visual Left template has a subject field but no footer.

![visualleft](assets/visualleft.png)

PDF preview of a letter created using the Visual Left template

## Visual Top {#visual-top}

“视觉效果最佳”模板顶部有视觉边距。 The Visual Top template has a field for entering recipient&#39;s address on the page itself. The Visual Top template has the subject field and a footer that reflows for letters that extend to multiple pages.

![visualtop](assets/visualtop.png)

PDF preview of a letter created using the Visual Top template

## 视觉顶部——经典 {#visual-top-classic}

The Visual Top - Classic template has a header on top of the page with the company logo. “视觉效果最佳——经典”模板有一个字段用于输入主题，但没有页脚。

![visualtopclassic](assets/visualtopclassic.png)

PDF预览使用视觉顶部——经典模板创建的字母

