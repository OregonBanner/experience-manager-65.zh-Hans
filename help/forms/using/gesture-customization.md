---
title: 手势自定义
seo-title: 手势自定义
description: 自定义AEM Forms应用程序上的手势
seo-description: 自定义AEM Forms应用程序上的手势
uuid: 117e0e21-66bd-42f1-879c-6c1443991974
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 747d13d3-e7cc-4aa1-bcc8-4b57157e71ed
exl-id: 6debb1a7-7889-4fdd-87c7-ecb87cc0b1f5
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 0%

---

# 手势自定义{#gesture-customization}

您可以自定义AEM Forms应用程序的手势，以提供一种与应用程序进行交互的独特方法。 例如，您可以添加新手势以打开或关闭任务或起点。

## 在AEM Forms应用程序{#to-customize-gestures-in-aem-forms-app}中自定义手势

在AEM Forms应用程序中，左轻扫会打开一个新任务或“起始点”，而右轻扫则不执行任何操作。 以下示例提供了在AEM Forms应用程序中执行右轻扫手势时打开新任务或起点的步骤。

1. 打开您的项目。

   * 对于iOS，在Xcode中打开`Capture.xcodeproj`
   * 对于Android，在Eclipse中打开Android项目。
   * 对于Windows，在Visual Studio中打开`MWSWindows.sln`。

1. 导航到视图文件夹并打开`task.js`文件进行编辑。

   * 在Xcode中，导航到&#x200B;**Capture > www > wsmobile > js > runtime > views**&#x200B;文件夹。
   * 在Eclipse中，导航到&#x200B;**assets > www > wsmobile > js > runtime > views**&#x200B;文件夹。
   * 在Visual Studio中，导航到&#x200B;**MWSWindows > www > wsmobile > js >运行时>视图**&#x200B;文件夹。

   >[!NOTE]
   >
   >task.js文件包含与任务或起始点列表中列出的每个任务或起始点相关联的骨干视图。

1. 在`task.js`文件中，搜索视图的events属性。

   events属性是一个映射，每个条目的格式如下：

   `"EventName Selector": "Function"`

   在`Selector`指定的HTML元素上触发名为`EventName`的Javascript事件时，将调用`Function`。

1. 查找

   * &quot;点按.taskContentArea&quot; :&quot;onTaskClick&quot;,

      &quot;点按.taskOpenArea&quot; :&quot;onTaskClick&quot;,

      &quot;点按.task-content&quot; :&quot;onTaskClick&quot;,

      &quot;tap .last_empty_div&quot; :&quot;onTaskClick&quot;,
   替换为

   * &quot;swipe .taskContentArea&quot; :&quot;onTaskClick&quot;,

      &quot;swipe .taskOpenArea&quot; :&quot;onTaskClick&quot;,

      &quot;轻扫.task-content&quot; :&quot;onTaskClick&quot;,

      &quot;swipe .last_empty_div&quot; :&quot;onTaskClick&quot;,


1. 保存并关闭`task.js`文件。
1. 构建并运行AEM Forms应用程序。 现在，您可以使用左轻扫和右轻扫来打开。

同样，您也可以对手势、HTML元素和函数的各种组合在其他视图中进行更改。
