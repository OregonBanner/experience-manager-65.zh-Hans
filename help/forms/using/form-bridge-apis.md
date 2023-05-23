---
title: 適用於HTML5表單的Form Bridge API
seo-title: Form Bridge APIs for HTML5 forms
description: 外部應用程式會使用FormBridge API連線至XFA行動表單。 API會在父視窗上排程FormBridgeInitialized事件。
seo-description: External applications use the FormBridge API to connect to the XFA Mobile Form. The API dispatches a FormBridgeInitialized event on the parent window.
uuid: 0db22649-522b-4857-9ffd-826c52381d15
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: developer-reference
discoiquuid: c05c9911-7c49-4342-89de-61b8b9953c83
exl-id: b598ef47-49ff-4806-8cc7-4394aa068eaa
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '940'
ht-degree: 0%

---

# 適用於HTML5表單的Form Bridge API {#form-bridge-apis-for-html-forms}

您可以使用Form Bridge API來開啟XFA型HTML5表單與您的應用程式之間的通訊通道。 Form Bridge API提供 **connect** 用於建立連線的API。

此 **connect** API接受處理常式作為引數。 在XFA型HTML5表單與表單橋接器之間成功建立連線後，就會叫用控制代碼。

您可以使用以下範常式式碼來建立連線。

```javascript
// Example showing how to connect to FormBridge
window.addEventListener("FormBridgeInitialized",
                                function(event) {
                                    var fb = event.detail.formBridge;
                                    fb.connect(function() {
                                           //use form bridge functions
                         })
                            })
```

>[!NOTE]
>
>在加入formRuntime.jsp檔案之前，請確定您已建立連線。

## 可用的Form Bridge API  {#available-form-bridge-api-nbsp}

**getBridgeVersion()**

傳回指令碼程式庫的版本號碼

* **輸入**：無
* **輸出**：指令碼程式庫的版本號碼
* **錯誤**：無

**isConnected()** 檢查表單狀態是否已初始化

* **輸入**：無
* **輸出**： **True** 如果XFA表單狀態已初始化

* **錯誤**：無

**connect(handler， context)** 連線至FormBridge並在連線完成且表單狀態初始化後執行函式

* **输入**:

   * **處理常式**：連線Form Bridge後要執行的函式
   * **內容**：前後關聯（這個）的目標物件 *處理常式* 函式已設定。

* **輸出**：無
* **錯誤**：無

**getDataXML(options)** 以XML格式傳回目前的表單資料

* **输入:**

   * **選項：** 包含下列屬性的JavaScript物件：

      * **錯誤**：錯誤處理常式函式
      * **成功**：成功處理常式函式。 此函式傳遞一個包含XML的物件 *資料* 屬性。
      * **內容**：前後關聯（這個）的目標物件 *成功* 函式已設定
      * **validationChecker**：呼叫以檢查從伺服器收到的驗證錯誤的函式。 驗證函式傳遞了錯誤字串陣列。
      * **formState**：必須傳回資料XML之XFA表單的JSON狀態。 如果未指定，則會傳回目前轉譯之表單的資料XML。

* **輸出：** 無
* **錯誤：** 無

**registerConfig(configName， config)** 向FormBridge註冊使用者/入口網站的特定設定。 這些設定會覆寫預設設定。 在設定區段中指定支援的設定。

* **输入:**

   * **configName：** 要覆寫的設定名稱

      * **widgetConfig：** 允許使用者以自訂Widget覆寫表單中的預設Widget。 設定會覆寫，如下所示：

         *formBridge.registerConfig(&quot;widgetConfig&quot;：{/&amp;ast；configuration&amp;ast；/})*

      * **pagingConfig：** 允許使用者覆寫僅轉譯第一頁的預設行為。 設定會覆寫，如下所示：

         *window.formBridge.registerConfig(&quot;pagingConfig&quot;：{pagingDisabled： &lt;true false=&quot;&quot;>，shrinkPageDisabled： &lt;true false=&quot;&quot;> })。*

      * **Loggingconfig：** 允許使用者覆寫記錄層級、停用類別的記錄，或是否要顯示記錄主控台或傳送至伺服器。 設定可以覆寫，如下所示：

      ```javascript
      formBridge.registerConfig{
        "LoggerConfig" : {
      {
      "on":`<true *| *false>`,
      "category":`<array of categories>`,
      "level":`<level of categories>`, "
      type":`<"console"/"server"/"both">`
      }
        }
      ```

      * **SubmitServiceProxyConfig：** 允許使用者註冊提交和記錄器Proxy服務。

         ```javascript
         window.formBridge.registerConfig("submitServiceProxyConfig",
         {
         "submitServiceProxy" : "`<submitServiceProxy>`",
         "logServiceProxy": "`<logServiceProxy>`",
         "submitUrl" : "`<submitUrl>`"
         });
         ```
   * **設定：** 設定的值



* **輸出：** 包含中組態原始值的物件 *資料* 屬性。

* **錯誤：** 無

**hideFields(fieldArray)** 隱藏fieldArray中提供Som運算式的欄位。 將指定欄位的presence屬性設定為隱藏

* **输入:**

   * **fieldArray：** 要隱藏之欄位的Som運算式陣列

* **輸出：** 無
* **錯誤：** 無

**showFields(fieldArray)** 顯示fieldArray中提供Som運算式的欄位。 將所提供欄位的presence屬性設定為可見

* **输入:**

   * **fieldArray：** 要顯示之欄位的Som運算式陣列

* **輸出：** 無
* **錯誤：** 無

**hideSubmitButton()** 隱藏表單中的所有提交按鈕

* **輸入**：無
* **輸出**：無
* **錯誤**：如果未初始化表單狀態，則會擲回例外狀況

**getFormState()** 傳回代表表單狀態的JSON

* **輸入：** 無
* **輸出：** 物件，內含代表下列專案之目前表單狀態的JSON： *資料* 屬性。

* **錯誤：** 無

**restoreFormState(options)** 從選項物件中提供的JSON狀態還原表單狀態。 狀態已套用，並在作業完成後呼叫成功或錯誤處理常式

* **输入:**

   * **選項：** 包含下列屬性的JavaScript物件：

      * **錯誤**：錯誤處理常式函式
      * **成功**：成功處理常式函式
      * **內容**：前後關聯（這個）的目標物件 *成功* 函式已設定
      * **formState**：表單的JSON狀態。 表單會還原為JSON狀態。

* **輸出：** 無
* **錯誤：** 無

**setFocus (som)** 將焦點設定在Som運算式中指定的欄位

* **輸入：** 要設定焦點的欄位的一些運算式
* **輸出：** 無
* **錯誤：** Som運算式不正確時擲回例外狀況

**setFieldValue (som， value)** 設定指定Som運算式的欄位值

* **输入:**

   * **som：** 包含欄位的Som運算式的陣列。 用來設定欄位值的som運算式。
   * **值：** 陣列包含對應至中提供的Som運算式的值 **som**&#x200B;陣列。 如果值的資料型別與fieldType不同，則不會修改值。

* **輸出：** 無
* **錯誤：** Som運算式不正確時擲回例外狀況

**getFieldValue (som)** 傳回指定Som運算式的欄位值

* **輸入：** 包含必須擷取其值之欄位的Som運算式的陣列
* **輸出：** 包含結果為Array的物件 **資料** 屬性。

* **錯誤：** 無

### getFieldValue() API範例 {#example-of-nbsp-getfieldvalue-api}

```JavaScript
var a =  formBridge.getFieldValue("xfa.form.form1.Subform1.TextField");
if(a.errors) {
    var err;
     while((err = a.getNextMessage()) != null)
               alert(a.message)
} else {
   alert(a.data[0])
}
```

**getFieldProperties(som， property)** 擷取Som運算式中所指定欄位之指定屬性的值清單

* **输入:**

   * **som：** 包含欄位的Som運算式的陣列
   * **屬性**：需要其值的屬性名稱

* **輸出：** 包含結果為Array的物件 *資料* 屬性

* **錯誤：** 無

**setFieldProperties（som，屬性，值）** 為Som運算式中指定的所有欄位設定指定屬性的值

* **输入:**

   * **som：** 包含必須設定其值的欄位之Som運算式的陣列
   * **屬性**：必須設定值的屬性
   * **值：** 包含Som運算式中所指定欄位之指定屬性的值的陣列

* **輸出：** 無
* **錯誤：** 無

## Form Bridge API的範例用法 {#sample-usage-of-form-bridge-api}

```JavaScript
// Example 1: FormBridge.restoreFormState
  function loadFormState() {
    var suc = function(obj) {
             //success
            }
    var err = function(obj) {
           while(var t = obj.getNextMessage()) {
         $("#errorDiv").append("<div>"+t.message+"</div>");
           }
           }
        var _formState = // load form state from storage
    formBridge.restoreFormState({success:suc,error:err,formState:_formState}); // not passing a context means that this will be formBridge itself. Validation errors will be checked.
  }

//--------------------------------------------------------------------------------------------------

//Example 2: FormBridge.submitForm
  function SubmitForm() {
    var suc = function(obj) {
             var data = obj.data;
         // submit the data to a url;
            }
    var err = function(obj) {
           while(var t = obj.getNextMessage()) {
         $("#errorDiv").append("<div>"+t.message+"</div>");
           }
           }
    formBridge.submitForm({success:suc,error:err}); // not passing a context means that this will be formBridge itself. Validation errors will be checked.
  }
```
