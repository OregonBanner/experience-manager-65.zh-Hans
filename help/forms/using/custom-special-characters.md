---
title: 通訊管理中的自訂特殊字元
seo-title: Custom special characters in Correspondence Management
description: 瞭解如何在通訊管理中新增自訂特殊字元。
seo-description: Learn how to add custom special characters in Correspondence Management.
uuid: a1890f6d-8e0c-471f-a9bd-861acf1f17e6
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: 9f26565c-a7ba-4e9e-bf77-a95eb8e351f2
docset: aem65
feature: Correspondence Management
exl-id: 3e978c3e-12f2-4dc6-801d-8ab4c5df6700
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '639'
ht-degree: 1%

---

# 通訊管理中的自訂特殊字元{#custom-special-characters-in-correspondence-management}

## 概述 {#overview}

Correspondence Management已內建210個特殊字元的預設支援，您可以輕鬆地在信函中插入。

例如，您可以插入下列特殊字元：

* 幣別符號，例如€、¥和£
* 數學符號，例如∑、√、∂和^
* 標點符號為&quot;和&quot;

您可以在字母中插入特殊字元：

* 在 [文字編輯器](/help/forms/using/document-fragments.md#createtext)
* 在 [通訊中的可編輯內嵌模組](../../forms/using/create-correspondence.md#managecontent)

![specialcharactersinlinemodule](assets/specialcharactersinlinemodule.png)

管理員可以透過自訂來新增對更多/自訂特殊字元的支援。 本文提供如何新增支援其他自訂特殊字元的指示。

## 新增或修改通訊管理中對自訂特殊字元的支援 {#creatingfolderstructure}

使用下列步驟新增對自訂特殊字元的支援：

1. 前往 `https://'[server]:[port]'/[ContextPath]/crx/de` 並以管理員身分登入。
1. 在apps資料夾中，建立名為的資料夾 **[!UICONTROL 特殊字元]** 路徑/結構類似於specialcharacters資料夾（位於libs底下的textEditorConfig資料夾）：

   1. 以滑鼠右鍵按一下 **特殊字元** 資料夾並選取 **覆蓋節點**：

      `/libs/fd/cm/ma/gui/configuration/textEditorConfig/specialcharacters`

   1. 確定「覆蓋節點」對話方塊具有下列值：

      **路徑：** /libs/fd/cm/ma/gui/configuration/textEditorConfig/specialcharacters

      **覆蓋位置：** /apps/

      **符合節點型別：** 已核取

      >[!NOTE]
      >
      >請勿在/libs分支中進行變更。 您所做的任何變更都可能遺失，因為每當您：
      >
      >
      >
      >    * 在您的執行個體上升級
      >    * 套用Hot Fix
      >    * 安裝功能套件


   1. 按一下 **確定** 然後按一下 **全部儲存**. Specialcharacters資料夾會在指定的路徑中建立。

      建立覆蓋圖後，請確認節點結構標籤。 使用覆蓋圖在/apps中建立的每個節點，都應與該節點的/libs中定義的類別和屬性相同。 如果/apps位置下方的節點結構中缺少任何屬性或標籤，請將其標籤與/libs中的對應節點同步。

1. 確保 **[!UICONTROL textEditorConfig]** 節點具有下列屬性和值：

   | 名称 | 类型 | 价值 |
   |---|---|---|
   | cmConfigurationType | 字符串 | cmTextEditorConfiguration |
   | cssPath | 字符串 | /libs/fd/cm/ma/gui/components/admin/createasset/textcontrol/clientlibs/textcontrol |

1. 以滑鼠右鍵按一下 **[!UICONTROL 特殊字元]** 資料夾並選取 **建立>子節點** 然後按一下 **全部儲存**：

   /apps/fd/cm/ma/gui/configuration/textEditorConfig/specialcharacters/&lt;yourchildnode>

1. 重新整理「文字編輯器\建立通訊UI」頁面。 您新增的節點是UI中特殊字元清單的最後一個節點。
1. 按一下 **全部儲存**.
1. 視需要對特殊字元進行變更：

<table>
 <tbody>
  <tr>
   <td><strong>收件人...</strong></td>
   <td><strong>完成下列步驟</strong></td>
  </tr>
  <tr>
   <td>新增自訂特殊字元</td>
   <td>
    <ol>
     <li>在「/apps/fd/cm/ma/gui/configuration/textEditorConfig/specialcharacters」下新增具有強制屬性的子節點。</li>
     <li>按一下全部儲存</li>
     <li>重新整理文字編輯器\建立通訊UI以檢視變更。</li>
    </ol> </td>
  </tr>
  <tr>
   <td>更新現有的特殊字元屬性</td>
   <td>
    <ol>
     <li>覆蓋要更新的節點（如上所述），並驗證標籤和類別。</li>
     <li>變更任何值，例如註解、值、endValue和多重註解。 </li>
     <li>按一下「儲存全部」。 </li>
     <li>重新整理文字編輯器\建立通訊UI以檢視變更。</li>
    </ol> </td>
  </tr>
  <tr>
   <td>隱藏特殊字元</td>
   <td>
    <ol>
     <li>覆蓋要隱藏在「/apps/fd/cm/ma/gui/configuration/textEditorConfig/specialcharacters」下的節點</li>
     <li>將sling：hideResource （布林值）屬性新增至要隱藏的節點（應用程式底下）。 </li>
     <li>按一下「儲存全部」。 </li>
     <li>重新整理文字編輯器\建立通訊UI以檢視變更。<br /> </li>
    </ol> </td>
  </tr>
  <tr>
   <td>隱藏多個特殊字元</td>
   <td>
    <ol>
     <li>將屬性「sling：hideChildren （String或String[]）」新增至「/apps/fd/cm/ma/gui/configuration/textEditorConfig/specialcharacters」。 </li>
     <li>新增節點名稱（要隱藏的特殊字元）作為「sling：hideChildren」屬性的值。 </li>
     <li>按一下「儲存全部」。 </li>
     <li>重新整理文字編輯器\建立通訊UI以檢視變更。<br /> </li>
    </ol> </td>
  </tr>
  <tr>
   <td>排序特殊字元</td>
   <td>
    <ol>
     <li>在「/apps/fd/cm/ma/gui/configuration/textEditorConfig/specialcharacters」下新增具有強制屬性的子節點。 </li>
     <li>將"sling：orderBefore (String)"屬性新增至新建立的子節點。 </li>
     <li>將節點名稱新增為值，新加入的特殊字元會顯示在值之前。 </li>
     <li>按一下「儲存全部」。 </li>
     <li>重新整理文字編輯器\建立通訊UI以檢視變更。<br /> </li>
    </ol> </td>
  </tr>
 </tbody>
</table>
