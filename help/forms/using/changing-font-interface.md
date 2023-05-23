---
title: 變更介面的字型
seo-title: Changing the font on the interface
description: 如何選擇性地變更使用者介面上的字型。
seo-description: How to change the fonts on the user interface selectively.
uuid: 421fdd24-441a-4092-8c52-f3ed3d5d5671
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 9fcb80b4-cbc2-48a5-afd1-4f3bc50bc503
docset: aem65
exl-id: 226f70f0-8eb4-4724-b496-5801dc6b436f
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '276'
ht-degree: 1%

---

# 變更介面的字型{#changing-the-font-on-the-interface}

您可以變更AEM Forms工作區中顯示的字型。 在使用者介面的特定區段中使用的字型，會在樣式表的對應區段中定義。 您可以選擇性地變更使用者介面上的字型。

請遵循 [AEM Forms工作區自訂的一般步驟](../../forms/using/generic-steps-html-workspace-customization.md) 並根據您的需求，遵循自訂CSS、HTML或兩者的步驟。

1. 在現有樣式中變更或新增字型系列。
1. 變更或新增HTML元素的字型系列內嵌。
1. 新增樣式並將其用於HTML元素。

例如，若要將頂端導覽列錨點文字的字型變更為Courier New，請遵循下列步驟：

1. 透過存取登入CRXDE Lite `https://'[server]:[port]'/lc/crx/de/index.jsp`.
1. 执行下列操作之一：

   1. 若要變更現有樣式中的font-family，請在/apps/ws/css的newStyle.css檔案中新增下列內容。

      ```css
      #topnav a {
         font-family: "Courier New";
      }
      ```

   1. 若要為HTML元素新增字型系列內嵌，請複製 `/libs/ws/js/runtime/templates/appnavigation.html` 檔案至 `/apps/ws/js/runtime/templates/appnavigation.html`.

      更新/apps/ws/js/runtime/templates/appnavigation.html檔案，如下所示：

      ```jsp
      <li class="process"><a href="#" title="<%= $.t('index.header.topnav.startprocess.detail')%>" style="font-family:Courier New;" ><%= $.t('index.header.topnav.startprocess.name')%></a></li>
      <li class="todo"><a href="#/todo" title="<%= $.t('index.header.topnav.todo.detail')%>" style="font-family:Courier New;" ><%= $.t('index.header.topnav.todo.name')%></a></li>
      <li class="track"><a href="#/tracking" title="<%= $.t('index.header.topnav.tracking.detail')%>" style="font-family:Courier New;" ><%= $.t('index.header.topnav.tracking.name')%></a></li>
      <li class="preference"><a href="#/preferences" title="<%= $.t('index.header.topnav.preferences.detail')%>" style="font-family:Courier New;" ><%= $.t('index.header.topnav.preferences.name')%></a></li>
      ```

      開啟/apps/ws/js/registry.js檔案進行編輯和取代 `text!/lc/libs/ws/js/runtime/templates/appnavigation.html` 替換為 `text!/lc/apps/ws/js/runtime/templates/appnavigation.html`.

   1. 若要新增定義font-family的樣式，請在/apps/ws/css的newStyle.css檔案中新增下列內容。

      ```css
      .myNewFontStyle a {
         font-family: "Courier New";
      }
      ```

      若要為HTML元素新增字型系列內嵌，請在/apps/ws/js/runtime/templates的appnavigation.html檔案中新增下列內容。

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

1. 重新啟動工作區並清除瀏覽器快取，使變更可見。

![change_font_before](assets/change_font_before.png)

字型自訂前的頂端導覽列

![change_font_after](assets/change_font_after.png)

第一個索引標籤的字型自訂後的頂端導覽列
