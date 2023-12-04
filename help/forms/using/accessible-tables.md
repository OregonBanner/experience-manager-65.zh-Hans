---
title: 在HTML5表单中创建可访问的复杂表
seo-title: Create accessible complex tables in HTML5 forms
description: 了解如何在HTML5表单中创建无障碍的表。
seo-description: Learn how to create accessible tables in HTML5 forms.
uuid: e52562d2-4dc3-4359-9dbb-c18614921808
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 3504afe1-abf5-4fbf-a0d2-e093361764bd
feature: Mobile Forms
exl-id: 3b8e3323-9ac4-4f5c-8c52-e2186e9169ea
source-git-commit: 10b370fd8f855f71c6d7d791c272137bb5e04d97
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 0%

---

# 在HTML5表单中创建可访问的复杂表 {#create-accessible-complex-tables-in-html-forms}

HTML5 Forms中表的默认实现使用HTMLDIV元素来呈现表。 渲染包括使用ARIA角色来满足辅助功能要求。

为避免屏幕阅读器出现辅助功能问题（该屏幕阅读器不完全支持与数据表一起使用的ARIA角色），HTML5 Forms为表提供了替代演绎版。 这些表基于Designer中引入的新表格式，该格式还支持：

* 行标题
* 行跨度

要在HTML5 Forms中使用新格式，请将表标记为复杂表。 要将表标记为复杂，请添加 `extras` 表子表单的XML源中的标记，如下所示：

```xml
</extras>
 <text name="complexTable">1</text>
 </extras>
```

标记为的表 *complextable* 遵循本机HTML演绎版，并为某些屏幕阅读器提供更好的无障碍支持。  要创建行范围，请选择同一列中表的连续单元格，右键单击所选内容，然后单击 **[!UICONTROL 合并单元格]**.

>[!NOTE]
>
>创建行范围仅适用于最左侧的单元格。

要将行标记为行标题，请选择行中的所有单元格，右键单击选定内容，然后单击 **[!UICONTROL 标记标题]**.

要将单元格标记为列标题，请选择列中的任意单元格，右键单击选定内容，然后单击 **[!UICONTROL 标记标题]**.

新增限制 *Accessibletable* 格式：

* 如果在表中使用rowspan，则不支持可增长的字段
* 不支持嵌套表（表单元格中的表）
* 仅对标题行和标题单元格支持rowspan
* 仅支持常规表
* 不支持在rowspan > 1的表中进行数据预填充
