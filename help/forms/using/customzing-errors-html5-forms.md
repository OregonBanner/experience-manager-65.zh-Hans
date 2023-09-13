---
title: 自定义HTML5表单的错误消息
description: 了解如何自定义HTML5表单的错误消息显示，包括如何更改其位置和外观。
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
feature: Mobile Forms
exl-id: c4ae53a3-8de1-4985-a73e-829749de9814
source-git-commit: 5af420c8e95fed88a8516cce27b8bbc7d3974e75
workflow-type: tm+mt
source-wordcount: '499'
ht-degree: 3%

---

# 自定义HTML5表单的错误消息 {#customizing-error-messages-for-html-forms}

在HTML5表单中，开箱即用的错误消息和警告具有固定的位置和外观（字体和颜色），仅对选定字段显示错误，并且只显示一个错误。

本文提供了自定义HTML5表单错误消息的步骤，以便您可以执行以下操作：

* 更改错误消息的外观和位置。 您可以生成错误以显示于任何字段的顶部、底部和右侧。
* 在任意给定时刻显示多个字段的错误消息。
* 无论是否选择字段，都会显示错误。

## 自定义错误消息  {#customizing-error-messages-nbsp}

在自定义错误消息之前，请下载并提取附加的包(CustomErrorManager-1.0-SNAPSHOT.zip)。

提取包后，打开CustomErrorManager-1.0-SNAPSHOT文件夹。 它包含jcr_root和META-INF文件夹。 这些文件夹包含自定义错误消息所需的CSS和.JS文件。

[获取文件](assets/customerrormanager-1.0-snapshot.zip)

### 自定义错误消息的位置  {#customizing-the-position-of-error-messages-nbsp}

要自定义错误消息的位置，请添加 &lt;div> 标记每个错误和警告字段，放置 &lt;div> 标签上的样式，并将css样式应用于 &lt;div> 标记之前。 有关详细步骤，请参阅以下步骤：

1. 导航至 `CustomErrorManager-1.0-SNAPSHOT`文件夹并打开 `etc\clientlibs\mf-custom-error-manager\CustomErrorManager\javascript` 文件夹。
1. 打开 `customErrorManager.js` 文件以供编辑。此 `markError` 函数接受以下参数：

   |   |  |
   |---|---|
   | jqWidget | jqWidget是小组件的句柄。 |
   | msg | 包含错误消息 |
   | 类型 | 指示是错误还是警告 |

1. 在开箱即用的实施中，错误消息显示在字段的右侧。 若要在顶部显示错误消息，请使用以下代码。

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

1. 保存并关闭该文件。
1. 导航至 `CustomErrorManager-1.0-SNAPSHOT` 文件夹并创建jcr_root和META-INF文件夹的归档文件。 将存档重命名为CustomErrorManager-1.0-SNAPSHOT.zip。
1. 使用包管理器上传并安装包。

## 显示多个字段的错误消息  {#display-error-messages-for-multiple-fields-nbsp}

使用附加的包同时显示所有字段的错误消息。 要显示单个错误消息，请使用默认配置文件。

### 自定义错误消息的外观。  {#customizing-the-appearance-of-error-messages-nbsp}

1. 导航到etc\clientlibs\mf-custom-error-manager\CustomErrorManager\css文件夹。

1. 打开文件sample.css进行编辑。 css文件包含2个ID，即#customError和#customWarning。 您可以使用这些ID更改各种属性，如颜色和字体大小。

   使用以下代码可更改错误/警告消息的字体大小和颜色。

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

1. 保存并关闭该文件。
1. 导航到CustomErrorManager-1.0-SNAPSHOT文件夹，并创建jcr_root和META-INF文件夹的归档文件。 将存档重命名为CustomErrorManager-1.0-SNAPSHOT.zip。
1. 使用包管理器上传并安装包。

## 使用新配置文件呈现表单。  {#render-the-form-with-the-new-profile-nbsp}

html5表单现成使用默认配置文件： `https://&lt;server&gt;/content/xfaforms/profiles/default.html?contentRoot=&lt;xdp location&gt;&template=&lt;name of the xdp&gt;`

要查看带有自定义错误消息的表单，请使用错误配置文件渲染表单： `https://&lt;server&gt;/content/xfaforms/profiles/error.html?contentRoot=&lt;xdp location&gt;&template=&lt;name of the xdp&gt;`

>[!NOTE]
>
>附加的包将安装错误配置文件。
