---
title: 主题自定义
seo-title: 主题自定义
description: 如何自定义AEM Forms应用程序的主题。
seo-description: 如何自定义AEM Forms应用程序的主题。
uuid: 36632e67-1cc6-416d-ae80-d84bbabab4bd
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: c72f608e-052a-4bf9-b7bc-ddf57483af35
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317

---


# 主题自定义 {#theme-customization}

您可以自定义HTML代码和CSS文件，为AEM Forms应用程序提供独特的组织特定外观。 例如，可以更改任务或起点的背景颜色和高度。 以下示例提供了更改说明：

* 显示说明代替说明
* 显示路由数
* 背景渐变色

## 步骤 {#steps}

1. 打开您的项目。

   * 对于iOS，在Xcode `Capture.xcodeproj` 中打开
   * 对于Android，在Eclipse中打开Android项目。
   * 对于Windows，请在Visual `MWSWindows.sln` Studio中打开。

1. 导览至模板文件夹。

   * 在Xcode中，导航到“捕 **捉”>“www”>“wsmobile”>“js”>“运行时”>“模板** ”文件夹。
   * 在Eclipse中，导航到资产> www > wsmobile > js > runtime > templates文 **件夹** 。
   * 在Visual Studio中，导航到 **MWSWindows > www > wsmobile > js > runtime > templates文件夹** 。

1. Open the `template.html` file for editing.
1. 找到以下字符串：

   ```
   <%if ( (task.description !== "") && (task.description !== null) && (typeof task.description !== null) && (typeof task.description !== 'undefined') ) {%>
                  <div class="description_details">
                    <%= task.description %>
                  </div>
                 <%} else
   ```

   将其替换为 `<%`。

1. 在文件中找到以下代 `template.html` 码：

   ```
   <ul id="task_menu_list">
                                   <li class="approve" title="<%= task.availableCommands.directCommands[0]%>" data-routename="<%= task.availableCommands.directCommands[0]%>">
                                       <%= task.availableCommands.directCommands[0]%>
                                   </li>
                                   <li class="reject last" title="<%= task.availableCommands.directCommands[1]%>" data-routename="<%= task.availableCommands.directCommands[1]%>">
                                       <%= task.availableCommands.directCommands[1]%>
                                   </li>
   ```

1. 注释以下行并保存文件。

   ```
   task.availableCommands.directCommands[1]%>">
   <%= task.availableCommands.directCommands[1]%>
   </li>
   ```

1. 导览至css文件夹。

   * 在Xcode中，导航到 **Capture > www > wsmobile > css**。
   * 在Eclipse中，导航到资 **源> www > wsmobile > css**。
   * 在Visual Studio中，导航到 **MWSWindows > www > wsmobile > css**。

1. Open the `_style.css` file for editing.
1. 对于背景图像，请更 `#323232` 改为 `#fff`。
1. 保存更改并关闭 `_style.css` 文件。
1. 打开AEM Forms应用程序。

   AEM Forms应用程序现在显示说明而非说明。
