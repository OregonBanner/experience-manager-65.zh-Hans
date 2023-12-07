---
title: 自适应Forms、HTML5表单和AEM Forms的常见问题解答(FAQ)
description: 有关自适应Forms、HTML5表单和AEM Forms的布局、脚本支持和范围的常见问题解答(FAQ)。
docset: aem65
exl-id: 19a6e431-de66-4d5c-924f-f9c1a195390c
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '98'
ht-degree: 0%

---

# 常见问题解答(FAQ) {#frequently-asked-questions-faq}

1. 为什么中的条形码和签名字段未出现在我的HTML5表单中？

   答案：条形码和签名字段在HTML或移动场景中无关。 这些字段显示为非交互区域。 但是，AEM Forms Designer提供了一个新的签名涂写字段，该字段可用于代替签名字段。 您也可以添加 [自定义构件](../../forms/using/custom-widgets.md) 用于条形码，并将它集成。
