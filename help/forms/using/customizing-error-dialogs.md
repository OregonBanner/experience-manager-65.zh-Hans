---
title: 自定义错误对话框
seo-title: 自定义错误对话框
description: 如何自定义LiveCycleAEM Forms工作区的错误对话框，以添加不同的错误描述。
seo-description: 如何自定义LiveCycleAEM Forms工作区的错误对话框，以添加不同的错误描述。
uuid: 5ed1da68-bd5b-4a36-9a14-9d61733237e6
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: f547c0c1-3917-4092-9d63-c1b3aaefcef0
translation-type: tm+mt
source-git-commit: 07abce0e6e4d1a299ce32ab130366b4e676b6388
workflow-type: tm+mt
source-wordcount: '170'
ht-degree: 4%

---


# 自定义错误对话框 {#customizing-error-dialogs}

AEM Forms工作区允许您自定义错误对话框。 对AEM Forms工 [作区进行自定义](/help/forms/using/generic-steps-html-workspace-customization.md) ，请执行常规步骤，然后执行以下步骤以自定义错误对话框。

## 自定义文本 {#customizing-text}

1. 在文 `/apps/ws/locales/en-US/translation.json` 件中，更改自定 `wserror` 义值的值。 例如：

   ```json
   "wserror" : {
    "message" : "Message:",
    "ComponentUI" : "Component UI:",
    "error" : "Error",
    "ok" : "Ok",
    "ErrorCode" : "Error Code:"
    }
   ```

   收件人

   ```json
    "wserror" : {
    "message" : "Error Message:",
    "ComponentUI" : "UI Component:",
    "error" : "Something went wrong!!",
    "ok" : "Ok",
    "ErrorCode" : "Error Code:"
    }
   ```

   >[!NOTE]
   >
   >为所有支持的语言添加相应的键值对。

## 自定义CSS {#customizing-css}

1. 您可以通过在文件中添加以下代码片断来更新对话框、标题、内容区域、脚栏、脚栏按钮和其他 `/apps/ws/css/newStyle.css` 抵押品：

   ```css
   /*-------- Error Dialog -------------------------------------------------------------------------------------------------------------------*/
   .error-dialog{
       border: 2px solid #DEDEDE;
       width: 540px;
       height: 400px;
       position: absolute;
       z-index: 99999;
       left: 50%;
       margin-left: -271px;
       background:#2b2b2b;
       box-shadow:0px 0px 10px 3px #888;
       display:none;
   }
   .error-dialog .head-bar{
       height: 31px;
       background: url(../images/error.png) no-repeat 7px 10px #DEDEDE;
       color: #2B2B2B;
       font-size: 18px;
       padding-left: 30px;
       padding-top: 7px;
       text-overflow: ellipsis;
       overflow: hidden;
       white-space: nowrap;
   }
   .error-dialog .content-area{
       padding: 20px;
       border-bottom: 1px solid #1B1B1B;
       height: 268px;
   }
   .error-dialog .foot-bar{
       border-top: 1px solid #404040;
       height: 32px;
       padding:10px;
       text-align: right;
   }
   .error-dialog .foot-bar button{
       background: #52a1dc; /* Old browsers */
       background: -moz-linear-gradient(top,  #52a1dc 0%, #2680ce 100%, #207cca 100%, #2989d8 100%, #207cca 100%); /* FF3.6+ */
       background: -webkit-gradient(linear, left top, left bottom, color-stop(0%,#52a1dc), color-stop(100%,#2680ce), color-stop(100%,#207cca), color-stop(100%,#2989d8), color-stop(100%,#207cca)); /* Chrome,Safari4+ */
       background: -webkit-linear-gradient(top,  #52a1dc 0%,#2680ce 100%,#207cca 100%,#2989d8 100%,#207cca 100%); /* Chrome10+,Safari5.1+ */
       background: -o-linear-gradient(top,  #52a1dc 0%,#2680ce 100%,#207cca 100%,#2989d8 100%,#207cca 100%); /* Opera 11.10+ */
       background: -ms-linear-gradient(top,  #52a1dc 0%,#2680ce 100%,#207cca 100%,#2989d8 100%,#207cca 100%); /* IE10+ */
       background: linear-gradient(to bottom,  #52a1dc 0%,#2680ce 100%,#207cca 100%,#2989d8 100%,#207cca 100%); /* W3C */
       filter: progid:DXImageTransform.Microsoft.gradient( startColorstr='#52a1dc', endColorstr='#2680ce',GradientType=0 ); /* IE6-9 */
       border: #4F748F;
       height: 30px;
       width: 100px;
       font-size: 18px;
       color: white;
   
   }
   .error-dialog .single-col{
       width: 100%;
       list-style-type: none;
       padding: 0px;
       margin: 0px;
   }
   .error-dialog .single-col li{
       height: 28px;
       font-size:14px;
       color:#bebebe;
       text-overflow: ellipsis;
       overflow: hidden;
       white-space: nowrap;
   }
   .error-dialog .single-col li label{
       height: 28px;
       color:#fff;
       max-width:100px;
       margin-right: 14px;
       text-overflow: ellipsis;
       overflow: hidden;
       white-space: nowrap;
       float: left;
   }
   .error-dialog .double-col{
       width: 100%;
       list-style-type: none;
       padding: 0px;
       margin:0px;
   }
   .error-dialog .double-col li{
       height: 28px;
       font-size:14px;
       color:#bebebe;
       width: 50%;
       float: left;
       text-overflow: ellipsis;
       white-space: nowrap;
       overflow: hidden;
   }
   .error-dialog .double-col li.small{
       width: 30%;
   }
   .error-dialog .double-col li.big{
       width: 70%;
   }
   .error-dialog .double-col li label{
       height: 28px;
       color:#fff;
       max-width:100px;
       margin-right: 14px;
       text-overflow: ellipsis;
       overflow: hidden;
       white-space: nowrap;
       float: left;
   }
   .error-dialog .scroll-content{
       color:#bebebe;
       font-size:12px;
       height:175px;
       overflow-y:scroll;
       overflow-x:hidden;
       width:100%;
   
   }
   
   .error-background, .popup-background, .wsMessageBackGround, .userInfoBackGround, .busyState, .aboutWorkspaceBG {
       width: 100%;
       height: 100%;
       display: none;
       opacity: 0.6;
       background-color: black;
       left: 0px;
       top: 0px;
       position: fixed;
       z-index: 999;
       margin: 0px;
       padding: 0px;
   }
   ```

1. 对于脚条按钮跨度，将和按 `.error-dialog` 钮跨 `.foot-bar` 度与复合列表分开。 要进行此更改，请在newStyle.css文件中添加以下内容：

   ```css
   .browse-btn span, .attachementbtn span, .cancelAttachmentUpdate span, #taskAttachmentsContainer .uploadStatus span, .submitNoteButton span, .updateNoteButton span, .cancelNoteUpdate span,
   #userSearchPopUp #actionbar span, #taskarea .action button span, .error-dialog .foot-bar button span, .oooAction button span, .wsMessageContainerDiv .action button span
   {
       display: block;
       text-overflow: ellipsis;
       white-space: nowrap;
       overflow: hidden;
   }
   ```

   收件人

   ```css
   .browse-btn span, .attachementbtn span, .cancelAttachmentUpdate span, #taskAttachmentsContainer .uploadStatus span, .submitNoteButton span, .updateNoteButton span, .cancelNoteUpdate span,
   #userSearchPopUp #actionbar span, #taskarea .action button span, .oooAction button span, .wsMessageContainerDiv .action button span
   {
       display: block;
       text-overflow: ellipsis;
       white-space: nowrap;
       overflow: hidden;
   }
   
   /*-------- Customized following Portion --------*/
   .error-dialog .foot-bar button span
   {
       display: block;
       text-overflow: ellipsis;
       text-decoration:underline;
       white-space: wrap;
   }
   ```

>[!NOTE]
>
>如果您引用的是其他图像，请在所需的层次结构下添加 `/apps/ws/images`。

## 示例 {#examples}

* **要自定义错误对话框，请更改：**

```css
.error-dialog{
    border: 2px solid #DEDEDE;
    width: 540px;
    height: 400px;
    position: absolute;
    z-index: 99999;
    left: 50%;
    margin-left: -271px;
    background:#2b2b2b;
    box-shadow:0px 0px 10px 3px #888;
    display:none;
}
```

收件人

```css
.error-dialog{
    border: 9px solid #DEDEDE;
    width: 200px;
    height: 200px;
    position: absolute;
    z-index: 99999;
    left: 50%;
    margin-left: -271px;
    background: url(../images/my-error-bg.png) no-repeat 7px 10px #DEDEDE;
    box-shadow:0px 0px 10px 3px #888;
    display:none;
}
```

* **要自定义错误对话框标题，请更改：**

```css
.error-dialog .head-bar{
    height: 31px;
    background: url(../images/error.png) no-repeat 7px 10px #DEDEDE;
    color: #2B2B2B;
    font-size: 18px;
    padding-left: 30px;
    padding-top: 7px;
    text-overflow: ellipsis;
    overflow: hidden;
    white-space: nowrap;
}
```

收件人

```css
.error-dialog .head-bar{
    height: 40px;
    background: url(../images/error.png) no-repeat 7px 10px #DEDEDE;
    color: #FA0E39;
    font-size: 18px;
    padding-left: 30px;
    padding-top: 15px;
}
```
