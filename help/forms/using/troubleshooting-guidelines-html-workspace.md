---
title: AEM Forms工作区疑难解答指南
seo-title: Troubleshooting guidelines for AEM Forms workspace
description: 启用日志并在浏览器中使用调试器对AEM Forms工作区进行故障排除。
seo-description: Enable logs and use debugger in browser to troubleshoot AEM Forms workspace.
uuid: 07b8c8ed-f1ff-4be5-8005-251ff7b2ac85
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 5dae9ed9-77a3-44f5-a94d-ca5c355c8730
exl-id: a054b60a-5e89-4c98-87bc-35669988d160
source-git-commit: d3923e5e693e7426ee57e81e203f31964a23af3a
workflow-type: tm+mt
source-wordcount: '734'
ht-degree: 0%

---

# AEM Forms工作区疑难解答指南 {#troubleshooting-guidelines-for-aem-forms-workspace}

本文讨论如何通过启用日志记录和使用浏览器中的调试器来调试AEM Forms工作区。 它还解释了您在使用AEM Forms工作区时可能会遇到的一些常见问题及其解决方法。

## 无法安装AEM Forms工作区包 {#unable-to-install-aem-forms-workspace-package}

安装修补程序后，打开AEM Forms工作区。 如果遇到未找到资源错误，请打开CRX包管理器，然后重新安装 `adobe-lc-workspace-pkg-<version>.zip` 包。

安装包时，如果遇到错误 `javax.jcr.nodetype.ConstraintViolationException: OakConstraint0025: Authorizable property rep:authorizableId may not be removed`，请执行以下步骤：

1. 登录到CRXDE Lite。 默认URL为 `https://[localhost]:'port'/lc/crx/de/index.jsp`
1. 删除以下节点：

   `/home/groups/P/PERM_WORKSPACE_USER`

1. 转到包管理器。 默认URL为 `https://[localhost]:'port'/lc/crx/packmgr/index.jsp.`
1. 搜索并安装 `adobe-lc-workspace-pkg-[version].zip` 包。
1. 重新启动应用程序服务器。

## AEM Forms工作区日志记录 {#aem-forms-workspace-nbsp-logging}

您可以在各个级别生成日志，以实现错误的最佳故障排除。 例如，在复杂的应用程序中，在组件级别进行日志记录有助于对特定组件进行调试和故障排除。

在AEM Forms工作区中：

* 要获取有关特定组件文件的日志记录信息，请附加 `/log/<ComponentFile>/<LogLevel>` 在URL中，然后按 `Enter`. 在指定的日志级别上，组件文件的所有日志记录信息都打印在控制台上。

* 要获取所有组件文件的日志记录信息，请附加 `/log/all/trace` 在URL中，然后按 `Enter`.

* 日志格式： `<Component file> <Date>:<Time>: <Log Level> : <Log Message>`

>[!NOTE]
>
>默认情况下，所有组件的日志级别均设置为INFO。

* 用户设置的日志级别仅针对该浏览器会话进行维护。 当用户刷新页面时，所有组件的日志级别将设置为初始值。

### AEM Forms工作区中的组件文件列表 {#list-of-component-files-in-nbsp-aem-forms-workspace}

<table>
 <tbody>
  <tr>
   <td><p>allcategorymodel</p> </td>
   <td><p>processinstanceModel</p> </td>
   <td><p>任务列表模型</p> </td>
  </tr>
  <tr>
   <td><p>appnavigationModel</p> </td>
   <td><p>processInstanceView</p> </td>
   <td><p>任务列表视图</p> </td>
  </tr>
  <tr>
   <td><p>appnavigationView</p> </td>
   <td><p>processnamelistModel</p> </td>
   <td><p>任务模型</p> </td>
  </tr>
  <tr>
   <td><p>categorylistModel</p> </td>
   <td><p>processnamelistView</p> </td>
   <td><p>任务视图</p> </td>
  </tr>
  <tr>
   <td><p>categorylistView</p> </td>
   <td><p>processnameModel</p> </td>
   <td><p>teamqueuseview</p> </td>
  </tr>
  <tr>
   <td><p>categorymodel</p> </td>
   <td><p>processnameView</p> </td>
   <td><p>todoView</p> </td>
  </tr>
  <tr>
   <td><p>categoryView</p> </td>
   <td><p>searchtemplatedetailsView</p> </td>
   <td><p>trackingview</p> </td>
  </tr>
  <tr>
   <td><p>favoritecategoryModel</p> </td>
   <td><p>共享模型</p> </td>
   <td><p>uissettingsModel</p> </td>
  </tr>
  <tr>
   <td><p>筛选列表视图</p> </td>
   <td><p>共享视图</p> </td>
   <td><p>uissettingsView</p> </td>
  </tr>
  <tr>
   <td><p>筛选视图</p> </td>
   <td><p>startpointlistModel</p> </td>
   <td><p>userinfoModel</p> </td>
  </tr>
  <tr>
   <td><p>outofficeModel</p> </td>
   <td><p>startpointlistView</p> </td>
   <td><p>用户信息视图</p> </td>
  </tr>
  <tr>
   <td><p>outofficeView</p> </td>
   <td><p>起始点模型</p> </td>
   <td><p>usersearchModel</p> </td>
  </tr>
  <tr>
   <td><p>首选项视图</p> </td>
   <td><p>起始点视图</p> </td>
   <td><p>usersearchView</p> </td>
  </tr>
  <tr>
   <td><p>processinstancehistoryView</p> </td>
   <td><p>startProcessView</p> </td>
   <td><p>错误模型</p> </td>
  </tr>
  <tr>
   <td><p>processinstancelistModel</p> </td>
   <td><p>startprocessView</p> </td>
   <td><p>错误视图</p> </td>
  </tr>
  <tr>
   <td><p>processinstancelistView</p> </td>
   <td><p>任务详细信息视图</p> </td>
   <td><p>wsmessageView</p> </td>
  </tr>
 </tbody>
</table>

### AEM Forms Workspace中可用的日志级别 {#log-levels-available-in-nbsp-aem-forms-workspace}

* 致命
* 错误
* 警告
* 信息
* 调试
* TRACE
* 关闭

## 浏览器的调试信息 {#debugging-information-for-browsers}

可以在不同的浏览器中调试脚本和样式。

* **在IE中进行调试**：要在IE中调试AEM Forms工作区，请参阅： [https://learn.microsoft.com/en-us/office/dev/add-ins/testing/debug-add-ins-using-f12-tools-ie](https://learn.microsoft.com/en-us/office/dev/add-ins/testing/debug-add-ins-using-f12-tools-ie).

* **在Chrome中进行调试**：要在Chrome中打开调试器，请使用快捷键：Ctrl+Shift+I。有关更多信息，请参阅： [https://developer.chrome.com/docs/extensions/mv3/tut_debugging/](https://developer.chrome.com/docs/extensions/mv3/tut_debugging/).

* **在Firefox中进行调试**：有多个加载项可用于在Firefox中调试脚本和样式。 例如，Firebug就是这样一个调试实用程序([https://getfirebug.com](https://getfirebug.com))。

## 常见问题解答 {#faqs}

1. PDF表单未在Google Chrome中渲染或提交。

   1. 安装Adobe®Reader®插件。
   1. 在Chrome中，打开chrome://plugins以查看可用的插件。
   1. 禁用ChromePDF查看器插件，并启用Adobe Reader插件。

1. SWF表单或指南未在Google Chrome中呈现。

   1. 在Chrome中，打开chrome://plugins以查看可用的插件。
   1. 有关AdobeFlash®播放器插件的详细信息，请参阅。
   1. 禁用“AdobeFlash Player”插件下的PepperFlash。

1. 我已经自定义了AEM Forms工作区，但看不到更改内容。

   清除浏览器的缓存，然后访问AEM Forms工作区。

1. 用户在桌面中打开表单时，需要执行哪些操作才能在HTML中渲染表单？

   在使用Workbench时，为分配任务步骤中的默认配置文件选择“HTML”单选按钮。

1. 单击时未显示附件。

   要查看附件，请在浏览器中启用弹出窗口。

1. 用户登录到表单应用程序。 如果用户尝试登录到workspace，如果用户没有workspace权限，则可能无法加载。

   从其他表单应用程序注销，然后登录到工作区。

1. HTML表单，在其设计中使用“流程属性”，在AEM Forms工作区中呈现时，在表单内显示“提交”按钮。

   设计表单时，当您使用流程属性时，它会在表单中添加一个提交按钮。 在AEM Forms工作区中呈现为PDF时，“提交”按钮对最终用户不可见。 但是，在AEM Forms工作区中以HTML表单形式呈现时，最终用户可看到“提交”按钮。 单击表单中的此“提交”按钮不会启动任何操作。 单击表单外部AEM Forms工作区底部的“提交”按钮可完成任务。
