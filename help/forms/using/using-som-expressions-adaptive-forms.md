---
title: 在自适应表单中使用SOM表达式
seo-title: 在自适应表单中使用SOM表达式
description: 了解如何提取自适应表单面板的SOM表达式。
seo-description: 了解如何提取自适应表单面板的SOM表达式。
uuid: c5d55aff-fb69-4a1c-96ea-fb3f9322cbb0
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: 13f00bb2-561f-4d64-8829-292c663abeab
docset: aem65
translation-type: tm+mt
source-git-commit: 6b4bc58efd72900c54cb245878239e345d72ae3e
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# 在自适应表单中使用SOM表达式{#using-som-expressions-in-adaptive-forms}

自适应表单建模为AEM页面，在AEM存储库中以JCR内容结构表示。 内容结构的关键元素是guideContainer节点。 在guideContainer下面有rootPanel，它可能包含嵌套面板和字段。

您可以使用脚本对象模型(SOM)来引用特定文档对象模型(DOM)中的值、属性和方法。 DOM将内存对象和属性组织在树层次结构中。 SOM表达式引用字段／绘图元素和面板。

下图描绘了自适应表单在向表单添加组件时转换为的节点结构。 例如，您可以在根面板中添加一个面板，并在该面板中添加一个在运行时转换为DOM的单选按钮。 自适应形式单选按钮字段的SOM表达式指定为 `guide[0].guide1[0].guideRootPanel[0].panel1[0].radiobutton[0]`。

![DOM树](assets/hierarchy.png)

DOM树

自适应表单中任何元素的SOM表达式由前缀 `guide[0].guide1[0]`。 组件在节点结构层次中的位置用于导出其SOM表达式。

![具有两个单选按钮的DOM树](assets/hierarchy_radio_button.png)

具有两个单选按钮的DOM树

在自适应表单中更改单选按钮的位置时，SOM表达式会发生变化。 在创作模式中，您可以使用视图SOM表达式选项视图AEM Forms中字段或元素的SOM表达式。 该选项显示在面板上，并在右键单击该字段或元素时显示。

![以自适应形式提取SOM表达式](assets/som-expressions.png)

以自适应形式提取SOM表达式

在面板中，您可以从面板工具栏访问该功能。 此功能便于自适应表单作者编写脚本。

![使用面板工具栏提取SOM表达式](assets/som-expression.png)

使用面板工具栏提取SOM表达式

GuideBridge中列出的 [某些API](https://helpx.adobe.com/aem-forms/6/javascript-api/GuideBridge.html) 使用元素的SOM表达式。 例如，要以自适应形式将焦点置于特定字段，请将相应的SOM表达式传递 `getFocus`到API `guideBridge`。

