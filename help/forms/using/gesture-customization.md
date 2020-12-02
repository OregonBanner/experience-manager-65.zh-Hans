---
title: 手势自定义
seo-title: 手势自定义
description: 在您的AEM Forms应用程序上自定义手势
seo-description: 在您的AEM Forms应用程序上自定义手势
uuid: 117e0e21-66bd-42f1-879c-6c1443991974
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 747d13d3-e7cc-4aa1-bcc8-4b57157e71ed
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 0%

---


# 手势自定义{#gesture-customization}

您可以自定义AEM Forms应用程序的手势，以提供与应用程序交互的独特方法。 例如，可以添加新手势以打开或关闭任务或起点。

## 在AEM Forms应用程序{#to-customize-gestures-in-aem-forms-app}中自定义手势

在AEM Forms应用程序中，左轻扫会打开新任务或起始点，而右轻扫则无效。 以下示例提供在AEM Forms应用程序中执行右轻扫手势时打开新任务或起始点的步骤。

1. 打开您的项目。

   * 对于iOS，在Xcode中打开`Capture.xcodeproj`
   * 对于Android，在Eclipse中打开Android项目。
   * 对于Windows，在Visual Studio中打开`MWSWindows.sln`。

1. 导览至视图文件夹，然后打开`task.js`文件进行编辑。

   * 在Xcode中，导航到&#x200B;**Capture > www > wsmobile > js > runtime >视图**&#x200B;文件夹。
   * 在Eclipse中，导航到&#x200B;**资产> www > wsmobile > js > runtime >视图**&#x200B;文件夹。
   * 在Visual Studio中，导航到&#x200B;**MWSWindows > www > wsmobile > js > runtime >视图**&#x200B;文件夹。

   >[!NOTE]
   >
   >任务.js文件包含与列在任务或起点列表中的每个任务或起点关联的骨干视图。

1. 在`task.js`文件中，搜索事件的视图属性。

   事件属性是具有以下格式的每个条目的映射：

   `"EventName Selector": "Function"`

   在`Selector`指定的HTML元素上触发名为`EventName`的Javascript事件时，将调用`Function`。

1. 查找

   * &quot;点按。taskContentArea&quot; :&quot;onTaskClick&quot;,

      &quot;点按。taskOpenArea&quot;:&quot;onTaskClick&quot;,

      &quot;点按。任务内容&quot;:&quot;onTaskClick&quot;,

      &quot;点按。last_empty_div&quot;:&quot;onTaskClick&quot;,
   和

   * &quot;轻扫。taskContentArea&quot; :&quot;onTaskClick&quot;,

      &quot;轻扫。taskOpenArea&quot; :&quot;onTaskClick&quot;,

      &quot;轻扫。任务-内容&quot;:&quot;onTaskClick&quot;,

      &quot;轻扫。last_empty_div&quot;:&quot;onTaskClick&quot;,


1. 保存并关闭`task.js`文件。
1. 构建和运行AEM Forms应用程序。 现在，您可以通过左轻扫和右轻扫打开使用。

同样，您也可以对各种手势、HTML元素和函数组合在其他视图中进行更改。
