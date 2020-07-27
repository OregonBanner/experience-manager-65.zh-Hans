---
title: 更改界面上的字体
seo-title: 更改界面上的字体
description: 如何有选择地更改用户界面上的字体。
seo-description: 如何有选择地更改用户界面上的字体。
uuid: 421fdd24-441a-4092-8c52-f3ed3d5d5671
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 9fcb80b4-cbc2-48a5-afd1-4f3bc50bc503
docset: aem65
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 1%

---


# 更改界面上的字体{#changing-the-font-on-the-interface}

您可以更改在AEM Forms工作区中显示的字体。 在用户界面的特定部分中使用的字体在样式表的相应部分中定义。 您可以选择性地更改用户界面上的字体。

按照AEM Forms [工作区自定义的通用步骤](../../forms/using/generic-steps-html-workspace-customization.md) ，根据您的要求，按照自定义CSS、HTML或两者的步骤操作。

1. 以现有样式更改或添加字体系列。
1. 更改或添加HTML元素的行中字体系列。
1. 添加样式并将其用于HTML元素。

例如，要将顶部导航栏锚点文本的字体更改为Courier New，请执行以下步骤：

1. 通过访问登录到CRXDE `https://'[server]:[port]'/lc/crx/de/index.jsp`Lite。
1. 执行下列操作之一：

   1. 要更改现有样式的字体系列，请在newStyle.css文件（位于/apps/ws/css）中添加以下内容。

      ```css
      #topnav a {
         font-family: "Courier New";
      }
      ```

   1. 要为HTML元素添加行中的字体系列，请将文 `/libs/ws/js/runtime/templates/appnavigation.html` 件复制到 `/apps/ws/js/runtime/templates/appnavigation.html`。

      按如下方式更新/apps/ws/js/runtime/templates/appnavigation.html文件：

      ```jsp
      <li class="process"><a href="#" title="<%= $.t('index.header.topnav.startprocess.detail')%>" style="font-family:Courier New;" ><%= $.t('index.header.topnav.startprocess.name')%></a></li>
      <li class="todo"><a href="#/todo" title="<%= $.t('index.header.topnav.todo.detail')%>" style="font-family:Courier New;" ><%= $.t('index.header.topnav.todo.name')%></a></li>
      <li class="track"><a href="#/tracking" title="<%= $.t('index.header.topnav.tracking.detail')%>" style="font-family:Courier New;" ><%= $.t('index.header.topnav.tracking.name')%></a></li>
      <li class="preference"><a href="#/preferences" title="<%= $.t('index.header.topnav.preferences.detail')%>" style="font-family:Courier New;" ><%= $.t('index.header.topnav.preferences.name')%></a></li>
      ```

      打开/apps/ws/js/registry.js文件进行编辑并替换为 `text!/lc/libs/ws/js/runtime/templates/appnavigation.html` 该文 `text!/lc/apps/ws/js/runtime/templates/appnavigation.html`件。

   1. 要添加定义字体系列的样式，请在新的Style.css文件（位于/apps/ws/css）中添加以下内容。

      ```css
      .myNewFontStyle a {
         font-family: "Courier New";
      }
      ```

      要为HTML元素添加行中的字体系列，请在apps/ws/js/runtime/templates的appnavigation.html文件中添加以下内容。

      ```jsp
      <div id="topnav" class="myNewFontStyle">
          <ul>
              <li class="process"><a href="#" title="<%= $.t('index.header.topnav.startprocess.detail')%>" ><%= $.t('index.header.topnav.startprocess.name')%></a></li>
              <li class="todo"><a href="#/todo" title="<%= $.t('index.header.topnav.todo.detail')%>"><%= $.t('index.header.topnav.todo.name')%></a></li>
              <li class="track"><a href="#/tracking" title="<%= $.t('index.header.topnav.tracking.detail')%>" ><%= $.t('index.header.topnav.tracking.name')%></a></li>
              <li class="preference"><a href="#/preferences" title="<%= $.t('index.header.topnav.preferences.detail')%>" ><%= $.t('index.header.topnav.preferences.name')%></a></li>
          </ul>
      </div>
      ```

1. 重新启动工作区并清除浏览器缓存，以使更改可见。

![change_font_before](assets/change_font_before.png)

自定义字体之前的顶部导航栏

![change_font_after](assets/change_font_after.png)

自定义第一个选项卡的字体后的顶部导航栏
