---
title: 存取信件例項的API
seo-title: APIs to access letter instances
description: 瞭解如何使用API來存取信件例項。
seo-description: Learn how to use APIs to access letter instances.
uuid: e7fb7798-f49d-458f-87f5-22df5f3e7d10
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: 9c27f976-972a-4250-b56d-b84a7d72f8c8
feature: Correspondence Management
exl-id: 9d43d9d4-5487-416c-b641-e807227ac056
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '578'
ht-degree: 1%

---

# 存取信件例項的API {#apis-to-access-letter-instances}

## 概述 {#overview}

使用「通訊管理」的「建立通訊UI」，您可以儲存正在處理的信件例項草稿，並且有已提交的信件例項。

「通訊管理」會提供API，您可以使用這些API來建立清單介面，以處理已提交的信件例項或草稿。 API會列出並開啟代理程式的已提交和草稿信件例項，讓代理程式可以繼續處理草稿或已提交的信件例項。

## 正在擷取字母例項 {#fetching-letter-instances}

Correspondence Management會公開API，以透過LetterInstanceService服務擷取信件例項。

| 方法 | 描述 |
|--- |--- |
| getAllLetterInstances | 根據輸入查詢引數擷取信件例項。 若要擷取所有信件例項，請將查詢引數傳遞為null。 |
| getLetterInstance | 根據信件例項ID擷取指定的信件例項。 |
| letterInstanceExists | 檢查指定的名稱是否存在LetterInstance。 |

>[!NOTE]
>
>LetterInstanceService是OSGI服務，可以在Java中使用@Reference來擷取其執行個體
>類別或sling.getService(LetterInstanceService。 類別)。

### 使用getAllLetterInstances {#using-nbsp-getallletterinstances}

以下API會根據查詢物件（已提交和草稿）來尋找信件例項。 如果查詢物件為Null，則會傳回所有信件例項。 此API傳回以下清單： [LetterInstanceVO](https://helpx.adobe.com/aem-forms/6-2/javadocs/com/adobe/icc/dbforms/obj/LetterInstanceVO.html) 物件，可用於擷取信件例項的其他資訊

**語法**： `List getAllLetterInstances(Query query) throws ICCException;`

<table>
 <tbody>
  <tr>
   <td><strong>参数</strong></td>
   <td><strong>描述</strong></td>
  </tr>
  <tr>
   <td>查詢</td>
   <td>查詢引數是用來尋找/篩選Letter例項。 在此查詢僅支援物件的頂層屬性/屬性。 查詢由陳述式組成，Statement物件中使用的「attributeName」應為Letter實體物件中屬性的名稱。<br /> </td>
  </tr>
 </tbody>
</table>

#### 範例1：擷取SUBMITTED型別的所有字母例項 {#example-fetch-all-the-letter-instances-of-type-submitted}

下列程式碼會傳回已提交信件例項的清單。 若要僅取得草稿，請變更 `LetterInstanceType.COMPLETE.name()` 至 `LetterInstanceType.DRAFT.name().`

```java
@Reference
LetterInstanceService letterInstanceService;
Query query = new Query();

List<LetterInstanceVO> submittedLetterInstances = new ArrayList<LetterInstanceVO>();

Statement statementForInstanceType = new Statement();
statementForInstanceType.setAttributeName("letterInstanceType");
statementForInstanceType.setOperator(Operator.EQUALS);
statementForInstanceType.setAttributeValue(LetterInstanceType.COMPLETE.name());
query.addStatement(statementForInstanceType);
submittedLetterInstances = letterInstanceService.getAllLetterInstances(query);
```

#### 範例2：擷取使用者提交的所有信件例項，信件例項型別為DRAFT {#example-nbsp-fetch-all-the-letter-instances-submitted-by-a-user-and-letter-instance-type-is-draft}

下列程式碼在相同查詢中有多個陳述式，可取得根據不同條件篩選的結果，例如使用者提交的信件例項（屬性提交者），以及letterInstanceType的型別為DRAFT。

```java
@Reference
LetterInstanceService letterInstanceService;

String submittedBy = "tglodman";
Query query = new Query();

List<LetterInstanceVO> submittedLetterInstances = new ArrayList<LetterInstanceVO>();

Statement statementForInstanceType = new Statement();
statementForInstanceType.setAttributeName("letterInstanceType");
statementForInstanceType.setOperator(Operator.EQUALS);
statementForInstanceType.setAttributeValue(LetterInstanceType.COMPLETE.name());
query.addStatement(statementForInstanceType);

Statement statementForSubmittedBy = new Statement();
statementForSubmittedBy .setAttributeName("submittedby");
statementForSubmittedBy .setOperator(Operator.EQUALS);
statementForSubmittedBy .setAttributeValue(submittedBy);
query.addStatement(statementForSubmittedBy );
submittedLetterInstances = letterInstanceService.getAllLetterInstances(query);
```

### 使用getLetterInstance {#using-nbsp-getletterinstance}

擷取由指定的字母例項ID所識別的信件例項。 如果執行個體ID不相符，則會傳回「 null」。

**語法：** `public LetterInstanceVO getLetterInstance(String letterInstanceId) throws ICCException;`

```java
@Reference
LetterInstanceService letterInstanceService;
String letterInstanceId = "/content/apps/cm/letterInstances/1001/sampleLetterInstance";
LetterInstanceVO letterInstance = letterInstanceService.getLetterInstance(letterInstanceId );
```

### 正在驗證LetterInstance是否存在 {#verifying-if-letterinstance-exist}

檢查信件例項是否存在指定的名稱

**語法**： `public Boolean letterInstanceExists(String letterInstanceName) throws ICCException;`

| **参数** | **描述** |
|---|---|
| letterInstanceName | 您要檢查其是否存在的信件例項名稱。 |

```java
@Reference
LetterInstanceService letterInstanceService;
String letterInstanceName = "sampleLetterInstance";
Boolean result = letterInstanceService.letterInstanceExists(letterInstanceName );
```

## 開啟字母例項 {#opening-letter-instances}

信件例項可以是已提交或草稿型別。 開啟兩種信件實體型別會顯示不同的行為：

* 如果是Submitted letter例項，則會開啟代表該例項的PDF。 伺服器上持續存在的已提交信件例項也包含dataXML和已處理的XDP，這可用於完成並進一步自訂使用案例，例如建立PDF/A。
* 如果是「草稿信件」例項，則建立通訊UI會重新載入到與建立草稿時完全相同的先前狀態

### 開啟草稿字母例項  {#opening-draft-letter-instance-nbsp}

CCR UI支援cmLetterInstanceId引數，該引數可用於重新載入字母。

`https://[hostName]:[portNo]/[contextPath]//aem/forms/createcorrespondence.html?random=[randomNo]&cmLetterInstanceId=[letterInstanceId]`

>[!NOTE]
>
>重新載入通訊時，您不必指定cmLetterId或cmLetterName/State/Version，因為提交的資料已包含重新載入通訊的所有詳細資訊。 RandomNo可用來避免瀏覽器快取問題，您可以將時間戳記當成隨機數字使用。

### 開啟提交的字母例項 {#opening-submitted-letter-instance}

可使用字母例項ID直接開啟已提交的PDF：

`https://[hostName]:[portNo]/[contextPath]/[letterInstanceId]`
