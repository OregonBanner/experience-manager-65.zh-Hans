---
title: 運算式產生器中的遠端函式
seo-title: Expression Builder
description: 通訊管理中的運算式產生器可讓您建立運算式及遠端函式。
seo-description: Expression Builder in Correspondence Management lets you create expressions and remote functions.
uuid: 6afb84c0-ad03-4bb1-a154-d46cc47650ae
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: 68e3071e-7ce6-4bdc-8561-14bcaeae2b6c
docset: aem65
feature: Correspondence Management
exl-id: b41af9fe-c698-44b3-9ac6-97d42cdc02d4
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '786'
ht-degree: 1%

---

# 運算式產生器中的遠端函式{#remote-functions-in-expression-builder}

您可以使用「運算式產生器」建立運算式或條件，對「資料字典」或一般使用者提供的資料值進行計算。 「對應關係管理」會使用運算式評估的結果來選取文字、影像、清單和條件等資產，並視需要將其插入對應關係中。

## 使用運算式產生器建立運算式及遠端函式 {#creating-expressions-and-remote-functions-with-expression-builder}

運算式產生器內部使用JSP EL程式庫，因此運算式會遵循JSPEL語法。 如需詳細資訊，請參閱 [運算式範例](#exampleexpressions).

![表达式生成器](assets/expressionbuilder.png)

### 运算符 {#operators}

運算式產生器頂列中有可用於運算式的運運算元。

### 運算式範例 {#exampleexpressions}

以下是一些常用的JSP EL範例，您可以在通訊管理解決方案中使用：

* 若要新增兩個數字： ${number1 + number2}
* 若要串連兩個字串： ${str1} ${str2}
* 若要比較兩個數字： ${age &lt; 18}

如需詳細資訊，請參閱 [JSP EL規格](https://download.oracle.com/otn-pub/jcp/jsp-2.1-fr-spec-oth-JSpec/jsp-2_1-fr-spec-el.pdf). 使用者端運算式管理員不支援JSP EL規格中的某些變數和函式，特別是：

* 集合索引和對應索引鍵(使用 [] 表示法)的變數名稱中不支援在使用者端評估的運算式。
* 以下是運算式中使用的引數型別或傳回函式型別：

   * java.lang.String
   * java.lang.Character
   * Char
   * java.lang.Boolean
   * 布尔值
   * java.lang.Integer
   * Int
   * java.util.list
   * java.lang.Short
   * 短
   * java.lang.Byte
   * 位元組
   * java.lang.Double
   * 双精度型
   * java.lang.Long
   * 长整型
   * java.lang.Float
   * 浮点数
   * java.util.Calendar
   * java.util.Date
   * java.util.List

### 遠端函式 {#remote-function}

遠端函式提供在運算式中使用自訂邏輯的功能。 您可以將自訂邏輯寫入運算式，作為Java中的方法使用，並在運算式中使用相同的函式。 可用的遠端函式會列在運算式編輯器左側的「遠端函式」標籤下。

![remotefunction](assets/remotefunction.png)

#### 新增自訂遠端函式 {#adding-custom-remote-functions}

您可以建立自訂套件組合來匯出您自己的遠端函式，以便在運算式內使用。 若要建立自訂套件組合以匯出您自己的遠端函式，請執行下列工作。 它示範如何撰寫將輸入字串轉換為大寫的自訂函式。

1. 定義OSGi服務的介面，其中包含要匯出以供Expression Manager使用的方法。
1. 在介面A上宣告方法，並使用@ServiceMethod註解(com.adobe.exm.expeval.ServiceMethod)標註這些方法。 Expression Manager會忽略任何未標註的方法。 ServiceMethod附註具有下列可選屬性，也可以指定：

   1. **已啟用**：判斷此方法是否已啟用。 Expression Manager會忽略停用的方法。
   1. **familyId**：指定方法的系列（群組）。 如果為空，Expression Manager會假設方法屬於預設系列。 沒有從中選擇函式的系列登入（預設系列除外）。 Expression Manager會使用由各種組合匯出的所有函式所指定的所有系列ID的聯集，以動態方式建立登入。 請確定此處指定的ID可合理讀取，因為它也會顯示在運算式編寫使用者介面中。
   1. **顯示名稱**：人類看得懂的函式名稱。 此名稱用於製作使用者介面中的顯示目的。 如果為空，Expression Manager會使用函式的前置詞和local-name來建構預設名稱。
   1. **說明**：函式的詳細描述。 此說明用於製作使用者介面中的顯示用途。 如果為空，Expression Manager會使用函式的前置詞和local-name建構預設描述。

   ```java
   package mergeandfuse.com;
   import com.adobe.exm.expeval.ServiceMethod;
   
   public interface RemoteFunction {
    @ServiceMethod(enabled=true,displayName="Returns_all_caps",description="Function to convert to all CAPS", familyId="remote")
    public String toAllCaps(String name);
   
   }
   ```

   您也可以選擇使用@ServiceMethodParameter註解(com.adobe.exm.expeval.ServiceMethodParameter)標註方法的引數。 此註解僅用於指定在編寫使用者介面中使用的人類可讀名稱與方法引數說明。 確定介面方法的引數和傳回值屬於下列其中一種型別：

   * java.lang.String
   * java.lang.Character
   * Char
   * java.lang.Boolean
   * 布尔值
   * java.lang.Integer
   * Int
   * java.lang.Short
   * 短
   * java.lang.Byte
   * 位元組
   * java.lang.Double
   * 双精度型
   * java.lang.Long
   * 长整型
   * java.lang.Float
   * 浮点数
   * java.util.Calendar
   * java.util.Date
   * java.util.List


1. 定義介面的實作、將其設定為OSGI服務，並定義以下服務屬性：

```jsp
@org.apache.felix.scr.annotations.Properties({
  @org.apache.felix.scr.annotations.Property(name = "connectors.jsoninvoker", boolValue = true),
  @org.apache.felix.scr.annotations.Property(name = "connectors.jsoninvoker.alias", value = "<service_id>"),
  @org.apache.felix.scr.annotations.Property(name = "exm.service", boolValue = true)})
```

exm.service=true專案會指示Expression Manager此服務包含適用於運算式的遠端函式。 此 &lt;service_id> 值必須為有效的Java識別碼（英數、$、_且不含其他特殊字元）。 以REMOTE_關鍵字為前置詞的這個值，構成運算式內部使用的前置詞。 例如，使用REMOTE_foo：bar()可在運算式內參照具有註解方法bar()和服務屬性中服務ID的介面。

```java
package mergeandfuse.com;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Service;

@Component(metatype = true, immediate = true, label = "RemoteFunctionImpl")
@Service(value = RemoteFunction.class)
@org.apache.felix.scr.annotations.Properties({
  @org.apache.felix.scr.annotations.Property(name = "connectors.jsoninvoker", boolValue = true),
  @org.apache.felix.scr.annotations.Property(name = "connectors.jsoninvoker.alias", value = "test1"),
  @org.apache.felix.scr.annotations.Property(name = "exm.service", boolValue = true)})
public class RemoteFuntionImpl implements RemoteFunction {

 @Override
 public String toAllCaps(String name) {
  System.out.println("######Got######"+name);
  
  return name.toUpperCase();
 }
 
}
```

以下是要使用的範例封存：

* **GoodFunctions.jar.zip** 是jar檔案，其套件包含範例遠端函式定義。 下載GoodFunctions.jar.zip檔案並將其解壓縮以取得jar檔案。
* **GoodFunctions.zip** 是定義自訂遠端函式並為其建立套件組合的原始程式碼套件。

GoodFunctions.jar.zip

[获取文件](assets/goodfunctions.jar.zip)

GoodFunctions.zip

[获取文件](assets/goodfunctions.zip)
