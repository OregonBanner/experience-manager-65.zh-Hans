---
title: 手势自定义
seo-title: 手势自定义
description: 在AEM Forms应用程序上自定义手势
seo-description: 在AEM Forms应用程序上自定义手势
uuid: 117e0e21-66bd-42f1-879c-6c1443991974
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 747d13d3-e7cc-4aa1-bcc8-4b57157e71ed
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 手势自定义 {#gesture-customization}

您可以自定义AEM Forms应用程序的手势，以提供与应用程序交互的独特方法。 例如，可以添加新手势以打开或关闭任务或起点。

## 在AEM Forms应用程序中自定义手势 {#to-customize-gestures-in-aem-forms-app}

在AEM Forms应用程序中，左轻扫会打开新任务或起始点，而右轻扫则不执行任何操作。 以下示例提供了在AEM Forms应用程序中执行右击手势时打开新任务或起点的步骤。

1. 打开您的项目。

   * 对于iOS，在Xcode `Capture.xcodeproj` 中打开
   * 对于Android，在Eclipse中打开Android项目。
   * 对于Windows，请在Visual `MWSWindows.sln` Studio中打开。

1. 导览至视图文件夹，然后打开文 `task.js` 件进行编辑。

   * 在Xcode中，导航到“捕 **捉”>“www”>“wsmobile”>“js”>“运行时”>“视图** ”文件夹。
   * 在Eclipse中，导航到资产> www > wsmobile > js > runtime > views文 **件夹** 。
   * 在Visual studio中，导航到 **MWSWindows > www > wsmobile > js > runtime > views** 文件夹。
   >[!NOTE]
   >
   >task.js文件包含与任务列表或起始点列表中列出的每个任务或起始点相关联的骨干视图。

1. 在文 `task.js` 件中，搜索视图的events属性。

   events属性是一个映射，每个条目的格式如下：

   `"EventName Selector": "Function"`

   当您触发在指定的HTML元 `EventName`素上命名的Javascript事件时， `Selector`将 `Function`调用该事件。

1. 查找

   * &quot;点按。taskContentArea&quot; :“onTaskClick”,

      &quot;点按。taskOpenArea&quot; :“onTaskClick”,

      “点按。task-content”:“onTaskClick”,

      &quot;tap .last_empty_div&quot; :“onTaskClick”,
   和

   * &quot;轻扫。taskContentArea&quot;:“onTaskClick”,

      &quot;轻扫。taskOpenArea&quot;:“onTaskClick”,

      “轻扫。task-content”:“onTaskClick”,

      &quot;swipe .last_empty_div&quot;:“onTaskClick”,


1. 保存并关闭 `task.js` 文件。
1. 构建并运行AEM Forms应用程序。 现在，您可以通过左轻扫和右轻扫打开使用。

同样，您也可以对手势、HTML元素和函数的各种组合在其他视图中进行更改。

**[联系支持](https://www.adobe.com/account/sign-in.supportportal.html)**
