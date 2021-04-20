---
title: 访问字母实例的API
seo-title: 访问字母实例的API
description: 了解如何使用API访问字母实例。
seo-description: 了解如何使用API访问字母实例。
uuid: e7fb7798-f49d-458f-87f5-22df5f3e7d10
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: 9c27f976-972a-4250-b56d-b84a7d72f8c8
feature: Correspondence Management
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '594'
ht-degree: 1%

---


# 访问字母实例{#apis-to-access-letter-instances}的API

## 概述 {#overview}

使用Corresponce Management的“创建通信UI”，您可以保存正在进行中的字母实例的草稿，并且存在已提交的字母实例。

Correndence Management为您提供了API，您可以使用它构建列表界面以处理已提交的信函实例或草稿。 API列表并打开代理的已提交和已草拟字母实例，以便代理可以继续处理草稿或已提交的字母实例。

## 正在获取字母实例{#fetching-letter-instances}

Corresponce Management公开API以通过LetterInstanceService服务获取字母实例。

| 方法 | 描述 |
|--- |--- |
| getAllLetterInstances | 根据输入查询参数获取字母实例。 要获取所有字母实例，请将查询参数作为null传递。 |
| getLetterInstance | 根据字母实例Id获取指定的字母实例。 |
| letterInstanceExists | 检查给定名称是否存在LetterInstance。 |

>[!NOTE]
>
>LetterInstanceService是OSGI服务，它的实例可通过在Java中使用@Reference来检索
>类或sling.getService(LetterInstanceService)。 类)。

### 使用getAllLetterInstances {#using-nbsp-getallletterinstances}

以下API根据查询对象（“已提交”和“草稿”）查找字母实例。 如果查询对象为null，则返回所有字母实例。 此API返回[LetterInstanceVO](https://helpx.adobe.com/aem-forms/6-2/javadocs/com/adobe/icc/dbforms/obj/LetterInstanceVO.html)对象的列表，可用于提取字母实例的其他信息

**语法**:  `List getAllLetterInstances(Query query) throws ICCException;`

<table>
 <tbody>
  <tr>
   <td><strong>参数</strong></td>
   <td><strong>描述</strong></td>
  </tr>
  <tr>
   <td>查询</td>
   <td>查询参数用于查找/筛选Letter实例。 此处的查询仅支持对象的顶级属性/属性。 查询由语句组成，Statement对象中使用的“attributeName”应为Letter实例对象中属性的名称。<br /> </td>
  </tr>
 </tbody>
</table>

#### 示例1:提取SUBMITTED {#example-fetch-all-the-letter-instances-of-type-submitted}类型的所有字母实例

以下代码返回已提交字母实例的列表。 要仅获取草稿，请将`LetterInstanceType.COMPLETE.name()`更改为`LetterInstanceType.DRAFT.name().`

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

#### 示例2：提取用户提交的所有字母实例，并且字母实例类型为DRAFT {#example-nbsp-fetch-all-the-letter-instances-submitted-by-a-user-and-letter-instance-type-is-draft}

以下代码在同一查询中有多个语句，以根据用户提交的字母实例（属性提交者）等不同条件过滤结果，并且letterInstanceType的类型为DRAFT。

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

获取由给定字母实例id标识的字母实例。 如果实例ID不匹配，则返回“ null”。

**语法：** `public LetterInstanceVO getLetterInstance(String letterInstanceId) throws ICCException;`

```java
@Reference
LetterInstanceService letterInstanceService;
String letterInstanceId = "/content/apps/cm/letterInstances/1001/sampleLetterInstance";
LetterInstanceVO letterInstance = letterInstanceService.getLetterInstance(letterInstanceId );
```

### 验证LetterInstance是否存在{#verifying-if-letterinstance-exist}

检查给定名称是否存在字母实例

**语法**:  `public Boolean letterInstanceExists(String letterInstanceName) throws ICCException;`

| **参数** | **描述** |
|---|---|
| letterInstanceName | 要检查其是否存在的字母实例的名称。 |

```java
@Reference
LetterInstanceService letterInstanceService;
String letterInstanceName = "sampleLetterInstance";
Boolean result = letterInstanceService.letterInstanceExists(letterInstanceName );
```

## 打开字母实例{#opening-letter-instances}

字母实例的类型可以是“已提交”或“草稿”。 打开两个字母实例类型时显示不同的行为：

* 如果是“已提交的信函实例”，则会打开表示信函实例的PDF。 服务器上保留的已提交Letter实例还包含dataXML和已处理的XDP，它可用于完成和进一步自定义用例，如创建PDF/A。
* 如果是Draft字母实例，则创建通信UI将重新加载到与创建草稿时相同的上一状态

### 打开草稿字母实例  {#opening-draft-letter-instance-nbsp}

CCR UI支持cmLetterInstanceId参数，该参数可用于重新加载字母。

`https://[hostName]:[portNo]/[contextPath]//aem/forms/createcorrespondence.html?random=[randomNo]&cmLetterInstanceId=[letterInstanceId]`

>[!NOTE]
>
>重新加载通信时，您不必指定cmLetterId或cmLetterName/State/Version，因为提交的数据已经包含有关重新加载的通信的所有详细信息。 RandomNo用于避免浏览器缓存问题，您可以使用时间戳作为随机数。

### 正在打开已提交的信函实例{#opening-submitted-letter-instance}

提交的PDF可以使用字母实例ID直接打开：

`https://[hostName]:[portNo]/[contextPath]/[letterInstanceId]`
