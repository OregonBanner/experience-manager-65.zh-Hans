---
title: 用于访问信件实例的API
seo-title: 用于访问信件实例的API
description: 了解如何使用API访问信件实例。
seo-description: 了解如何使用API访问信件实例。
uuid: e7fb7798-f49d-458f-87f5-22df5f3e7d10
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: 9c27f976-972a-4250-b56d-b84a7d72f8c8
feature: 通信管理
exl-id: 9d43d9d4-5487-416c-b641-e807227ac056
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '594'
ht-degree: 1%

---

# 用于访问信件实例{#apis-to-access-letter-instances}的API

## 概述 {#overview}

使用通信管理的“创建通信”UI，可以保存正在进行中的信件实例的草稿，并且会提交信件实例。

通信管理为您提供了API，您可以使用这些API构建列表界面以处理提交的信件实例或草稿。 API列表，并打开代理提交的和草稿的信件实例，以便代理可以继续处理草稿或提交的信件实例。

## 正在获取信件实例{#fetching-letter-instances}

通信管理会公开API以通过LetterInstanceService服务获取信件实例。

| 方法 | 描述 |
|--- |--- |
| getAllLetterInstances | 根据输入查询参数获取信件实例。 要获取所有信件实例，请将查询参数传递为null。 |
| getLetterInstance | 根据信件实例ID获取指定的信件实例。 |
| letterInstanceExists | 检查LetterInstance是否按给定名称存在。 |

>[!NOTE]
>
>LetterInstanceService是OSGI服务，其实例可通过在Java中使@Reference来检索
>类或sling.getService(LetterInstanceService)。 类)。

### 使用getAllLetterInstances {#using-nbsp-getallletterinstances}

以下API根据查询对象（已提交和草稿）查找信件实例。 如果查询对象为null，则返回所有字母实例。 此API返回[LetterInstanceVO](https://helpx.adobe.com/aem-forms/6-2/javadocs/com/adobe/icc/dbforms/obj/LetterInstanceVO.html)对象的列表，该列表可用于提取字母实例的其他信息

**语法**:  `List getAllLetterInstances(Query query) throws ICCException;`

<table>
 <tbody>
  <tr>
   <td><strong>参数</strong></td>
   <td><strong>描述</strong></td>
  </tr>
  <tr>
   <td>查询</td>
   <td>查询参数用于查找/筛选信件实例。 此处查询仅支持对象的顶级属性/属性。 查询由语句组成，Statement对象中使用的“attributeName”应为Letter实例对象中属性的名称。<br /> </td>
  </tr>
 </tbody>
</table>

#### 示例1:获取类型为{#example-fetch-all-the-letter-instances-of-type-submitted}的所有信件实例

以下代码会返回已提交的信件实例列表。 要仅获取草稿，请将`LetterInstanceType.COMPLETE.name()`更改为`LetterInstanceType.DRAFT.name().`

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

#### 示例2：获取用户提交的所有信件实例，信件实例类型为DRAFT {#example-nbsp-fetch-all-the-letter-instances-submitted-by-a-user-and-letter-instance-type-is-draft}

以下代码在同一查询中包含多个语句，以获取根据用户提交的信件实例（由提交的属性）等不同条件筛选的结果，并且letterInstanceType的类型为DRAFT。

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

获取由给定信件实例id标识的信件实例。 如果实例ID不匹配，则返回“ null”。

**语法：** `public LetterInstanceVO getLetterInstance(String letterInstanceId) throws ICCException;`

```java
@Reference
LetterInstanceService letterInstanceService;
String letterInstanceId = "/content/apps/cm/letterInstances/1001/sampleLetterInstance";
LetterInstanceVO letterInstance = letterInstanceService.getLetterInstance(letterInstanceId );
```

### 验证LetterInstance是否存在{#verifying-if-letterinstance-exist}

检查信件实例是否按给定名称存在

**语法**:  `public Boolean letterInstanceExists(String letterInstanceName) throws ICCException;`

| **参数** | **描述** |
|---|---|
| letterInstanceName | 要检查其是否存在的信件实例的名称。 |

```java
@Reference
LetterInstanceService letterInstanceService;
String letterInstanceName = "sampleLetterInstance";
Boolean result = letterInstanceService.letterInstanceExists(letterInstanceName );
```

## 开始字母实例{#opening-letter-instances}

信件实例的类型可为“已提交”或“草稿”。 打开这两个字母实例类型会显示不同的行为：

* 如果是Submitted letter实例，则会打开表示该信件实例的PDF。 服务器上保留的已提交信件实例还包含dataXML和已处理的XDP，它可用于完成和进一步自定义用例，如创建PDF/A。
* 对于草稿信件实例，创建通信UI将重新加载到与创建草稿期间完全相同的先前状态

### 打开草稿信件实例  {#opening-draft-letter-instance-nbsp}

CCR UI支持cmLetterInstanceId参数，该参数可用于重新加载信件。

`https://[hostName]:[portNo]/[contextPath]//aem/forms/createcorrespondence.html?random=[randomNo]&cmLetterInstanceId=[letterInstanceId]`

>[!NOTE]
>
>重新加载通信时，您不必指定cmLetterId或cmLetterName/State/Version，因为提交的数据已经包含有关重新加载的通信的所有详细信息。 RandomNo用于避免浏览器缓存问题，您可以将时间戳用作随机数。

### 正在打开已提交的信件实例{#opening-submitted-letter-instance}

提交的PDF可以使用信件实例ID直接打开：

`https://[hostName]:[portNo]/[contextPath]/[letterInstanceId]`
