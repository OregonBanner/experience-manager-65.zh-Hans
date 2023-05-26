---
title: 更改界面的颜色方案
seo-title: Changing the color scheme of the interface
description: 如何有选择地修改AEM Forms workspace用户界面部分的配色方案。
seo-description: How to modify the color scheme of AEM Forms workspace user interface portions selectively.
uuid: 32c32f7a-8271-4d2c-8a1f-ad5ab3c90b83
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 18dab82a-badf-4c32-83a2-cd5cb04cae89
exl-id: e0a261a2-518b-4984-a5b5-24f0b9222e24
source-git-commit: 30327950779337ce869b6ca376120bc09826be21
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 3%

---

# 更改界面的颜色方案 {#changing-the-color-scheme-of-the-interface}

您可以根据自己的要求，修改AEM Forms workspace用户界面部分的配色方案。 以下是一些具有代表性的颜色方案自定义示例。 除了本文中讨论的步骤外，请参阅 [AEM Forms工作区自定义的一般步骤](/help/forms/using/generic-steps-html-workspace-customization.md).

## 顶部导航栏 {#top-navigation-bar}

### 使用背景图像 {#using-background-image}

更新AEM Forms工作区顶部的导航栏。

1. 创建背景图像以更新颜色。 将文件命名为newBackground.jpg。
1. 使用WebDAV客户端上传/apps/ws/images文件夹中的背景图像文件。

   >[!NOTE]
   >
   >有关WebDAV访问的详细信息，请参见 [https://dev.day.com/docs/en/crx/current/how_to/webdav_access.html](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=zh-Hans).

1. 通过添加以下样式，引用/apps/ws/css/newStyle.css中的新背景图像。

   ```css
   #header {
       background:#292929 url(../images/newBackground.jpg) repeat-x;
   }
   ```

### 在CSS中使用color属性 {#using-color-property-in-css}

1. 在/apps/ws/css的newStyle.css中添加以下样式

   ```css
   #header {
   background : none;
   background-color: gray;
   }
   ```

## 类别组件 {#category-component}

类别组件在左侧面板中显示任务的各个类别。 若要更改其颜色，请定义背景颜色 `.category` CSS文件的元素。

## 任务组件 {#task-component}

任务显示在称为TaskList组件的中间面板中。 要更改其颜色，请修改样式表中与.task选择器关联的样式。
