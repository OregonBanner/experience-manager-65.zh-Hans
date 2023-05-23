---
title: 在HTML5表單中建立可存取的複雜表格
seo-title: Create accessible complex tables in HTML5 forms
description: 瞭解如何在HTML5表單中建立無障礙表格。
seo-description: Learn how to create accessible tables in HTML5 forms.
uuid: e52562d2-4dc3-4359-9dbb-c18614921808
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 3504afe1-abf5-4fbf-a0d2-e093361764bd
feature: Mobile Forms
exl-id: 3b8e3323-9ac4-4f5c-8c52-e2186e9169ea
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '273'
ht-degree: 0%

---

# 在HTML5表單中建立可存取的複雜表格 {#create-accessible-complex-tables-in-html-forms}

HTML5 Forms中表格的預設實作使用HTMLDIV元素來轉譯表格。 轉譯涉及使用ARIA角色來滿足協助工具需求。

為了避免熒幕助讀程式無法完整支援資料表格所用ARIA角色的協助工具問題，HTML5 Forms提供表格的替代轉譯。 這些表格以Designer中匯入的新表格格式為基礎，也支援：

* 列標題
* 列跨度

若要在HTML5 Forms中使用新格式，請將表格標示為複雜。 若要將表格標籤為複雜，請新增 `extras` 標籤的位置，如下所示：

```xml
</extras>
 <text name="complexTable">1</text>
 </extras>
```

標示為的表格 *complextable* 遵循原生HTML轉譯，並為某些熒幕朗讀程式提供更好的協助工具支援。  若要建立列範圍，請選取相同欄中表格的連續儲存格，以滑鼠右鍵按一下選取範圍，然後按一下 **[!UICONTROL 合併儲存格]**.

>[!NOTE]
>
>建立列跨距僅適用於最左側的儲存格。

若要將列標示為列標題，請選取列中的所有儲存格，以滑鼠右鍵按一下選取範圍，然後按一下 **[!UICONTROL 標頭標籤]**.

若要將儲存格標示為欄標題，請選取欄中的任何儲存格，以滑鼠右鍵按一下選取範圍，然後按一下 **[!UICONTROL 標頭標籤]**.

新限制 *Accessibletable* 格式：

* 表格中使用rowspan時，不支援可成長的欄位
* 不支援巢狀表格（表格儲存格內的表格）
* rowspan的支援僅限於標題列和標題儲存格
* 僅支援一般表格
* rowspan > 1的表格不支援資料預填
