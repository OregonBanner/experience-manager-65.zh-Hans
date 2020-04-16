---
title: 在HTML5表单中创建可访问的复杂表
seo-title: 在HTML5表单中创建可访问的复杂表
description: 了解如何在HTML5表单中创建可访问的表。
seo-description: 了解如何在HTML5表单中创建可访问的表。
uuid: e52562d2-4dc3-4359-9dbb-c18614921808
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 3504afe1-abf5-4fbf-a0d2-e093361764bd
translation-type: tm+mt
source-git-commit: f9389a06f9c2cd720919486765cee76257f272c3

---


# 在HTML5表单中创建可访问的复杂表 {#create-accessible-complex-tables-in-html-forms}

HTML5 Forms中表的默认实现使用HTML DIV元素来呈现表。 渲染涉及使用ARIA角色来满足辅助功能要求。

为避免屏幕阅读器的辅助功能问题，这些屏幕阅读器不完全支持数据表使用的ARIA角色，HTML5 Forms为表格提供了替代再现。 这些表基于Designer中引入的新表格格式，该格式还支持：

* 行标题
* 行跨

要使用HTML5 Forms中的新格式，请将表标记为复杂。 要将表标记为复杂表，请按 `extras` 如下方式在表子表单的XML源中添加标签：

```
</extras>
 <text name="complexTable">1</text>
 </extras>
```

标记为complexTable的表遵循 *原生HTML再现* ，并为某些屏幕阅读器提供更好的辅助功能支持。  要创建行范围，请在同一列中选择表的连续单元格，右键单击所选内容，然后单击“合并单 **[!UICONTROL 元格”]**。

>[!NOTE]
>
>创建行跨仅适用于最左侧的单元格。

要将行标为行标题，请选择行中的所有单元格，右键单击选定内容，然后单击标 **[!UICONTROL 记标题]**。

要将单元格标记为列标题，请选择列中的任意单元格，右键单击选定内容，然后单击“标 **[!UICONTROL 记标题”]**。

新AccessibleTable格式 *的限制* :

* 如果表中使用了rowspan，则不支持可扩展字段
* 不支持嵌套表（表单元格中的表）
* 对rowspan的支持仅限于标题行和标题单元格
* 支持仅限于常规表
* 不支持在行跨度> 1的表中预填充数据

