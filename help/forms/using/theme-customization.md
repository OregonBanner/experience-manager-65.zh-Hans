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
exl-id: 9b8c5933-b783-48f9-b463-15a01e06ee98
source-git-commit: 6bc228866aca785ec768daefb73970fc24568ef0
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 0%

---

# 主题自定义 {#theme-customization}

您可以自定义HTML代码和CSS文件，以便为AEM Forms应用程序提供特定于组织的不同外观。 例如，您可以更改任务的背景颜色和高度或“起点”。 以下示例提供了更改说明：

* 显示说明代替说明
* 显示路由数
* 背景渐变颜色

## 步骤 {#steps}

1. 打开您的项目。

   * 对于iOS，在Xcode中打开`Capture.xcodeproj`
   * 对于Android，在Eclipse中打开Android项目。
   * 对于Windows，在Visual Studio中打开`MWSWindows.sln`。

1. 导航到模板文件夹。

   * 在Xcode中，导航到&#x200B;**Capture > www > wsmobile > js > runtime > templates**&#x200B;文件夹。
   * 在Eclipse中，导航到&#x200B;**assets > www > wsmobile > js > runtime > templates**&#x200B;文件夹。
   * 在Visual Studio中，导航到&#x200B;**MWSWindows > www > wsmobile > js > runtime > templates**&#x200B;文件夹。

1. 打开`template.html`文件进行编辑。
1. 找到以下字符串：

   ```jsp
   <%if ( (task.description !== "") && (task.description !== null) && (typeof task.description !== null) && (typeof task.description !== 'undefined') ) {%>
                  <div class="description_details">
                    <%= task.description %>
                  </div>
                 <%} else
   ```

   将其替换为`<%`。

1. 在`template.html`文件中找到以下代码：

   ```jsp
   <ul id="task_menu_list">
                                   <li class="approve" title="<%= task.availableCommands.directCommands[0]%>" data-routename="<%= task.availableCommands.directCommands[0]%>">
                                       <%= task.availableCommands.directCommands[0]%>
                                   </li>
                                   <li class="reject last" title="<%= task.availableCommands.directCommands[1]%>" data-routename="<%= task.availableCommands.directCommands[1]%>">
                                       <%= task.availableCommands.directCommands[1]%>
                                   </li>
   ```

1. 注释以下行并保存文件。

   ```jsp
   task.availableCommands.directCommands[1]%>">
   <%= task.availableCommands.directCommands[1]%>
   </li>
   ```

1. 导航到css文件夹。

   * 在Xcode中，导航至&#x200B;**Capture > www > wsmobile > css**。
   * 在Eclipse中，导航到&#x200B;**assets > www > wsmobile > css**。
   * 在Visual Studio中，导航到&#x200B;**MWSWindows > www > wsmobile > css**。

1. 打开`_style.css`文件进行编辑。
1. 对于背景图像，请将`#323232`更改为`#fff`。
1. 保存更改并关闭`_style.css`文件。
1. 打开AEM Forms应用程序。

   AEM Forms应用程序现在显示说明而不是描述。
