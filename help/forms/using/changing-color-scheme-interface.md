---
title: 更改界面的颜色方案
seo-title: 更改界面的颜色方案
description: 如何有选择地修改AEM Forms工作区用户界面部分的颜色方案。
seo-description: 如何有选择地修改AEM Forms工作区用户界面部分的颜色方案。
uuid: 32c32f7a-8271-4d2c-8a1f-ad5ab3c90b83
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 18dab82a-badf-4c32-83a2-cd5cb04cae89
exl-id: e0a261a2-518b-4984-a5b5-24f0b9222e24
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 0%

---

# 更改接口{#changing-the-color-scheme-of-the-interface}的颜色方案

您可以修改AEM Forms工作区用户界面部分的颜色方案，以符合您的要求。 以下是一些代表性颜色方案自定义的示例。 除了本文中讨论的步骤之外，请参阅[AEM Forms工作区自定义的一般步骤](/help/forms/using/generic-steps-html-workspace-customization.md)。

## 顶部导航栏{#top-navigation-bar}

### 使用背景图像{#using-background-image}

更新位于AEM Forms工作区顶部的导航栏。

1. 创建背景图像以更新颜色。 将文件命名为newBackground.jpg。
1. 使用WebDAV客户端在/apps/ws/images文件夹中上传背景图像文件。

   >[!NOTE]
   >
   >有关WebDAV访问的更多信息，请参阅[https://dev.day.com/docs/en/crx/current/how_to/webdav_access.html](https://docs.adobe.com/docs/en/crx/current/how_to/webdav_access.html)。

1. 通过添加以下样式，在/apps/ws/css/newStyle.css中引用新的背景图像。

   ```css
   #header {
       background:#292929 url(../images/newBackground.jpg) repeat-x;
   }
   ```

### 在CSS {#using-color-property-in-css}中使用颜色属性

1. 在/apps/ws/css的newStyle.css中添加以下样式

   ```css
   #header {
   background : none;
   background-color: gray;
   }
   ```

## 类别组件{#category-component}

类别组件在左侧面板中显示各种类别的任务。 要更改其颜色，请在CSS文件的`.category`元素中定义背景颜色。

## 任务组件{#task-component}

任务显示在名为TaskList组件的中间面板中。 要更改其颜色，请修改样式表中与.task选择器关联的样式。
