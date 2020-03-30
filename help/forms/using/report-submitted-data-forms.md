---
title: 用于在表单门户上处理提交表单的API
seo-title: 用于在表单门户上处理提交表单的API
description: AEM Forms提供了API，您可以使用这些API在表单门户中查询提交的表单数据并对其执行操作。
seo-description: AEM Forms提供了API，您可以使用这些API在表单门户中查询提交的表单数据并对其执行操作。
uuid: c47c8392-e5a9-4c40-b65e-4a7f379a6b45
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: developer-reference
discoiquuid: 9457effd-3595-452f-a976-ad9eda6dc909
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f

---


# 用于在表单门户上处理提交表单的API {#apis-to-work-with-submitted-forms-on-forms-portal}

AEM Forms提供了API，您可以使用它来查询通过表单门户提交的表单数据。 此外，您还可以使用本文档中介绍的API发布注释或更新已提交表单的属性。

>[!NOTE]
>
>将调用API的用户必须添加到审阅者组，如将提交审阅者关 [联到表单中所述](/help/forms/using/adding-reviewers-form.md)。

## GET /content/forms/portal/submission.review.json?func=getFormsForSubmissionReview {#get-content-forms-portal-submission-review-json-func-getformsforsubmissionreview-br}

返回所有合格表单的列表。

### URL parameters {#url-parameters}

此API不需要其他参数。

### 响应 {#response}

响应对象包含一个JSON数组，其中包含表单名称及其存储库路径。 响应的结构如下：

```
[
 {formName: "<form name>",
 formPath: "<path to the form>" },
 {.....},
 ......]
```

### 示例 {#example}

**请求URL**

```
https://[host]:[port]/content/forms/portal/submission.review.json?func=getFormsForSubmissionReview
```

**响应**

```java
[{"formPath":"/content/dam/formsanddocuments/forms-review/form2","formName":"form2"},{"formPath":"/content/dam/formsanddocuments/forms-review/form1","formName":"form1"}]
```

## GET /content/forms/portal/submission.review.json?func=getAllSubmissions {#get-content-forms-portal-submission-review-json-func-getallsubmissions}

返回所有已提交表单的详细信息。 但是，可以使用URL参数限制结果。

### URL parameters {#url-parameters-1}

在请求URL中指定以下参数：

<table>
 <tbody>
  <tr>
   <th>参数</th>
   <th>描述</th>
  </tr>
  <tr>
   <td><code>formPath</code></td>
   <td>指定表单所在的CRX存储库路径。 如果不指定表单路径，则返回空响应。<br /> </td>
  </tr>
  <tr>
   <td><code>offset</code> （可选）</td>
   <td>在结果集的索引中指定起始点。 The default value is <strong>0</strong>.</td>
  </tr>
  <tr>
   <td><code>limit</code> （可选）</td>
   <td>限制结果数。 The default value is <strong>30</strong>.</td>
  </tr>
  <tr>
   <td><code>orderby</code> <br /> （可选）</td>
   <td>指定结果排序的属性。 默认值为 <strong>jcr:lastModified</strong>，它根据上次修改时间对结果排序。</td>
  </tr>
  <tr>
   <td><code>sort</code> <br /> （可选）</td>
   <td>指定结果排序的顺序。 默认值为desc <strong></strong>，它按降序排序结果。 您可以指定 <code>asc</code> 按升序对结果排序。</td>
  </tr>
  <tr>
   <td><code>cutPoints</code> <br /> （可选）</td>
   <td>指定要包含在结果中的表单属性的逗号分隔列表。 默认属性为：<br /><code>formName</code>, <code>formPath</code><code>submitID</code>, <code>formType</code>, <code>jcr:lastModified</code>, <code>owner</code></td>
  </tr>
  <tr>
   <td><code>search</code> <br /> （可选）</td>
   <td>在表单属性中搜索指定值并返回具有匹配值的表单。 默认值为 <strong>""</strong>.</td>
  </tr>
 </tbody>
</table>

### 响应 {#response-1}

响应对象包含一个JSON数组，其中包含指定表单的详细信息。 响应的结构如下：

```
{
 total: "<total number of submissions>",
 items: [{ formName: "<name of the form>", formPath: "<path to the form>", owner: "<owner of the form>"},
 ....]}
```

### 示例 {#example-1}

**请求URL**

```
https://[host]:[port]/content/forms/portal/submission.review.json?func=getAllSubmissions&formPath=/content/dam/formsanddocuments/forms-review/form2
```

**响应**

```java
{"total":1,"items":[{"formName":"form2","formPath":"/content/dam/formsanddocuments/forms-review/form2","submitID":"1403037413508500","formType":"af","jcr:lastModified":"2015-11-05T17:52:32.243+05:30","owner":"admin"}]}
```

## POST /content/forms/portal/submission.review.json?func=addComment {#post-content-forms-portal-submission-review-json-func-addcomment-br}

向指定的提交实例添加注释。

### URL parameters {#url-parameters-2}

在请求URL中指定以下参数：

| 参数 | 描述 |
|---|---|
| `submitID` | 指定与提交实例关联的元数据ID。 |
| `Comment` | 指定要添加到指定提交实例的注释文本。 |

### 响应 {#response-2}

在成功发布评论时返回评论ID。

### 示例 {#example-2}

**请求URL**

```
https://[host:'port'/content/forms/portal/submission.review.json?func=addComment&submitID=1403037413508500&comment=API+test+comment
```

**响应**

```java
1403873422601300
```

## GET /content/forms/portal/submission.review.json?func=getComments {#get-content-forms-portal-submission-review-json-func-getcomments-nbsp}

返回在指定的提交实例上发布的所有注释。

### URL parameters {#url-parameters-3}

在请求URL中指定以下参数：

| 参数 | 描述 |
|---|---|
| `submitID` | 指定提交实例的元数据ID。 |

### 响应 {#response-3}

响应对象包含一个JSON数组，该数组包含与指定的提交ID关联的所有注释。 响应的结构如下：

```
[{
 owner: "<name of the commenter>",
 comment: "<comment text>",
 time: "<time when the comment was posted>"},
 { }......]
```

### 示例 {#example-3}

**请求URL**

```
https://[host]:'port'/content/forms/portal/submission.review.json?func=getComments&submitID=1403037413508500
```

**响应**

```java
[{"owner":"fr1","comment":"API test comment","time":1446726988250}]
```

## POST /content/forms/portal/submission.review.json?func=updateSubmission {#post-content-forms-portal-submission-review-json-func-updatesubmission-br}

更新指定提交的表单实例的指定属性的值。

### URL parameters {#url-parameters-4}

在请求URL中指定以下参数：

| 参数 | 描述 |
|---|---|
| `submitID` | 指定与提交实例关联的元数据ID。 |
| `property` | 指定要更新的表单属性。 |
| `value` | 指定要更新的表单属性的值。 |

### 响应 {#response-4}

返回一个JSON对象，其中包含已发布更新的相关信息。

### 示例 {#example-4}

**请求URL**

```
https://[host]:'port'/content/forms/portal/submission.review.json?func=updateSubmission&submitID=1403037413508500&value=sample_value&property=some_new_prop
```

**响应**

```java
{"formName":"form2","owner":"admin","jcr:lastModified":1446727516593,"path":"/content/forms/fp/admin/submit/metadata/1403037413508500.html","submitID":"1403037413508500","status":"submitted"}
```

