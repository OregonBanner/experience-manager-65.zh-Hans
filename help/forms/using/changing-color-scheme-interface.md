---
title: 更改接口的颜色方案
seo-title: 更改接口的颜色方案
description: 如何有选择地修改AEM Forms工作区用户界面部分的颜色方案。
seo-description: 如何有选择地修改AEM Forms工作区用户界面部分的颜色方案。
uuid: 32c32f7a-8271-4d2c-8a1f-ad5ab3c90b83
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 18dab82a-badf-4c32-83a2-cd5cb04cae89
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317

---


# 更改接口的颜色方案 {#changing-the-color-scheme-of-the-interface}

您可以修改AEM Forms工作区用户界面部分的颜色方案以满足您的要求。 以下是一些典型颜色方案自定义的示例。 除了本文中讨论的步骤之外，请参阅AEM Forms工 [作区自定义的常规步骤](/help/forms/using/generic-steps-html-workspace-customization.md)。

## Top navigation bar {#top-navigation-bar}

### 使用背景图像 {#using-background-image}

要更新AEM Forms工作区顶部的导航栏，请执行以下操作：

1. 创建背景图像以更新颜色。 将文件命名为newBackground.jpg。
1. 使用WebDAV客户端上传/apps/ws/images文件夹中的背景图像文件。

   >[!NOTE]
   >
   >有关WebDAV访问的详细信息，请参 [阅https://dev.day.com/docs/en/crx/current/how_to/webdav_access.html](https://docs.adobe.com/docs/en/crx/current/how_to/webdav_access.html)。

1. 通过添加以下样式在/apps/ws/css/newStyle.css中引用新的背景图像。

   ```css
   #header {
       background:#292929 url(../images/newBackground.jpg) repeat-x;
   }
   ```

### 在CSS中使用颜色属性 {#using-color-property-in-css}

1. 在/apps/ws/css的newStyle.css中添加以下样式

   ```css
   #header {
   background : none;
   background-color: gray;
   }
   ```

## 类别组件 {#category-component}

类别组件在左面板中显示您的任务的各种类别。 要更改其颜色，请在CSS文件的元 `.category` 素中定义背景颜色。

## 任务组件 {#task-component}

任务显示在称为TaskList组件的中间面板中。 要更改其颜色，请修改与样式表中的。任务选择器关联的样式。
