---
title: 数据字典
seo-title: Data Dictionary
description: 通訊管理中的資料字典可讓您將後端資料整合到信件中，作為用於客戶通訊的輸入。
seo-description: Data dictionary in Correspondence Management lets you integrate back-end data to letters as inputs for use in customer correspondence.
uuid: 178a285e-b4a4-4a36-a2aa-b43ecb0871ed
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: a1a0ad6b-023a-4822-9cce-0618657c3f9d
docset: aem65
feature: Correspondence Management
exl-id: aaed75e6-8849-46a8-b986-896ad729adda
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '3838'
ht-degree: 1%

---

# 数据字典{#data-dictionary}

## 简介 {#introduction}

資料字典可讓商務使用者使用來自後端資料來源的資訊，而不需瞭解其基礎資料模型的技術細節。 資料字典是由資料字典元素(DDE)所組成。 您可以使用這些資料元素將後端資料整合到信件，作為輸入以用於客戶通訊。

資料字典是描述基礎資料結構及其相關屬性的中繼資料獨立表示法。 資料字典是使用商業辭彙建立的。 可對應至一或多個基礎資料模型。

資料字典由三種型別的元素組成：簡單、複合和集合元素。 簡單DDE是基本元素，例如字串、數字、日期和布林值，其中包含城市名稱等資訊。 複合DDE包含其他DDE，其型別可以是基本型別、複合型別或集合。 例如，由街道地址、城市、省、國家/地區和郵遞區號組成的地址。 集合是類似的簡單或複合DDE清單。 例如，客戶擁有多個地點或不同的帳單和送貨地址。

通訊管理使用後端、客戶或根據資料字典結構儲存的收件者特定資料，建立針對不同客戶的通訊。 例如，可以使用易記名稱建立檔案，例如「親愛的{First Name}」、「先生」。 {姓氏}&quot;.

一般來說，商務使用者不需要中繼資料表示法方面的知識，例如XSD （XML結構描述）和Java類別。 但是，它們通常需要存取這些資料結構和屬性才能建置解決方案。

### 資料字典工作流程 {#data-dictionary-workflow}

1. 作者 [建立資料字典](#createdatadictionary) 上傳結構描述或從頭開始。
1. 作者會根據資料字典建立信函和互動式通訊，並視需要聯結信函和互動式通訊中的資料字典元素。
1. 作者可以下載以資料字典的結構描述為基礎的範例資料XML檔案。 作者可以修改範例資料XML檔案，該檔案可以與資料字典關聯為測試資料。 字母預覽期間會使用相同的值。
1. 當 [預覽信件](../../forms/using/create-letter.md#p-types-of-linkage-available-for-each-of-the-fields-p)，作者選擇預覽含有資料的信件（自訂預覽）。 信件會開啟，其中預先填入了Author提供的資料。 這會在建立通訊介面中開啟。 預覽此信函的代理程式可以修改此信函的內容、資料及附件，也可以提交最終信函。 如需建立信件的詳細資訊，請參閱 [建立對應](../../forms/using/create-letter.md).

## 先决条件 {#prerequisite}

安裝 [相容性套件](compatibility-package.md) 若要檢視 **資料字典** 上的選項 **Forms** 頁面。

## 建立資料字典 {#createdatadictionary}

您可以使用資料字典編輯器來建立資料字典，也可以上傳XSD結構描述檔案來據此建立資料字典。 然後，您可以新增更多必要資訊（包括欄位）來擴充資料字典。 無論資料字典的建立方式為何，業務流程擁有者不需要後端系統的知識。 業務流程擁有者只需要瞭解領域物件及其定義，就能完成流程。

>[!NOTE]
>
>對於需要類似元素的多個字母，您可以建立通用資料字典。 但是，具有大量元素的大型資料字典在使用資料字典和載入元素（例如字母和檔案片段）時可能會導致效能問題。 如果您遇到效能問題，請嘗試為不同的字母建立個別的資料字典。

1. 選取 **Forms** > **資料字典**.
1. 點選 **建立資料字典**.
1. 在「屬性」畫面中，新增下列內容：

   * **標題：** （選用）輸入資料字典的標題。 標題不是唯一的，而且可以包含特殊字元和非英文字元。 字母和其他檔案片段會以其標題（可用時）參照，例如在縮圖和資產屬性中。 參考資料字典的名稱而非標題。
   * **名稱：** 資料字典的唯一名稱。 在「名稱」欄位中，您只能輸入英文字元、數字和連字型大小。 「名稱」欄位會根據「標題」欄位自動填入，且在「標題」欄位中輸入的特殊字元、空格、數字和非英文字元會取代為連字型大小。 雖然「標題」欄位中的值會自動複製到「名稱」，但您可以編輯該值。

   * **說明**：（選用）資料字典的說明。
   * **標籤：** （可選）若要建立自訂標籤，請在文字欄位中輸入值，然後按Enter鍵。 您可以在標籤的文字欄位下方看到您的標籤。 儲存此文字時，也會建立新新增的標籤。
   * **延伸屬性**：（選用）點選 **新增欄位** 以指定資料字典的中繼資料屬性。 在「屬性名稱」欄中，輸入唯一的屬性名稱。 在「值」欄中輸入要與屬性關聯的值。

   ![德文指定的資料字典屬性](do-not-localize/1_ddproperties.png)

1. （可選）若要上傳資料字典的XSD結構描述定義，請在「資料字典結構」窗格下點選 **上傳XML結構描述**. 瀏覽至XSD檔案、選取該檔案，然後點選 **開啟**. 系統會根據上傳的XML結構描述建立資料字典。 您需要調整資料字典中元素的顯示名稱和說明。 要執行此操作，請點選元素名稱並編輯其說明、顯示名稱及右窗格欄位中的其他詳細資訊。

   如需已計算DD元素的詳細資訊，請參閱 [計算的資料字典元素](#computedddelements).

   >[!NOTE]
   >
   >您可以略過上傳結構描述檔案，並使用使用者介面從頭開始建立資料字典。 要執行此操作，請略過此步驟並繼續後續步驟。

1. 點選 **下一個**.
1. 在新增屬性畫面中，將元素新增至資料字典。 如果您已上傳結構描述以取得資料字典的基本結構，您也可以新增/刪除元素並編輯其詳細資訊。

   您可以點選元素右側的三個點，然後將元素新增至資料字典結構。

   ![1_2_createanelement](assets/1_2_createanelement.png)

   選取「複合元素」、「集合元素」或「基本元素」。

   * 複合DDE包含其他DDE，其型別可以是基本型別、複合型別或集合。 例如，由街道地址、城市、省、國家/地區和郵遞區號組成的地址。
   * 基本的DDE是字串、數字、日期和布林值等元素，可包含城市名稱等資訊。
   * 集合是類似的簡單或複合DDE清單。 例如，客戶擁有多個地點或不同的帳單和送貨地址。

   以下是建立資料字典的一些規則：

   * 資料字典中僅允許複合型別作為頂層DDE。
   * 名稱、參考名稱和元素型別是資料字典和DDE的必要欄位。
   * 參照名稱必須是唯一的。
   * 父系DDE （複合）不能有兩個同名的子系。
   * 列舉僅包含基本字串型別。

   如需有關「複合」、「集合」和「基本」元素以及使用資料字典元素的詳細資訊，請參閱 [將資料字典元素對應至XML綱要](#mappingddetoschema).

   如需資料字典中驗證的詳細資訊，請參閱 [資料字典編輯器驗證](#ddvalidations).

   ![2_adddpropertiesbasic](assets/2_addddpropertiesbasic.png)

1. （選擇性）選取元素後，您可以在進階索引標籤中新增屬性（屬性）。 您也可以點選 **新增欄位** 和擴充DD元素的屬性。

   ![3_addddpropertiesadvanced](assets/3_addddpropertiesadvanced.png)

1. （可選）您可以點選元素右側的三個點並選取「 」，以移除任何元素 **刪除**.

   ![4_deleteelement](assets/4_deleteelement.png)

   >[!NOTE]
   >
   >刪除具有子節點的複合/收集要素也會刪除其子節點。

1. （可選）在「資料字典結構」窗格中選取「欄位」和「變數清單」面板中的元素。 變更或新增與元素相關聯的任何必要屬性。
1. 點選 **儲存**.

### 建立一或多個資料字典的復本 {#create-copies-of-one-or-more-data-dictionary}

若要快速建立一個或多個具有與現有資料字典類似之屬性和元素的資料字典，您可以複製並貼上它們。

1. 從資料字典清單中，選取適當的資料字典。 UI會顯示「複製」圖示。
1. 点按复制。UI會顯示「貼上」圖示。
1. 點選「貼上」。 「貼上」對話方塊隨即顯示。 系統會自動為新資料字典指定名稱和標題。
1. 如有需要，請編輯您要用來儲存資料字典副本的標題和名稱。
1. 點選「貼上」。 會建立資料字典的復本。 現在，您可以在新建的資料字典中進行所需的變更。

## 檢視參考資料字典元素的檔案片段或檔案 {#see-the-document-fragments-or-documents-that-refer-to-a-data-dictionary-element}

編輯或檢視資料字典時，您可以檢視資料字典中的哪些元素在文字、條件、字母和互動式通訊中參照。

1. 執行下列任一項作業來編輯資料字典：

   * 將滑鼠指標暫留在資料字典上，然後點選「編輯」。
   * 選取資料字典，然後點選標頭中的「編輯」。
   * 將滑鼠指標暫留在資料字典上，然後點選「選取」。 然後點選標頭中的「編輯」。

   或點選資料字典以檢視。

1. 在資料字典中，點選簡單元素加以選取。 複合和集合元素沒有參照。

   除了元素的「基本」和「進階」屬性外，「借出內容」也會出現。

1. 點選「借出內容」。

   「借出內容」標籤會顯示下列專案：文字、條件、字母及互動式通訊。 每個標題也會顯示所選元素的參照數量。

1. 點選標題可檢視參照元素的資產名稱。

   ![lentcontent](assets/lentcontent.png)

1. 若要檢視其他元素的借出內容，請點選元素。
1. 若要顯示參考元素的資產，請點選其名稱。 瀏覽器會顯示資產、信函或互動式通訊。

## 使用測試資料 {#working-with-test-data}

1. 在資料字典頁面上，點選 **選取**.
1. 點選您要下載測試資料的資料字典，然後點選 **下載範例XML資料**.
1. 點選 **確定** 在警示訊息中。 下載XML檔案。
1. 使用Notepad或其他XML編輯器開啟XML檔案。 XML檔案的結構與元素中的資料字典和預留位置字串相同。 將預留位置字串取代為您要用來測試字母的資料。

   ```xml
   <?xml version="1.0" encoding="UTF-8" standalone="no"?>
   <Company>
   <Name>string</Name>
   <Type>string</Type>
   <HeadOfficeAddress>
   <Street>string</Street>
   <City>string</City>
   <State>string</State>
   <Zip>string</Zip>
   </HeadOfficeAddress>
   <SalesOfficeAddress>
   <Street>string</Street>
   <City>string</City>
   <State>string</State>
   <Zip>string</Zip>
   </SalesOfficeAddress>
   <HeadCount>1.0</HeadCount>
   <CEO>
   <PersonName>
   <FirstName>string</FirstName>
   <MiddleName>string</MiddleName>
   <LastName>string</LastName>
   </PersonName>
   <DOB>string</DOB>
   <CurrAddress>
   <Street>string</Street>
   <City>string</City>
   <State>string</State>
   <Zip>string</Zip>
   </CurrAddress>
   <DOJ>14-04-1973</DOJ>
   <Phone>1.0</Phone>
   </CEO>
   </Company>
   ```

   >[!NOTE]
   >
   >在此範例中，XML會為收集要素的三個值建立空間，但可以根據需求增加/減少值的數量。

1. 建立資料專案後，您可以在預覽含有測試資料的信函時使用此XML檔案。

   您可以使用DD新增此測試資料（選取DD並點選「上傳測試資料」並上傳此xml檔案）。因此，當您正常預覽信函時（非自訂），此XML資料就會用於信函中。 您也可以點選「自訂」，然後上傳此XML。

## 範例 {#samples}

下列程式碼範例顯示資料字典的實作詳細資料。

### 可上傳至資料字典的範例結構描述 {#sample-schema-that-can-be-uploaded-to-the-data-dictionary}

```xml
<?xml version="1.0" encoding="utf-8"?>
<xs:schema xmlns="DCT" targetNamespace="DCT" xmlns:xs="https://www.w3.org/2001/XMLSchema"
  elementFormDefault="qualified" attributeFormDefault="unqualified">
  <xs:element name="Company">
    <xs:complexType>
      <xs:sequence>
        <xs:element name="Name" type="xs:string"/>
        <xs:element name="Type" type="xs:anySimpleType"/>
        <xs:element name="HeadOfficeAddress" type="Address"/>
        <xs:element name="SalesOfficeAddress" type="Address" minOccurs="0"/>
        <xs:element name="HeadCount" type="xs:integer"/>
        <xs:element name="CEO" type="Employee"/>
        <xs:element name="Workers" type="Employee" maxOccurs="unbounded"/>
      </xs:sequence>
    </xs:complexType>
  </xs:element>
  <xs:complexType name="Employee">
    <xs:complexContent>
      <xs:extension  base="Person">
        <xs:sequence>
          <xs:element name="CurrAddress" type="Address"/>
          <xs:element name="DOJ" type="xs:date"/>
          <xs:element name="Phone" type="xs:integer"/>
        </xs:sequence>
      </xs:extension>
    </xs:complexContent>
  </xs:complexType>
  <xs:complexType name="Person">
    <xs:sequence>
      <xs:element name="PersonName" type="Name"/>
      <xs:element name="DOB" type="xs:dateTime"/>
    </xs:sequence>
  </xs:complexType>
  <xs:complexType name="Name">
    <xs:sequence>
      <xs:element name="FirstName" type="xs:string"/>
      <xs:element name="MiddleName" type="xs:string"/>
      <xs:element name="LastName" type="xs:string"/>
    </xs:sequence>
  </xs:complexType>
  <xs:complexType name="Address">
    <xs:sequence>
      <xs:element name="Street" type="xs:string"/>
      <xs:element name="City" type="xs:string"/>
      <xs:element name="State" type="xs:string"/>
      <xs:element name="Zip" type="xs:string"/>
    </xs:sequence>
  </xs:complexType>
</xs:schema>
```

## 與DDE相關聯的通用屬性 {#common-attributes-associated-with-a-dde}

下表詳細說明與DDE相關的一般屬性：

<table>
 <tbody>
  <tr>
   <td><strong>属性</strong></td>
   <td><strong>类型</strong></td>
   <td><strong>描述</strong></td>
  </tr>
  <tr>
   <td>名称</td>
   <td>字符串</td>
   <td>必填.<br /> DDE的名稱。 此名稱必須是唯一的。</td>
  </tr>
  <tr>
   <td>參考資料<br /> 名稱</td>
   <td>字符串</td>
   <td>必填. DDE的唯一參考名稱，允許對DDE的參考，這些參考與資料字典的階層或結構變更無關。 文字模組已使用此名稱對應</td>
  </tr>
  <tr>
   <td>displayname</td>
   <td>字符串</td>
   <td>選用的使用者易記的DDE名稱。</td>
  </tr>
  <tr>
   <td>说明</td>
   <td>字符串</td>
   <td>DDE的說明。</td>
  </tr>
  <tr>
   <td>elementType</td>
   <td>字符串</td>
   <td>必填. DDE的型別：字串、數字、日期、布林值、複合、集合。</td>
  </tr>
  <tr>
   <td>元素子型別</td>
   <td>字符串</td>
   <td>DDE的子型別：ENUM。 僅適用於STRING和NUMBER elementType。</td>
  </tr>
  <tr>
   <td>键</td>
   <td>布尔值</td>
   <td>表示DDE是否為關鍵元素的布林值欄位。</td>
  </tr>
  <tr>
   <td>已计算</td>
   <td>布尔值</td>
   <td>表示是否已計算DDE的布林值欄位。 計算的DDE值是其他DDE值的函式。 依預設，支援jsp運算式。</td>
  </tr>
  <tr>
   <td>表达式</td>
   <td>字符串</td>
   <td>「已計算」DDE的運算式。 預設提供的運算式評估服務支援JSP EL運算式。 您可以使用自訂實作來取代運算式服務。</td>
  </tr>
  <tr>
   <td>valueSet</td>
   <td>列表</td>
   <td>列舉型別DDE的一組允許值。 例如，帳戶型別只能有（儲存、目前）值。</td>
  </tr>
  <tr>
   <td>extendedProperties</td>
   <td>对象</td>
   <td>新增到DDE的自訂屬性地圖（使用者介面特定或任何其他資訊）。</td>
  </tr>
  <tr>
   <td>必填</td>
   <td>布尔值</td>
   <td>此旗標指出與資料字典對應的例項資料來源必須包含此特定DDE的值。</td>
  </tr>
  <tr>
   <td>捆绑</td>
   <td>Bindingelement</td>
   <td>元素的XML或Java繫結。</td>
  </tr>
 </tbody>
</table>

### 計算的資料字典元素 {#computedddelements}

資料字典也可以包含計算元素。 計算資料字典元素一律與運算式相關聯。 此運算式的評估目的是在執行階段取得資料字典元素的值。 計算的DDE值是其他DDE值或常值的函式。 預設支援JSP運算式語言(EL)運算式。 EL運算式使用${ }字元，有效的運算式可包含常值、運運算元、變數（資料字典元素參考）和函式呼叫。 在運算式中參考資料字典元素時，會使用DDE的參考名稱。 資料字典中每個資料字典元素的參考名稱都是唯一的。

計算過的DDE PersonFullName可與EL串連運算式相關聯，例如${PersonFirstName} ${PersonLastName}。

## XSD與資料字典之間的資料型別對應 {#data-type-mapping-between-xsd-and-data-dictionary-br}

匯出XSD需要特定的資料對應，下表對此有詳細說明。 DDI資料欄會指出DDI中可用的DDE值型別。

<table>
 <tbody>
  <tr>
   <td>XSD <br /> </td>
   <td><p>数据字典 <br /> </p> </td>
   <td>DDI （執行個體值資料型別）<br /> </p> </td>
  </tr>
  <tr>
   <td><p>xs：型別的元素 — 複合型別<br /> </p> </td>
   <td>型別的DDE — 複合<br /> </p> </td>
   <td>java.util.Map<br /> </td>
  </tr>
  <tr>
   <td><p>xs：元素，其中maxOccurs &gt; 1<br /> </p> </td>
   <td>型別的DDE — 集合 — <br /> COLLECTION DDE會建立一個DDE節點，用來擷取上層COLLECTION節點的資訊。 對於簡單/複合資料型別的集合，也會建立相同的。 只要您擁有型別複合的COLLECTION，資料字典樹狀結構就會擷取為擷取型別資訊而建立之DDE子系中的組成欄位。<br /> - DDE （集合）<br /> - DDE（型別資訊的複合）<br /> - DDE(STRING)欄位1<br /> - DDE(STRING)欄位2<br /> <br /> </p> </td>
   <td>java.util.List<br /> </td>
  </tr>
  <tr>
   <td>型別的屬性 — xs：id <br /> </p> </td>
   <td>型別 — 字串的DDE <br /> </td>
   <td>java.lang.String<br /> </td>
  </tr>
  <tr>
   <td>xs：attribute /xs：element型別 — xs：string</p> </td>
   <td>型別 — 字串的DDE<br /> </td>
   <td>java.lang.String<br /> </td>
  </tr>
  <tr>
   <td>xs：attribute /xs：element型別 — xs：布林值 <br /> </td>
   <td>型別的DDE — 布林值 <br /> </td>
   <td>java.lang.Boolean<br /> </td>
  </tr>
  <tr>
   <td>xs：attribute /xs：element型別 — xs：date </td>
   <td>型別的DDE — 日期 </td>
   <td>java.lang.String</td>
  </tr>
  <tr>
   <td>xs：attribute /xs：element型別 — xs：integer </td>
   <td>型別 — 數字的DDE </td>
   <td>java.lang.Double</td>
  </tr>
  <tr>
   <td>xs：attribute /xs：element型別 — xs：long</td>
   <td>型別 — 數字的DDE </td>
   <td>java.lang.Double</td>
  </tr>
  <tr>
   <td>xs：attribute /xs：element型別 — xs：double</td>
   <td>型別 — 數字的DDE </td>
   <td>java.lang.Double</td>
  </tr>
  <tr>
   <td>列舉型別和baseType的元素 — xs：string</td>
   <td>DDE /<br /> 型別 — 字串<br /> 子型別 — 列舉<br /> valueSet - ENUM允許的值<br /> </td>
   <td>java.lang.String</td>
  </tr>
 </tbody>
</table>

## 從資料字典下載範例資料檔案 {#download-a-sample-data-file-from-a-data-dictionary}

建立資料字典後，您可以下載為XML範例資料檔案，在其中輸入文字。

1. 在「資料字典」頁面中，點選 **選取** 然後點選資料字典加以選取。
1. 選取 **下載範例XML資料**.
1. 點選 **確定** 在警示訊息中。

   Correspondence Management會根據選取的資料字典結構建立XML檔案，然後以名稱將其下載到您的電腦 &lt;data-dictionary-name>-SampleData。 現在，您可以在XML或文字編輯器中編輯此檔案，以便在下列情況下輸入資料： [建立字母](../../forms/using/create-letter.md).

## 中繼資料的國際化 {#internationalization-of-meta-data}

當您想要以不同語言傳送相同信函給客戶時，可以本地化「資料字典」和「資料字典元素」的顯示名稱、說明和列舉值集。

### 將資料字典當地語系化 {#localize-data-dictionary}

1. 在資料字典頁面上，點選 **選取** 然後點選資料字典加以選取。
1. 點選 **下載本地化資料**.
1. 點選 **確定** 在警示中。 「通訊管理」會將名稱為DataDictionary的zip檔案下載到您的電腦 — &lt;ddname>.zip.
1. Zip檔案包含.properties檔案。 此檔案會定義下載的資料字典。 屬性檔案的內容類似於以下內容：

   ```ini
   #Wed May 20 16:06:23 BST 2015
   DataDictionary.EmployeeDD.description=
   DataDictionary.EmployeeDD.displayName=EmployeeDataDictionary
   DataDictionaryElement.name.description=
   DataDictionaryElement.name.displayName=name
   DataDictionaryElement.person.description=
   DataDictionaryElement.person.displayName=person
   ```

   屬性檔案的結構為資料字典的說明和顯示名稱各定義一行，以及資料字典中的每個資料字典元素。 此外，屬性檔案會針對每個資料字典元素所設定的列舉值定義一行。 與資料字典一樣，對應的屬性檔案可以有多個資料字典元素定義。 此外，檔案可以包含一或多個列舉值集的定義。

1. 若要更新不同地區設定的.properties檔案，請更新檔案中的顯示名稱和說明值。 針對您想要本地化的每種語言，建立更多檔案例項。 僅支援法文、德文、日文和英文。

1. 使用下列名稱儲存不同的更新屬性檔案：

   _fr_FR.properties法文

   _de_DE.properties德文

   _ja_JA.properties日文

   _en_EN.properties英文

1. 將.properties檔案（或多個區域設定的檔案）封存至單一.zip檔案中。

1. 在「資料字典」頁面中，選取 **更多** > **上傳本地化資料** 並選取包含當地語系化屬性檔案的zip檔案。
1. 若要檢視本地化變更，請變更您的瀏覽器地區設定。

## 資料字典驗證 {#ddvalidations}

資料字典編輯器會在建立或更新資料字典時強制進行下列驗證。

* 資料字典中僅允許複合型別做為頂層元素。
* 分葉層次不允許使用複合與收集元素。 分葉層級只允許基本元素（字串、日期、數字、布林值）。 此驗證可確保沒有任何複合與收集元素沒有子DDE。
* 上傳XSD檔案以建立資料字典時，資料字典編輯器會提示輸入頂層元素（如果存在多個元素）以建立資料字典。
* 名稱是資料字典唯一需要的引數。
* 父系DDE （複合）不能有兩個同名的子系
* 確保只有在不是必要引數時，才會將DDE標籤為已計算。 無法計算必要的元素，也不需要計算元素。 此外，集合和複合元素不能是計算元素。
* 確保DDE標示為必要，除非未計算。 它也能確保它不是表示「集合」型別的「collectionElement」（集合元素的唯一子系）。
* 資料字典或DDE的extendedProperties中不允許空白索引鍵或重複索引鍵。
* 請勿在延伸屬性的索引鍵或值中使用冒號(：)或垂直列(|)字元。 對於這些禁止使用的字元的使用沒有驗證。

在資料字典層級套用的驗證

* 資料字典名稱不得為Null。
* 資料字典名稱僅可包含英數字元。
* 資料字典中的子元素清單不得為Null或空白。
* 資料字典不得包含超過一個頂層資料字典元素。
* 資料字典中只允許複合型別做為頂層元素。

在資料字典元素層級套用的驗證。

* 所有DDE名稱不可以是Null，而且不能包含空格。
* 所有DDE都必須有「非null/非null」元素型別。
* 所有DDE參考名稱不可以是Null。
* 所有DDE參照名稱必須是唯一的。
* 所有DDE參考只能包含英數字元和「_」。
* 所有DDE顯示名稱只能包含英數字元和「_」。
* 分葉層次不允許使用複合與收集元素。 分葉層級只允許基本元素（字串、日期、數字、布林值）。 此驗證可確保沒有任何複合與收集元素沒有子DDE。
* 複合父DDE不能有兩個同名的子元素。
* ENUM子型別僅用於String和Number元素。
* 無法計算集合和複合元素。
* DDE不可同時為已計算與必要。
* 計算的DDE必須包含有效的運算式。
* 計算的DDE不可以有XML繫結。
* 無法計算或需要表示集合DDE型別的DDE。
* 子型別ENUM的DDE不得包含null或空值集。
* 集合DDE的XML繫結不得對應至屬性。
* XML繫結語法必須有效，例如，只有一個@出現，只有在後面跟有屬性名稱時才允許@。

## 將資料字典元素對應至XML綱要 {#mappingddetoschema}

您可以從「XML綱要」建立資料字典，或使用「資料字典」使用者介面來建置它。 資料字典中的所有資料字典元素(DDE)都有一個「XML繫結」欄位，可儲存DDE與XML結構描述中元素的繫結。 每個DDE中的繫結都是相對於父DDE的。

以下詳細資訊範例模型和程式碼範例顯示資料字典的實作詳細資料。

## 對應簡單（基本）元素 {#mapping-simple-primitive-elements}

基本的DDE代表本質為原子性的欄位或屬性。 定義在複雜型別（複合DDE）或重複元素（集合DDE）範圍以外的基本DDE可以儲存在XML Schema內的任何位置。 對應至基本DDE的資料位置不取決於其父DDE的對應。 基本DDE會使用「XML繫結」欄位的對應資訊來決定其值，且對應會轉換為下列其中一項：

* 屬性
* 元素
* 文字內容
* 無（忽略的DDE）

以下範例顯示一個簡單的結構描述。

```xml
<?xml version="1.0" encoding="UTF-8"?>
<xs:schema xmlns:xs="https://www.w3.org/2001/XMLSchema">
  <xs:element name='age' type='integer'/>
  <xs:element name='price' type='decimal'/>
</xs:schema>
```

| **資料字典元素** | **預設XML繫結** |
|---|---|
| 年龄 | /年龄 |
| 价格 | /价格 |

### 對應複合元素 {#mapping-composite-elements}

複合元素不支援繫結，如果提供繫結，則會忽略該繫結。 基本型別的所有組成子DDE的繫結必須是絕對的。 允許複合DDE子元素的絕對對應，可提供XPath繫結方面的更多彈性。 將複合DDE對應到XML結構描述中的複雜型別元素，會限制其子元素的繫結範圍。

以下範例顯示註記的結構描述。

```xml
<xs:element name="note">
    <xs:complexType>
        <xs:sequence>
            <xs:element name="to" type="xs:string"/>
            <xs:element name="from" type="xs:string"/>
            <xs:element name="heading" type="xs:string"/>
            <xs:element name="body" type="xs:string"/>
        </xs:sequence>
    </xs:complexType>
</xs:element>
```

<table>
 <tbody>
  <tr>
   <td><strong>資料字典元素</strong></td>
   <td><strong>預設XML繫結</strong></td>
  </tr>
  <tr>
   <td>注意</td>
   <td>empty(null)<br /> </td>
  </tr>
  <tr>
   <td>到</td>
   <td>/note/to</td>
  </tr>
  <tr>
   <td>从</td>
   <td>/note/from</td>
  </tr>
  <tr>
   <td>标题</td>
   <td>/note/heading</td>
  </tr>
  <tr>
   <td>內文</td>
   <td>/note/body</td>
  </tr>
 </tbody>
</table>

### 對應收集要素 {#mapping-collection-elements}

收集要素只對應至基數> 1的其他收集要素。 集合DDE的子DDE具有與其父系的XML繫結相關的相對（本機） XML繫結。 由於集合元素的子DDE必須具有與父系相同的基數，因此相對繫結必須確保基數限制，以便子DDE不會指向非重複的XML結構描述元素。 在以下範例中，「TokenID」的基數必須與其父集合DDE的「Token」相同。

將集合DDE對應至XML Schema元素時：

* 與Collection元素對應的DDE繫結必須是絕對XPath

* 不提供代表Collection元素型別的DDE繫結。 如果提供，則會忽略繫結。

* Collection元素之所有子DDE的繫結必須相對於父Collection元素。

下列XML結構描述會宣告名稱為Token且maxOccurs屬性為「unbounded」的元素。 因此，Token是收集元素。

```xml
<?xml version="1.0" encoding="utf-8"?>
<Root>
  <Tokens>
    <TokenID>string</TokenID>
    <TokenText>
      <TextHeading>string</TextHeading>
      <TextBody>string</TextBody>
    </TokenText>
  </Tokens>
  <Tokens>
    <TokenID>string</TokenID>
    <TokenText>
      <TextHeading>string</TextHeading>
      <TextBody>string</TextBody>
    </TokenText>
  </Tokens>
  <Tokens>
    <TokenID>string</TokenID>
    <TokenText>
      <TextHeading>string</TextHeading>
      <TextBody>string</TextBody>
    </TokenText>
  </Tokens>
</Root>
```

與此範例關聯的Token.xsd將是：

```xml
<xs:element name="Root">
  <xs:complexType>
    <xs:sequence>
      <xs:element name="Tokens" type="TokenType" maxOccurs="unbounded"/>
    </xs:sequence>
  </xs:complexType>
</xs:element>

<xs:complexType name="TokenType">
  <xs:sequence>
    <xs:element name="TokenID" type="xs:string"/>
    <xs:element name="TokenText">
      <xs:complexType>
        <xs:sequence>
          <xs:element name="TextHeading" type="xs:string"/>
          <xs:element name="TextBody" type="xs:string"/>
        </xs:sequence>
      </xs:complexType>
    </xs:element>
  </xs:sequence>
</xs:complexType>
```

| **資料字典元素** | **預設XML繫結** |
|---|---|
| 根 | empty(null) |
| Token | /Root/Tokens |
| 复合 | empty(null) |
| 權杖ID | 權杖ID |
| 權杖文字 | empty(null) |
| 權杖標題 | TokenText/TextHeading |
| TokenBody | TokenText/文字內文 |
