---
title: 佈景主題自訂
seo-title: Theme Customization
description: 如何自訂AEM Forms應用程式的主題。
seo-description: How to customize the theme of your AEM Forms app.
uuid: 36632e67-1cc6-416d-ae80-d84bbabab4bd
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: c72f608e-052a-4bf9-b7bc-ddf57483af35
exl-id: 9b8c5933-b783-48f9-b463-15a01e06ee98
source-git-commit: 6bc228866aca785ec768daefb73970fc24568ef0
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 0%

---

# 佈景主題自訂 {#theme-customization}

您可以自訂HTML程式碼和CSS檔案，為AEM Forms應用程式提供獨特的組織專屬外觀和風格。 例如，您可以變更任務或「起點」的背景顏色和高度。 以下範例提供變更的指示：

* 顯示指示以取代說明
* 顯示路由數目
* 背景漸層顏色

## 步骤 {#steps}

1. 開啟您的專案。

   * 若為iOS，請開啟 `Capture.xcodeproj` 在Xcode中
   * 若是Android，請在Eclipse中開啟Android專案。
   * 若是Windows，請開啟 `MWSWindows.sln` 在Visual Studio中。

1. 導覽至templates資料夾。

   * 在Xcode中，導覽至 **擷取> www > wsmobile > js >執行階段>範本** 資料夾。
   * 在Eclipse中，導覽至 **資產> www > wsmobile > js >執行階段>範本** 資料夾。
   * 在Visual Studio中，導覽至 **MWSWindows > www > wsmobile > js >執行階段>範本** 資料夾。

1. 開啟 `template.html` 檔案進行編輯。
1. 找出下列字串：

   ```jsp
   <%if ( (task.description !== "") && (task.description !== null) && (typeof task.description !== null) && (typeof task.description !== 'undefined') ) {%>
                  <div class="description_details">
                    <%= task.description %>
                  </div>
                 <%} else
   ```

   取代為 `<%`.

1. 在「 」中找到以下程式碼 `template.html` 檔案：

   ```jsp
   <ul id="task_menu_list">
                                   <li class="approve" title="<%= task.availableCommands.directCommands[0]%>" data-routename="<%= task.availableCommands.directCommands[0]%>">
                                       <%= task.availableCommands.directCommands[0]%>
                                   </li>
                                   <li class="reject last" title="<%= task.availableCommands.directCommands[1]%>" data-routename="<%= task.availableCommands.directCommands[1]%>">
                                       <%= task.availableCommands.directCommands[1]%>
                                   </li>
   ```

1. 註解下列行並儲存檔案。

   ```jsp
   task.availableCommands.directCommands[1]%>">
   <%= task.availableCommands.directCommands[1]%>
   </li>
   ```

1. 導覽至css資料夾。

   * 在Xcode中，瀏覽至 **擷取> www > wsmobile > css**.
   * 在Eclipse中，導覽至 **資產> www > wsmobile > css**.
   * 在Visual Studio中，導覽至 **MWSWindows > www > wsmobile > css**.

1. 開啟 `_style.css` 檔案進行編輯。
1. 背景影像，變更 `#323232` 至 `#fff`.
1. 儲存變更並關閉 `_style.css` 檔案。
1. 開啟AEM Forms應用程式

   AEM Forms應用程式現在會顯示指示，而非說明。
