---
title: 参考书信模板
description: AEM Forms提供了可用于快速创建信件的通信管理信件布局模板。
products: SG_EXPERIENCEMANAGER/6.3/FORMS
content-type: reference
topic-tags: correspondence-management
exl-id: 40d127b5-1ce6-41fb-ac4c-2bf7ae79da82
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '453'
ht-degree: 0%

---

# 参考书信模板 {#reference-letter-templates}

在通信管理中，信件模板包含典型的表单字段、布局功能（如页眉和页脚）以及用于内容投放的空“目标区域”。

通信管理在中提供信件模板 [AEM Forms附加组件包](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=en). 您可以根据品牌和业务需求在Designer中自定义模板。 该资源包包含以下模板：

* Classic
* Classic简单用法
* 平衡左侧
* 向右平衡
* 可视化左侧
* 视觉顶部
* Visual Top — 经典

安装包后，布局模板(XDP)将列在位于以下位置的templates-folder中：

`https://'[server]:[port]'/[context-root]/aem/forms.html/content/dam/formsanddocuments/templates-folder`

以下是此包中所有模板中的常用字段：

* 日期
* 致敬
* 关闭文本
* 签名文本

![列出了所有CM书信模板](assets/templatescorrespondence.png)

安装AEM-FORMS-6.3-REFERENCE-LAYOUT-TEMPLATES包后，模板将列在templates-folder中

## Classic {#classic}

Classic模板顶部带有徽标，非常适合于普通专业信件。

![classic](assets/classic.png)

使用ClassicPDF创建的信件的模板预览

## Classic简单用法 {#classic-simple}

包含用于捕获电话号码和电子邮件地址的字段。 Classic Simple模板与Classic模板类似，不同之处在于它没有可输入收件人地址的字段。

![联系信息片段](assets/classicsimple.png)

使用Classic SimplePDF创建的信件的模板预览

## 平衡左侧 {#balanced-left}

“平衡左侧”模板在信件左侧包含徽标。

![向左平衡](assets/balancedleft.png)

使用“左平衡”模板创建的信件的PDF预览

## 向右平衡 {#balanced-right}

Balanced Right模板左侧具有公司徽标，并为在信件本身中输入收件人地址提供了空间。 Balanced Right模板还包括一个页脚，当您的信件有多个页面时重排。

![balancedright](assets/balancedright.png)

使用“右平衡”模板创建的信件的PDF预览

## 可视化左侧 {#visual-left}

Visual Left模板在页面左侧有一个侧头，其中公司徽标放在侧头上方。 可视化左侧模板有一个主题字段，但没有页脚。

![可视化左侧](assets/visualleft.png)

使用“可视化左侧”PDF创建的信件的模板预览

## 视觉顶部 {#visual-top}

“可视化顶部”模板顶部有可视边距。 Visual Top模板中有一个字段，用于在页面本身中输入收件人的地址。 Visual Top模板具有“主题”字段和重排到多个页面的字母的页脚。

![visualtop](assets/visualtop.png)

使用Visual TopPDF创建的信件的模板预览

## Visual Top — 经典 {#visual-top-classic}

Visual Top - Classic模板的页面顶部有一个带有公司徽标的标题。 Visual Top - Classic模板中有一个字段用于输入主题，但没有页脚。

![visualtopclassic](assets/visualtopclassic.png)

使用Visual Top - ClassicPDF创建的信件的模板预览
