---
title: 建立具有可重複區段的表單
seo-title: Creating forms with repeatable sections
description: 可重複區段是可動態新增或移除至表單的面板。
seo-description: Repeatable sections are panels that can be dynamically added or removed to a form.
uuid: c3fa2aa4-a6b4-458e-8534-138e075290b1
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 01724ca0-6901-45e7-b045-f44814ed574e
feature: Adaptive Forms
exl-id: f2abae0a-f7fd-4a39-bd8c-03492ce06fe9
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1119'
ht-degree: 0%

---

# 建立具有可重複區段的表單 {#creating-forms-with-repeatable-sections}

可重複區段是可動態新增或移除至表單的面板。

例如，在申請工作時，求職者會提供之前的就業詳細資料，例如公司名稱、角色、專案和其他資訊。 所有僱主的資訊都需要外觀不同但相似的區段。 在這種情況下，僱用表單會提供僱主區段，並提供動態新增更多此類區段的選項。 這些動態新增的區段稱為可重複區段。

您可以使用下列其中一種方法來建立可重複的面板：

## 透過指令碼使用執行個體管理員  {#using-instance-manager-via-scripts-nbsp}

1. 在編輯模式中，選取面板，然後點選 ![cmppr](assets/cmppr.png). 在側邊欄中的「屬性」下方，啟用 **讓面板可重複**. 指定「 」的值 **[!UICONTROL 最大值]** 和 **[!UICONTROL 最小值]** 欄位。

   「最大值」欄位會指定面板在頁面上出現的最大次數。 您可以在「最大計數」欄位中指定–1，讓面板無限次出現。

   「最小值」欄位會指定面板在表單上顯示的最小次數。 如果您將Minimum Count欄位設為零，稍後您可在轉譯完成後透過指令碼移除所有例項。

   >[!NOTE]
   >
   >若要建立不可重複的面板，請將「最大值」和「最小值」欄位的值設定為1。 摺疊式功能表版面在「最大計數」欄位中不支援–1。 您可以指定高數字來提供無限值的概念。

1. 面板的父項（要重複）應包含新增和刪除按鈕，以管理可重複面板的例項。 執行以下步驟，將按鈕插入父項並在按鈕上啟用指令碼：

   1. 從側邊欄中，將按鈕元件拖放至面板的父系。 選取元件並點選 ![edit-rules](assets/edit-rules.png). 按鈕的規則會在規則編輯器中開啟。
   1. 在「規則編輯器」視窗中，按一下 **建立**.

      選取 **視覺化編輯器** 「表單物件與函式」列中的。

      1. 在規則區域的WHEN下，選取state **已點按**.
      1. 在THEN底下：

         * 若要建立新增面板按鈕，請選取 **新增例項**，並使用拖放面板 ![切換側面板](assets/toggle-side-panel.png) 或使用以下方式選取它： **拖放物件或在這裡選取。**
         * 若要建立刪除面板按鈕，請選取 **移除例項**，並使用拖放面板 ![切換側面板](assets/toggle-side-panel.png) 或使用以下方式選取它： **拖放物件或在這裡選取。**

      選取 **代碼編輯器** 「表單物件與函式」列中的。 按一下 **編輯規則** 在程式碼區域中：

      * 若要建立新增面板按鈕，請指定 `this.panel.instanceManager.addInstance()`
      * 若要建立刪除面板按鈕，請指定 `this.panel.instanceManager.removeInstance(this.panel.instanceIndex)`

      按一下 **完成**.

      >[!NOTE]
      >
      >如果欄位屬於可重複面板，則無法在指令碼中直接使用其名稱來存取它。 若要存取欄位，請使用 `instances` 中的API `InstanceManager`. 使用的語法 `instances` 中的API `InstanceManager` 為：
      >
      >
      >`<panelName>.instanceManager.instances[<instanceNumber>].<fieldname>`
      >
      >
      >例如，您可以建立最適化表單，其可重複面板具有文字方塊。 當您使用三個可重複的文字方塊預先填入表單時，您需要下列xml：
      >
      >
      >`<panel1><textbox1>AA1</panel1></textbox1>`
      >
      >
      >`<panel1><textbox1>AA2</panel1></textbox1>`
      >
      >
      >`<panel1><textbox1>AA3</panel1></textbox1>`
      >
      >
      >若要讀取AA1資料，請指定：
      >
      >
      >`Panel1.instanceManager.instances[0].textbox.value`
      >
      >
      >若要讀取AA2資料，請指定：
      >
      >
      >`Panel1.instanceManager.instances[1].textbox.value`
      >
      >
      >如需詳細資訊，請參閱：Class： InstanceManager#instances in [AEM Forms Java API參考](https://adobe.com/go/learn_aemforms_documentation_63).

      >[!NOTE]
      >
      >從最適化表單中移除面板的所有執行個體時，若要新增已移除面板的執行個體，請使用_panelName語法來擷取面板的執行個體管理員，並使用執行個體管理員的addInstance API來新增已刪除的執行個體。 例如，_panelName.addInstance()。 它會新增已移除面板的例項。



## 使用上層面板的收合式選單版面   {#using-the-accordion-layout-for-the-parent-panel-nbsp}

面板有各種版面配置選項。 摺疊式設計的「版面配置」選項對可重複面板提供開箱即用的支援。 執行以下步驟，使用Layout for accordian設計選項重複面板：

1. 在要重複的面板父項上，點選 ![cmppr](assets/cmppr.png). 您可以在側邊欄中看到屬性。 在 **版面** 下拉式清單，選取 **收合式選單**.
1. 在要重複的面板上，點選 ![cmppr](assets/cmppr.png). 您可以在側邊欄中看到面板屬性。 啟用 **讓面板可重複** 標籤，並指定 **最大值** 和 **最小值** 欄位。

   現在，您可以使用加號(+)和刪除( ![delete-panel](assets/delete-panel.png))按鈕以新增和移除面板。

## 使用表單範本中的重複子表單(XDP/XSD) {#using-repeating-subforms-from-form-template-xdp-xsd}

可重複子表單類似於最適化Forms中的可重複面板。 在AEM Forms Designer中，執行下列步驟以建立重複的子表單：

1. 在「階層」浮動視窗中，選取要重複的子表單的父子表單。
1. 在「物件」浮動視窗中，按一下「子表單」標籤，然後在「內容」清單中，選取「流程」。
1. 選取要重複的子表單。
1. 在「物件」浮動視窗中，按一下「子表單」標籤，然後在「內容」清單中選取「位置」或「流量」。
1. 按一下「繫結」標籤，並為每個資料專案選取「重複子表單」。
1. 若要指定最小重複次數，請選取「最小計數」，並在相關方塊中輸入數字。 如果此選項設為0，且資料合併時未提供子表單中物件的資料，則轉譯表單時不會放置子表單。
1. 若要指定子表單重複次數上限，請選取「最大值」，並在相關方塊中輸入數字。 如果您未在「最大值」方塊中指定值，則子表單重複次數為無限制。
1. 若要指定一組子表單重複次數，而不考慮資料數量，請選取「初始計數」，並在相關方塊中輸入數字。 如果選取此選項，但無可用資料或資料專案少於指定的「初始計數」值，則表格上仍會放置子表格的空白例項。
1. 在父子表單中新增兩個按鈕 — 一個用於新增例項，另一個用於刪除可重複子表單的例項。 如需詳細步驟，請參閱 [建置動作](https://help.adobe.com/en_US/AEMForms/6.1/DesignerHelp/WS107c29ade9134a2c74572b5612a87ca2b56-8000.2.html#WS107c29ade9134a2c-1f74d86012a87d4fe55-8000.2).
1. 現在，將表單範本連結至最適化表單。 如需詳細步驟，請參閱 [根據範本建立最適化表單](/help/forms/using/creating-adaptive-form.md#create-an-adaptive-form-based-on-a-template).
1. 使用步驟9中建立的按鈕來新增和移除子表單。

附加的.zip檔案包含一個範例可重複的子表單。

[获取文件](assets/samplerepeatablesubform.zip)

## 使用XML結構描述(XSD)的重複設定 {#using-repeat-settings-of-an-xml-schema-xsd-br}

您可以從XML結構描述以及任何複雜型別元素的minOccours &amp; maxOccurs屬性建立可重複的面板。 如需「XML綱要」的詳細資訊，請參閱 [使用XML結構描述作為表單模型建立調適型表單](/help/forms/using/adaptive-form-xml-schema-form-model.md).

在以下程式碼中， `SampleType`面板使用minOccours &amp; maxOccurs屬性。

```xml
<?xml version="1.0" encoding="utf-8" ?>
    <xs:schema targetNamespace="https://adobe.com/sample.xsd"
                    xmlns="https://adobe.com/sample.xsd"
                    xmlns:xs="https://www.w3.org/2001/XMLSchema"
                >

        <xs:element name="sample" type="SampleType"/>

        <xs:complexType name="SampleType">
            <xs:sequence>
                <xs:element name="leaderName" type="xs:string" default="Enter Name"/>
                <xs:element name="assignmentStartDate" type="xs:date"/>
                <xs:element name="gender" type="GenderEnum"/>
                <xs:element name="noOfProjectsAssigned" type="IntType"/>
                <xs:element name="assignmentDetails" type="AssignmentDetails"
                                            minOccurs="0" maxOccurs="10"/>
            </xs:sequence>
        </xs:complexType>

        <xs:complexType name="AssignmentDetails">
            <xs:attribute name="name" type="xs:string" use="required"/>
            <xs:attribute name="durationOfAssignment" type="xs:unsignedInt" use="required"/>
            <xs:attribute name="numberOfMentees" type="xs:unsignedInt" use="required"/>
             <xs:attribute name="descriptionOfAssignment" type="xs:string" use="required"/>
             <xs:attribute name="financeRelatedProject" type="xs:boolean"/>
       </xs:complexType>
  <xs:simpleType name="IntType">
            <xs:restriction base="xs:int">
            </xs:restriction>
        </xs:simpleType>
  <xs:simpleType name="GenderEnum">
            <xs:restriction base="xs:string">
                <xs:enumeration value="Female"/>
                <xs:enumeration value="Male"/>
            </xs:restriction>
        </xs:simpleType>
    </xs:schema>
```

>[!NOTE]
>
>對於非摺疊式版面，請使用最適化表單按鈕元件來新增和移除執行個體。
