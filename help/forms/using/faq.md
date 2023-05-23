---
title: HTML5表單常見問題集(FAQ)
seo-title: Frequently asked questions (FAQ) for HTML5 forms
description: 關於版面配置、指令碼支援和HTML5表單範圍的常見問答(FAQ)。
seo-description: Frequently Asked Questions (FAQ) about layout, scripting support, and scope of HTML5 forms.
uuid: 398e31de-3e46-4288-b3cd-39d51fa17abc
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 4b676e7e-191f-4a19-8b8f-fc3e30244b59
docset: aem65
feature: Mobile Forms
exl-id: 85c9315e-1bc8-44a9-937e-af6fc7cf54d1
source-git-commit: 99c9eddad7a2ec7eb23b3c374a1c0e65e141da20
workflow-type: tm+mt
source-wordcount: '2005'
ht-degree: 0%

---


# HTML5表單常見問題集(FAQ){#frequently-asked-questions-faq-for-html-forms}

有一些關於版面配置、指令碼支援和HTML5表單範圍的常見問題(FAQ)。

## 布局 {#layout}

1. 中的條碼和簽名欄位為何沒有出現在我的表單中？

   答案：條碼和簽名欄位在HTML或行動場景中沒有關聯。 這些欄位會顯示為非互動區域。 不過，AEM Forms Designer提供新的簽名手寫欄位，可用來取代簽名欄位。 您也可以新增 [自訂Widget](../../forms/using/custom-widgets.md) 並加以整合。

1. XFA文字欄位是否支援RTF文字？

   回答： XFA欄位允許AEM Forms Designer中的RTF內容，但是不受支援，而且會呈現為一般文字，不支援從使用者介面設定文字的樣式。 此外，具有梳狀屬性的XFA欄位會顯示為一般欄位，不過根據梳狀位數的值，允許的字元數仍有限制。

1. 使用可重複的子表單是否有任何限制？

   答案：可重複子表單的初始計數應為1或更多。 不支援初始計數為零的可重複子表單。 您也可以選擇使用可重複的子表單，而在載入表單時不要顯示它。 若要達成使用案例：

   1. 將可重複子表單的初始計數設為1。

      ![初始計數](assets/intial-count.png)

   1. 使用表單的初始化事件來隱藏子表單的主要執行個體。 例如，下列程式碼會在表單初始化時隱藏子表單的主要例項。 它也會驗證應用程式型別，以確保指令碼僅在使用者端上執行：

      ```javascript
      if ((xfa.host.appType == "HTML 5" || xfa.host.appType == "Exchange-Pro" || xfa.host.appType == "Reader")&&(_RepeatSubform.count == 1)&&(form1.Page1.Subform1.RepeatSubform.Key.rawValue == null)) {
      RepeatSubform.presence = "hidden";
      }
      ```

   1. 開啟指令碼，以新增要編輯的子表單例項。 新增如下所示的程式碼，以新增子表單指令碼的例項。

      以下程式碼會檢查子表單的隱藏執行個體。 如果找到子表單的隱藏實體，請刪除子表單的隱藏實體並插入新的子表單實體。 如果找不到子表單的隱藏實體，則只需插入新的子表單實體即可。

      ```javascript
      if (RepeatSubform.presence == "hidden")
      {
      RepeatSubform.instanceManager.insertInstance(0);
      RepeatSubform.instanceManager.removeInstance(1);
      }
      else
      {
      RepeatSubform.instanceManager.addInstance(1);
      }
      ```

   1. 開啟用於移除子表單例項的指令碼以進行編輯。 新增類似下列的程式碼以移除Subform指令碼的例項。

      程式碼會檢查子表單的計數。 如果子表單的計數達到1，則程式碼會隱藏子表單，而不是刪除子表單。

      ```javascript
      if (RepeatSubform.instanceManager.count == 1) {
      RepeatSubform.presence = "hidden";
      } else {
      RepeatSubform.instanceManager.removeInstance(RepeatSubform.instanceManager.count - 1);
      }
      ```

   1. 開啟表單的預先提交事件以進行編輯。 將下列指令碼新增至事件，以在編輯前移除指令碼的隱藏實體。 它可防止在提交時傳送隱藏子表單的資料。

      ```javascript
      if(RepeatSubform.instanceManager.count == 1 && RepeatSubform.presence == "hidden") {
      RepeatSubform.instanceManager.removeInstance(0);
      }
      ```

1. 關於使用隱藏的子表單是否有任何限制？

   答案：具有複雜階層的隱藏子表單會分割成不同頁面，導致版面配置問題。 因應措施是最初將子表單標示為可見，然後根據某些邏輯或資料在初始化指令碼中隱藏它。

1. 為什麼某些文字被截斷或在HTML5中顯示不正確？

   回答：如果「繪圖」或「註解」文字元素沒有足夠的空間顯示內容，行動表單轉譯中的文字會顯示為截斷。 此截斷也可在AEM Forms Designer的「設計」檢視中看到。 雖然此截斷可在PDF中處理，但無法在HTML5表單中處理。 為避免此問題，請為「繪圖」或「註解文字」提供足夠的空間，使其在AEM Forms Designer的設計模式中不會截斷。

1. 我觀察到與缺少內容或重疊內容相關的版面配置問題。 原因是什麼？

   回答：如果在相同位置有「繪製文字」或「繪製影像」元素與其他重疊元素（例如「矩形」），則「繪製文字」內容在檔案順序中較晚出現時不會顯示(在「AEM Forms設計工具階層」檢視中)。 PDF支援透明分層，但HTML/瀏覽器不支援透明分層。

1. 為什麼在HTML表單中顯示的某些字型與設計表單時使用的字型不同？

   回答：HTML5 Forms不允許內嵌字型(與將字型內嵌在表單中的PDF forms相反)。 若要讓表單的HTML版本如預期般呈現，請確定AEM Forms伺服器的CRX存放庫(AEM內容存放庫)中以及安裝AEM Designer的電腦上有可用的字型。 當AEM Forms伺服器的CRX存放庫或AEM Designer安裝位置中無法使用字型時，表單會以備援字型呈現。

1. HTML表單中是否支援vAlign和hAlign屬性？

   回答：是，支援vAlign和hAlign屬性。 Internet Explorer和多行欄位不支援vAlign屬性。

1. HTML5表單是否支援希伯來字元？

   答案：HTML5表單在Microsoft Internet Explorer以外的所有瀏覽器中皆支援希伯來字元。

1. HTML5表單對數值欄位有任何限制嗎？

   答案：是，HTML5表單有一些限制。 如果數字位數超過picture子句中指定的計數，則數字不會本地化，且會以英文地區設定顯示。

1. 為何HTML表單的大小比PDF forms大？

   答案：許多中繼資料結構和物件（例如表單dom、資料dom和版面配置dom）都是將XDP轉譯為HTML表單所必需。

   對於PDF forms，Adobe Acrobat有內建的XTG引擎可建立中繼資料結構和物件。 Acrobat也會處理版面和指令碼。

   對於HTML5表單，瀏覽器沒有內建的XTG引擎來建立中繼資料結構，以及從原始XDP位元組建立物件。 因此，對於HTML5表單，會在伺服器上產生中間結構並傳送給使用者端。 在使用者端，以JavaScript為基礎的指令碼和版面引擎會使用這些中間結構。

   中間結構的大小取決於原始XDP和與XDP合併的資料的大小。

1. 在xdp中使用表格是否有任何限制？

   回答：複雜的表格會導致轉譯時發生問題。

   * 不支援表格內的區段(SubformSet)。
   * 某些表格中的頁首或頁尾列會標示為重複。 在多個頁面上分割這類表格可能會遇到一些問題。

1. 可存取的表格有任何限制嗎？

   回答：是，可存取的表格有下列限制：

   * 不支援表格內的巢狀表格和子表單。
   * 只有表格的頂端列或左側欄支援標題。 中間表格元素不支援標頭。 您可以套用標題至多個支援的列和欄標題，前提是所有這樣的列和欄與表格最頂端的列或最左邊的欄一起提供。
   * `Rowspan`和 `colspan`不支援來自表格內的隨機位置。

   * 您無法動態新增或移除包含rowspan值大於1之元素的列例項。

1. 熒幕助讀程式的工具提示和註解的閱讀順序為何？

   答案:
   * 當註解與工具提示同時出現時，只會讀取註解。 如果註解無法使用，則會讀取工具提示。 您也可以使用表單設計工具來指定在XDP中讀取的優先順序
   * 將滑鼠懸停在元素上時，會顯示工具提示。 如果無法使用工具提示，則會顯示語音文字。 如果語音文字無法使用，則會顯示欄位名稱。

1. 當您將滑鼠懸停在欄位上時，會顯示工具提示。 如何停用此功能？

   回答：若要停用暫留時的工具提示，請在「設計工具」的協助工具面板中選取「無」。

1. 在Designer中，使用者可以設定選項按鈕和核取方塊的自訂外觀屬性。 轉譯表單時，HTML5表單會將此類自訂外觀屬性納入考量嗎？

   回答：HTML5表單忽略選項按鈕和核取方塊的自訂外觀屬性。 選項按鈕和核取方塊會根據基礎瀏覽器的規格顯示。

1. 在支援的瀏覽器中開啟HTML5表單時，相鄰放置欄位的邊框未正確對齊，或子表單出現重疊。 在Forms Designer中預覽相同的HTML5表單時，欄位和版面不會出現未對齊的情況，而子表單會出現在正確的位置。 如何修正問題？

   答案：當子表單設定為流程內容，且子表單有隱藏的邊框元素時，相鄰放置欄位的邊框未正確對齊，或子表單出現重疊。 若要解決此問題，您可以移除或註解隱藏的 &lt;border> 來自對應XDP的元素。 例如，下列專案 &lt;border> 元素會標示為註解：

   ```xml
               <!--<border>
                  <edge presence="hidden"/>
                  <corner thickness="0.175mm" presence="hidden"/>
               </border> -->
   ```

1. 為什麼熒幕助讀程式無法正確搭配日期/時間欄位物件運作？

   答案：熒幕助讀程式不支援日期/時間欄位。 不過，您可以手動在欄位中輸入日期/時間，讓熒幕助讀程式閱讀該欄位。 使用工具提示或熒幕助讀程式文字來指示使用者手動選取欄位的日期/時間。

1. HTML5表單是否支援浮動欄位的顯示模式？

   答案：HTML5表單不支援浮動欄位的顯示模式。

1. HTML5 Forms中「日期」欄位的格式為何？

答案：「日期」欄位接受ISO格式YYYY-MM-DD。 如果您以某種其他格式指定日期，在使用者將索引標籤移出欄位之前，「日期欄位」不接受格式。

### 指令碼 {#scripting}

1. HTML Forms的JavaScript實作是否有任何限制？

   答案:

   * xfa.connectionSet指令碼的支援有限。 對於connectionSet，僅支援伺服器端的Web服務呼叫。 如需詳細資訊，請參閱 [指令碼支援](/help/forms/using/scripting-support.md).
   * 使用者端指令碼中不支援$record和$data。 不過，如果指令碼是以formReady、layoutReady區塊寫入，則這些指令碼仍然有效，因為這些事件在伺服器端執行。
   * 不支援XFA Draw元素專屬指令碼，例如變更Draw文字（若是欄位，則為標題文字）。

1. 使用formCalc是否有任何限制？

   回答：目前僅實作formCalc指令碼的子集。 如需詳細資訊，請參閱 [指令碼支援](/help/forms/using/scripting-support.md).

1. 是否有任何建議的命名慣例，以及任何要避免的保留關鍵字？

   答案:
   * 在AEM Forms Designer中，建議不要以底線(_)。 若要在名稱開頭使用底線，請在底線後加上首碼，_&lt;prefix>&lt;objectname>.
   * 所有HTML5 Forms API都是保留關鍵字。 對於自訂API/函式，請使用與不相同的名稱 [HTML5 forms API](/help/forms/using/scripting-support.md).

1. HTML5表單是否支援浮動欄位？

   回答：是，HTML5 Forms支援浮動欄位。 若要啟用浮動欄位，請將下列屬性新增至演算設定檔：

   >[!NOTE]
   >
   >依預設，這些欄位不會啟用浮動功能。 您可以使用Forms Designer來設定欄位的浮動屬性。

   1. 開啟CRXde Lite並導覽至 `/content/xfaforms/profiles/default` 節點。
   1. 新增屬性 `mfDataDependentFloatingField`字串型別並將屬性的值設定為 `true`.
   1. 按一下 **全部儲存**. 現在已使用更新的轉譯設定檔為HTMLForms啟用浮動欄位。

      >[!NOTE]
      >
      >若要為特定表單啟用浮動欄位而不更新轉譯設定檔，請將mfDataDependentFloatingField=true屬性傳遞為URL引數。

1. HTML5表單會多次執行初始化指令碼和表單就緒事件嗎？

   回答：是，初始化指令碼和表單就緒事件會執行多次，在伺服器上至少執行一次，並在使用者端執行一次。 建議根據某些商業邏輯（表單或欄位資料）編寫初始化或form：ready事件等指令碼，以便根據資料狀態和等冪（如果資料相同）執行動作。

### 設計XDP {#designing-xdp}

1. HTML5表單中是否有任何保留關鍵字？

   回答：所有HTML5 Forms API都是保留關鍵字。 對於自訂API/函式，請使用與不相同的名稱 [HTML5 forms API](/help/forms/using/scripting-support.md). 除了保留的關鍵字之外，如果您使用以底線(_)開頭的物件名稱，建議在底線後新增唯一的前置詞。 新增首碼有助於避免與HTML5表單內部API發生任何可能的衝突。 例如，`_fpField1`
