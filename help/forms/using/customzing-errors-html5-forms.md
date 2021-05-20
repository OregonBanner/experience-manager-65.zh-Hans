---
title: 为HTML5表单自定义错误消息
seo-title: 为HTML5表单自定义错误消息
description: 了解如何自定义HTML5表单错误消息的显示，包括如何更改其位置和外观。
seo-description: 了解如何自定义HTML5表单错误消息的显示，包括如何更改其位置和外观。
uuid: 6f48b64e-858f-4323-ad50-88e25f3c2e3d
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
discoiquuid: 44e49789-9075-41b3-bce8-03e8efce2d5a
feature: 移动设备表单
exl-id: c4ae53a3-8de1-4985-a73e-829749de9814
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '543'
ht-degree: 0%

---

# 自定义HTML5表单{#customizing-error-messages-for-html-forms}的错误消息

在HTML5表单中，现成的错误消息和警告具有固定的位置和外观（字体和颜色），仅为选定字段显示错误，并且只显示一个错误。

本文提供了将HTML5表单错误消息自定义到、

* 更改错误消息的外观和位置。 您可以在任何字段的顶部、底部和右侧显示错误。
* 在任何给定时刻显示多个字段的错误消息。
* 显示错误，而不考虑是否选择了字段。

## 自定义错误消息  {#customizing-error-messages-nbsp}

在自定义错误消息之前，请下载并解压附加的包(CustomErrorManager-1.0-SNAPSHOT.zip)。

解压包后，打开CustomErrorManager-1.0-SNAPSHOT文件夹。 它包含jcr_root和META-INF文件夹。 这些文件夹包含自定义错误消息所需的CSS和.JS文件。

[获取文件](assets/customerrormanager-1.0-snapshot.zip)

### 自定义错误消息的位置  {#customizing-the-position-of-error-messages-nbsp}

要自定义错误消息的位置，请为每个错误和警告字段添加&lt;div>标记，将&lt;div>标记放置在左侧或右侧，并在&lt;div>标记上应用css样式。 有关详细步骤，请参阅下面列出的步骤：

1. 导航到`CustomErrorManager-1.0-SNAPSHOT`文件夹并打开`etc\clientlibs\mf-custom-error-manager\CustomErrorManager\javascript`文件夹。
1. 打开`customErrorManager.js`文件进行编辑。 文件中的`markError`函数接受以下参数：

   |  |  |
   |---|---|
   | jqWidget | jqWidget是小组件的句柄。 |
   | msg | 包含错误消息 |
   | 类型 | 指示是错误还是警告 |

1. 在开箱即用的实施中，字段右侧会显示错误消息。 要使错误消息显示在顶部，请使用以下代码。

   ```javascript
   markError: function (jqWidget, msg, type) {
               var element = jqWidget.element,                                //Gives the div containing widget
                   pos = $(element).offset(),                          //Calculates the position of the div in the view port
                                                                   msgHeight = xfalib.view.util.TextMetrics.measureExtent(msg).height + 5;  //Calculating the height of the Error Message
                   styles = {};
                   styles.left = pos.left + "px";         // Assign the desired left position using pos.left. Here it is calculated for exact left of the field
                   styles.top = pos.top - msgHeight + "px";  // Assign the desired top position using pos.top. Here it is calculated for top of the field
               if (type != "warning") {
                   if(!jqWidget.errorDiv){
                                                                                   //Adding the warning div if it is not present already
                       jqWidget.errorDiv=$("<div id='customError'></div>").appendTo('body');
                   }
                   jqWidget.$css(jqWidget.errorDiv.get(0), styles); // Applying the styles to the warning div
                   jqWidget.errorDiv.text(msg).show();                     //Showing the warning message
               } else {
                   if(!jqWidget.errorDiv){
                                                                                   //Adding the error div if it is not present already
                       jqWidget.errorDiv=$("<div id='customWarning'></div>").appendTo('body');
                   }
                   jqWidget.$css(jqWidget.errorDiv.get(0), styles); // Applying the styles to the error div
                   jqWidget.errorDiv.text(msg).show();                     //Showing the warning message
               }
   
           },
   ```

1. 保存并关闭文件。
1. 导航到`CustomErrorManager-1.0-SNAPSHOT`文件夹，并创建jcr_root和META-INF文件夹的存档。 将存档重命名为CustomErrorManager-1.0-SNAPSHOT.zip。
1. 使用包管理器上传和安装包。

## 显示多个字段的错误消息  {#display-error-messages-for-multiple-fields-nbsp}

使用附加的包同时显示所有字段的错误消息。 要显示单条错误消息，请使用默认用户档案。

### 自定义错误消息的外观。  {#customizing-the-appearance-of-error-messages-nbsp}

1. 导航到etc\clientlibs\mf-custom-error-manager\CustomErrorManager\css folder目录。

1. 打开要编辑的文件sample.css。css文件包含2个id- #customError、#customWarning。 您可以使用这些ID更改各种属性，如颜色、字体大小等。

   使用以下代码更改错误/警告消息的字体大小和颜色。

   ```css
   #customError {
   color: #0000FF; // it changes the color of Error Message
   display:none;
   position:absolute;
   opacity:0.85;
   font-size: 24px;  // it changes the font size of Error Message
   z-index:5;
   }
   
   #customWarning {
   color: #00FF00;  // it changes the color of Warning Message
   display:none;
   position:absolute;
   opacity:0.85;
   font-size: 18px;   // it changes the font size of Warning Message
   z-index:5;
   }
   
   Save the changes.
   ```

1. 保存并关闭文件。
1. 导航到CustomErrorManager-1.0-SNAPSHOT文件夹并创建jcr_root和META-INF文件夹的存档。 将存档重命名为CustomErrorManager-1.0-SNAPSHOT.zip。
1. 使用包管理器上传和安装包。

## 使用新配置文件渲染表单。  {#render-the-form-with-the-new-profile-nbsp}

html5表单现成使用默认配置文件：https://&lt;server>/content/xfaforms/profiles/default.html?contentRoot=&lt;xdp位置>&amp;template=&lt;xdp的名称>

要查看带有自定义错误消息的表单，请渲染带有错误配置文件的表单：https://&lt;server>/content/xfaforms/profiles/error.html?contentRoot=&lt;xdp位置>&amp;template=&lt;xdp的名称>

>[!NOTE]
>
>附加的包会安装错误配置文件。
