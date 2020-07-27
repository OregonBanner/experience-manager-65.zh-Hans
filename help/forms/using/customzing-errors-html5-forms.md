---
title: 自定义HTML5表单的错误消息
seo-title: 自定义HTML5表单的错误消息
description: 了解如何自定义HTML5表单的错误消息显示，包括如何更改其位置和外观。
seo-description: 了解如何自定义HTML5表单的错误消息显示，包括如何更改其位置和外观。
uuid: 6f48b64e-858f-4323-ad50-88e25f3c2e3d
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
discoiquuid: 44e49789-9075-41b3-bce8-03e8efce2d5a
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '541'
ht-degree: 0%

---


# 自定义HTML5表单的错误消息 {#customizing-error-messages-for-html-forms}

在HTML5表单中，现成的错误消息和警告具有固定的位置和外观（字体和颜色），错误仅针对所选字段显示，只显示一个错误。

文章提供了将HTML5表单错误消息自定义为、

* 更改错误消息的外观和位置。 您可以在任何字段的顶部、底部和右侧显示错误。
* 在任意给定时刻显示多个字段的错误消息。
* 显示与字段无关的错误，无论是否已选择。

## 自定义错误消息  {#customizing-error-messages-nbsp}

在自定义错误消息之前，请下载并解压附加的包(CustomErrorManager-1.0-SNAPSHOT.zip)。

解压包后，打开CustomErrorManager-1.0-SNAPSHOT文件夹。 它包含jcr_root和META-INF文件夹。 这些文件夹包含自定义错误消息所需的CSS和。JS文件。

[获取文件](assets/customerrormanager-1.0-snapshot.zip)

### 自定义错误消息的位置  {#customizing-the-position-of-error-messages-nbsp}

要自定义错误消息的位置，请为每个错误和警告字段添加&lt;div>标记，在左侧或右侧放置&lt;div>标记，并在&lt;div>标记上应用css样式。 有关详细步骤，请参阅下面列出的步骤：

1. 导航到文 `CustomErrorManager-1.0-SNAPSHOT`件夹并打开文 `etc\clientlibs\mf-custom-error-manager\CustomErrorManager\javascript` 件夹。
1. Open the `customErrorManager.js` file for editing. 文件 `markError` 中的函数接受以下参数：

   |  |  |
   |---|---|
   | jqWidget | jqWidget是构件的句柄。 |
   | 味 | 包含错误消息 |
   | 类型 | 表示错误或警告 |

1. 在开箱即用的实现中，错误消息显示在字段的右侧。 要使错误消息显示在顶部，请使用以下代码。

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
1. 导览至文 `CustomErrorManager-1.0-SNAPSHOT` 件夹并创建jcr_root和META-INF文件夹的存档。 将存档重命名为CustomErrorManager-1.0-SNAPSHOT.zip。
1. 使用包管理器上传和安装包。

## 显示多个字段的错误消息  {#display-error-messages-for-multiple-fields-nbsp}

使用附加的包可同时显示所有字段的错误消息。 要显示单个错误消息，请使用默认用户档案。

### 自定义错误消息的外观。  {#customizing-the-appearance-of-error-messages-nbsp}

1. 导航到etc\clientlibs\mf-custom-error-manager\CustomErrorManager\css folder目录。

1. 打开要编辑的文件sample.css。css文件包含2个id- #customError, #customWarning。 您可以使用这些id更改各种属性，如颜色、字体大小等。

   使用以下代码更改错误／警告消息的字体大小和颜色。

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
1. 导航到CustomErrorManager-1.0-SNAPSHOT文件夹，创建jcr_root和META-INF文件夹的存档。 将存档重命名为CustomErrorManager-1.0-SNAPSHOT.zip。
1. 使用包管理器上传和安装包。

## 使用新用户档案渲染表单。  {#render-the-form-with-the-new-profile-nbsp}

现成的html5表单使用默认用户档案: https://&lt;server>/content/xfaforms/profiles/default.html?contentRoot=&lt;xdp location>&amp;template=&lt;xdp的名称>

要视图包含自定义错误消息的表单，请呈现包含错误用户档案的表单： https://&lt;server>/content/xfaforms/profiles/error.html?contentRoot=&lt;xdp location>&amp;template=&lt;xdp的名称>

>[!NOTE]
>
>附加的软件包会安装错误用户档案。

