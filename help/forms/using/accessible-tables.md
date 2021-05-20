---
title: 在HTML5表单中创建可访问的复杂表
seo-title: 在HTML5表单中创建可访问的复杂表
description: 了解如何在HTML5表单中创建无障碍表。
seo-description: 了解如何在HTML5表单中创建无障碍表。
uuid: e52562d2-4dc3-4359-9dbb-c18614921808
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 3504afe1-abf5-4fbf-a0d2-e093361764bd
feature: 移动设备表单
exl-id: 3b8e3323-9ac4-4f5c-8c52-e2186e9169ea
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '291'
ht-degree: 0%

---

# 在HTML5表单中创建可访问的复杂表{#create-accessible-complex-tables-in-html-forms}

HTML5 Forms中表的默认实施使用HTML DIV元素来呈现表。 呈现涉及使用ARIA角色来满足无障碍性要求。

为避免屏幕阅读器存在的辅助功能问题，这些屏幕阅读器不完全支持数据表中使用的ARIA角色，HTML5 Forms为表提供了替代呈现版本。 这些表基于Designer中引入的新表格式，该格式还支持：

* 行标题
* 行范围

要在HTML5 Forms中使用新格式，请将表标记为复杂。 要将表标记为复杂表，请在表子表单的XML源中添加`extras`标记，如下所示：

```xml
</extras>
 <text name="complexTable">1</text>
 </extras>
```

标记为&#x200B;*complexTable*&#x200B;的表遵循本机HTML呈现版本，并为某些屏幕阅读器提供更好的辅助功能支持。  要创建行范围，请选择同一列中表的连续单元格，右键单击选定的内容，然后单击&#x200B;**[!UICONTROL 合并单元格]**。

>[!NOTE]
>
>创建行跨度仅适用于最左侧的单元格。

要将行标记为行标题，请选择行中的所有单元格，右键单击所选内容，然后单击&#x200B;**[!UICONTROL 标记标题]**。

要将单元格标记为列标题，请选择列中的任意单元格，右键单击选定的内容，然后单击&#x200B;**[!UICONTROL 标记标题]**。

新&#x200B;*AccessibleTable*&#x200B;格式的限制：

* 如果表中使用了rowspan，则不支持可扩展字段
* 不支持嵌套表（表单元格中的表）
* 对行跨度的支持仅限于标题行和标题单元格
* 支持仅限于常规表格
* 不支持在行数> 1的表中预填充数据
