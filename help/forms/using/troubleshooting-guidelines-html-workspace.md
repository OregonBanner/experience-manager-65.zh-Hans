---
title: AEM Forms工作区疑难解答指南
seo-title: AEM Forms工作区疑难解答指南
description: 在浏览器中启用日志并使用调试器对AEM Forms工作区进行疑难解答。
seo-description: 在浏览器中启用日志并使用调试器对AEM Forms工作区进行疑难解答。
uuid: 07b8c8ed-f1ff-4be5-8005-251ff7b2ac85
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 5dae9ed9-77a3-44f5-a94d-ca5c355c8730
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317
workflow-type: tm+mt
source-wordcount: '747'
ht-degree: 0%

---


# AEM Forms工作区{#troubleshooting-guidelines-for-aem-forms-workspace}疑难解答指南

本文讨论如何通过启用日志记录和在浏览器中使用调试器调试AEM Forms工作区。 它还解释了在使用AEM Forms工作区时可能遇到的一些常见问题及其解决办法。

## 无法安装AEM Forms工作区包{#unable-to-install-aem-forms-workspace-package}

安装修补程序后，打开AEM Forms工作区。 如果遇到“找不到资源”错误，请打开CRX包管理器并重新安装`adobe-lc-workspace-pkg-<version>.zip`包。

安装包时，如果遇到错误`javax.jcr.nodetype.ConstraintViolationException: OakConstraint0025: Authorizable property rep:authorizableId may not be removed`，请执行以下步骤：

1. 登录CRX DE lite。 默认url为`https://[localhost]:'port'/lc/crx/de/index.jsp`
1. 删除以下节点：

   `/home/groups/P/PERM_WORKSPACE_USER`

1. 转到“包管理器”。 默认URL为`https://[localhost]:'port'/lc/crx/packmgr/index.jsp.`
1. 搜索并安装`adobe-lc-workspace-pkg-[version].zip`包。
1. 重新启动应用程序服务器。

## AEM Forms工作区日志{#aem-forms-workspace-nbsp-logging}

您可以在不同级别生成日志，以便对错误进行最佳故障诊断。 例如，在复杂的应用程序中，在组件级别进行日志记录有助于调试特定组件和排除特定组件故障。

在AEM Forms工作区中：

* 要获取有关特定组件文件的日志记录信息，请在URL后面追加`/log/<ComponentFile>/<LogLevel>`，然后按`Enter`。 在控制台上将打印指定日志级别的组件文件的所有日志信息。

* 要获取所有组件文件的日志记录信息，请在URL后面附加`/log/all/trace`，然后按`Enter`。

* 日志格式：`<Component file> <Date>:<Time>: <Log Level> : <Log Message>`

>[!NOTE]
>
>默认情况下，所有组件的日志级别均设置为INFO。

* 用户设置的日志级别仅对该浏览器会话进行维护。 当用户刷新页面时，日志级别将设置为其所有组件的初始值。

### AEM Forms工作区{#list-of-component-files-in-nbsp-aem-forms-workspace}中的组件文件列表

<table>
 <tbody>
  <tr>
   <td><p>allcategoryModel</p> </td>
   <td><p>processinstanceModel</p> </td>
   <td><p>tasklistModel</p> </td>
  </tr>
  <tr>
   <td><p>appnavigationModel</p> </td>
   <td><p>processInstanceView</p> </td>
   <td><p>tasklistView</p> </td>
  </tr>
  <tr>
   <td><p>appnavigationView</p> </td>
   <td><p>processnamelistModel</p> </td>
   <td><p>taskModel</p> </td>
  </tr>
  <tr>
   <td><p>categorylistModel</p> </td>
   <td><p>processnamelistView</p> </td>
   <td><p>taskView</p> </td>
  </tr>
  <tr>
   <td><p>categorylistView</p> </td>
   <td><p>processnameModel</p> </td>
   <td><p>teamqueuesView</p> </td>
  </tr>
  <tr>
   <td><p>categoryModel</p> </td>
   <td><p>processnameView</p> </td>
   <td><p>todoView</p> </td>
  </tr>
  <tr>
   <td><p>categoryView</p> </td>
   <td><p>searchtemplatedetailsView</p> </td>
   <td><p>trackingView</p> </td>
  </tr>
  <tr>
   <td><p>favoritecategoryModel</p> </td>
   <td><p>sharequeueModel</p> </td>
   <td><p>uisetingsModel</p> </td>
  </tr>
  <tr>
   <td><p>filterlistView</p> </td>
   <td><p>sharequeueView</p> </td>
   <td><p>设置视图</p> </td>
  </tr>
  <tr>
   <td><p>filterView</p> </td>
   <td><p>startpointlistModel</p> </td>
   <td><p>userinfoModel</p> </td>
  </tr>
  <tr>
   <td><p>outofoficeModel</p> </td>
   <td><p>startpointlistView</p> </td>
   <td><p>userinfoView</p> </td>
  </tr>
  <tr>
   <td><p>outofoficeView</p> </td>
   <td><p>startpointModel</p> </td>
   <td><p>usersearchModel</p> </td>
  </tr>
  <tr>
   <td><p>首选项视图</p> </td>
   <td><p>startpointView</p> </td>
   <td><p>usersearchView</p> </td>
  </tr>
  <tr>
   <td><p>processinstancehistoryView</p> </td>
   <td><p>startProcessView</p> </td>
   <td><p>wserrorModel</p> </td>
  </tr>
  <tr>
   <td><p>processinstancelistModel</p> </td>
   <td><p>startprocessView</p> </td>
   <td><p>wserrorView</p> </td>
  </tr>
  <tr>
   <td><p>processinstancelistView</p> </td>
   <td><p>taskdetailsView</p> </td>
   <td><p>wsmessageView</p> </td>
  </tr>
 </tbody>
</table>

### AEM Forms工作区{#log-levels-available-in-nbsp-aem-forms-workspace}中可用的日志级别

* 致命
* 错误
* 警告
* 信息
* 调试
* TRACE
* 关闭

## 浏览器{#debugging-information-for-browsers}的调试信息

脚本和样式可以在不同的浏览器中进行调试。

* **在IE中调试**:要在IE中调试AEM Forms工作区，请参阅： [https://msdn.microsoft.com/en-us/library/hh772704(v=vs.85).aspx](https://msdn.microsoft.com/en-us/library/hh772704(v=vs.85).aspx)。

* **在Chrome中调试**:要在Chrome中打开调试器，请使用快捷键：Ctrl+Shift+I。有关详细信息，请参阅： [https://developer.chrome.com/extensions/tut_debugging.html](https://developer.chrome.com/extensions/tut_debugging.html)。

* **在Firefox中调试**:在Firefox中调试脚本和样式可以使用几个加载项。例如，Firebug是这样的调试实用程序([https://getfirebug.com](https://getfirebug.com))。

## 常见问题解答{#faqs}

1. PDF表单在Google Chrome中无法呈现或提交。

   1. 安装Adobe®Reader®插件。
   1. 在Chrome中，打开chrome://plugins,视图可用的插件。
   1. 禁用Chrome PDF Viewer插件，并启用Adobe Reader插件。

1. SWF表单或指南未在Google Chrome中呈现。

   1. 在Chrome中，打开chrome://plugins,视图可用的插件。
   1. 请参阅AdobeFlash® Player插件的详细信息。
   1. 在AdobeFlash Player插件下禁用PepperFlash。

1. 我已自定义了AEM Forms工作区，但无法看到更改。

   清除浏览器缓存，然后访问AEM Forms工作区。

1. 当用户在桌面中打开表单时，需要执行哪些操作才能使表单以HTML格式呈现？

   在使用工作台时，在分配用户档案步骤中选择默认任务的HTML单选按钮。

1. 单击时，附件不显示。

   要视图附件，请在浏览器中启用弹出窗口。

1. 用户登录到表单应用程序。 如果用户尝试登录到工作区，则如果用户没有工作区权限，则可能无法加载。

   注销其他表单应用程序，然后登录到工作区。

1. 在HTML表单的设计中使用“流程属性”，在AEM Forms工作区中呈现时，在表单中显示“提交”按钮。

   在设计表单时，当您使用“流程属性”时，会在表单中添加一个“提交”按钮。 当在AEM Forms工作区中呈现为PDF时，最终用户不会看到“提交”按钮。 但是，在AEM Forms工作区中以HTML表单呈现时，最终用户可看到“提交”按钮。 单击表单中的此提交按钮不会启动任何操作。 单击表单外的AEM Forms工作区底部的“提交”按钮，完成任务。
