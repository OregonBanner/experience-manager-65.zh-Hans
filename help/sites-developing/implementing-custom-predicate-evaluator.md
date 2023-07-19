---
title: 为查询生成器实施自定义谓词计算器
seo-title: Implementing a Custom Predicate Evaluator for the Query Builder
description: 查询生成器提供了一种查询内容存储库的简单方法
seo-description: The Query Builder offers an easy way of querying the content repository
uuid: e71be518-027c-4792-9e02-06405804d9d2
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: ef253905-87da-4fa2-9f6c-778f1b12bd58
docset: aem65
exl-id: 72cbe589-14a1-40f5-a7cb-8960f02e0ebb
source-git-commit: 259f257964829b65bb71b5a46583997581a91a4e
workflow-type: tm+mt
source-wordcount: '776'
ht-degree: 0%

---

# 为查询生成器实施自定义谓词计算器{#implementing-a-custom-predicate-evaluator-for-the-query-builder}

本节介绍如何扩展 [查询生成器](/help/sites-developing/querybuilder-api.md) 实现自定义谓词求值器。

## 概述 {#overview}

此 [查询生成器](/help/sites-developing/querybuilder-api.md) 提供了一种查询内容存储库的简单方法。 CQ附带了一组谓词评估器，可帮助您处理数据。

但是，您可能希望通过实施自定义谓词计算器来简化查询，该计算器可隐藏一些复杂性并确保更好的语义。

自定义谓词还可以执行使用XPath无法直接执行的其他操作，例如：

* 从某个服务中查找一些数据
* 基于计算的自定义筛选

>[!NOTE]
>
>实施自定义谓词时必须考虑性能问题。

>[!NOTE]
>
>您可以在以下位置找到查询示例 [查询生成器](/help/sites-developing/querybuilder-api.md) 部分。

GITHUB上的代码

您可以在GitHub上找到此页面的代码

* [在GitHub上打开aem-search-custom-predicate-evaluator项目](https://github.com/Adobe-Marketing-Cloud/aem-search-custom-predicate-evaluator)
* 将项目下载为 [ZIP文件](https://github.com/Adobe-Marketing-Cloud/aem-search-custom-predicate-evaluator/archive/master.zip)

### 谓词计算器详细信息 {#predicate-evaluator-in-detail}

谓词计算器处理某些谓词的计算，这些谓词是查询的定义约束。

它将更高级别的搜索限制（例如“宽度> 200”）映射到适合实际内容模型(例如，元数据/@width > 200)的特定JCR查询。 或者，它可以手动筛选节点并检查其约束。

>[!NOTE]
>
>欲知关于 `PredicateEvaluator` 和 `com.day.cq.search` 包请参阅 [Java文档](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/search/package-summary.html).

### 实施复制元数据的自定义谓词求值器 {#implementing-a-custom-predicate-evaluator-for-replication-metadata}

作为示例，本节将介绍如何创建自定义谓词计算器，以帮助基于复制元数据的数据：

* `cq:lastReplicated` 存储上次复制操作的日期

* `cq:lastReplicatedBy` 用于存储触发上次复制操作的用户的id

* `cq:lastReplicationAction` 用于存储上次的复制操作（例如，激活、停用）

#### 使用默认谓词求值器查询复制元数据 {#querying-replication-metadata-with-default-predicate-evaluators}

以下查询获取中的节点列表 `/content` 已由激活的分支 `admin` 从年初开始。

```xml
path=/content

1_property=cq:lastReplicatedBy
1_property.value=admin

2_property=cq:lastReplicationAction
2_property.value=Activate

daterange.property=cq:lastReplicated
daterange.lowerBound=2013-01-01T00:00:00.000+01:00
daterange.lowerOperation=>=
```

此查询有效，但难以读取，并且不会突出显示三个复制属性之间的关系。 实施自定义谓词求值器将降低此查询的复杂性并提高其语义。

#### 目标 {#objectives}

的目标 `ReplicationPredicateEvaluator` ，以使用以下语法支持上述查询。

```xml
path=/content

replic.by=admin
replic.since=2013-01-01T00:00:00.000+01:00
replic.action=Activate
```

使用自定义谓词计算器将复制元数据谓词分组有助于创建有意义的查询。

#### 更新Maven依赖项 {#updating-maven-dependencies}

>[!NOTE]
>
>以下文档介绍了使用maven设置新的AEM项目 [如何使用Apache Maven构建AEM项目](/help/sites-developing/ht-projects-maven.md).

首先，您需要更新项目的Maven依赖项。 此 `PredicateEvaluator` 是 `cq-search` 工件，因此需要将其添加到您的Maven pom文件中。

>[!NOTE]
>
>范围 `cq-search` 依赖关系设置为 `provided` 因为 `cq-search` 将由 `OSGi` 容器。

pom.xml

以下代码片段显示了两者在 [统一差异格式](https://en.wikipedia.org/wiki/Diff#Unified_format)

```
@@ -120,6 +120,12 @@
             <scope>provided</scope>
         <dependency>
+            <groupid>com.day.cq</groupid>
+            <artifactid>cq-search</artifactid>
+            <version>5.6.4</version>
+            <scope>provided</scope>
+        </dependency>
+        <dependency>
             <groupid>junit</groupid>
             <artifactid>junit</artifactid>
             <version>3.8.1</version></dependency>
```

[aem-search-custom-predicate-evaluator](https://github.com/Adobe-Marketing-Cloud/aem-search-custom-predicate-evaluator)- [pom.xml](https://github.com/Adobe-Marketing-Cloud/aem-search-custom-predicate-evaluator/raw/7aed6b35b4c8dd3655296e1b10cf40c0dd1eaa61/pom.xml)

#### 编写ReplicationPredicateEvaluator {#writing-the-replicationpredicateevaluator}

此 `cq-search` 项目包含 `AbstractPredicateEvaluator` 抽象类。 只需几个步骤即可扩展此功能以实施您自己的自定义谓词计算器 `(PredicateEvaluator`)。

>[!NOTE]
>
>以下过程说明如何构建 `Xpath` 用于筛选数据的表达式。 另一种选择是实施 `includes` 逐行选择数据的方法。 请参阅 [Java文档](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/eval/PredicateEvaluator.html#includes28comdaycqsearchpredicatejavaxjcrqueryrowcomdaycqsearchevalevaluationcontext29) 了解更多信息。

1. 创建扩展的Java类 `com.day.cq.search.eval.AbstractPredicateEvaluator`
1. 使用为课程添加批注 `@Component` 如下所示

   src/main/java/com/adobe/aem/docs/search/ReplicationPredicateEvaluator.java

   以下代码片段显示了两者在 [统一差异格式](https://en.wikipedia.org/wiki/Diff#Unified_format)

```
@@ -19,8 +19,11 @@
  */
 package com.adobe.aem.docs.search;

+import org.apache.felix.scr.annotations.Component;
+
 import com.day.cq.search.eval.AbstractPredicateEvaluator;

+@Component(metatype = false, factory = "com.day.cq.search.eval.PredicateEvaluator/repli")
 public class ReplicationPredicateEvaluator extends AbstractPredicateEvaluator {

 }
```

[aem-search-custom-predicate-evaluator](https://github.com/Adobe-Marketing-Cloud/aem-search-custom-predicate-evaluator)- [src/main/java/com/adobe/aem/docs/search/ReplicationPredicateEvaluator.java](https://github.com/Adobe-Marketing-Cloud/aem-search-custom-predicate-evaluator/raw/ec70fac35fbd0d132e00c6066a204804e9cbe70f/src/main/java/com/adobe/aem/docs/search/ReplicationPredicateEvaluator.java)

>[!NOTE]
>
>此 `factory`必须为以开头的唯一字符串 `com.day.cq.search.eval.PredicateEvaluator/`并以您的自定义名称结尾 `PredicateEvaluator`.

>[!NOTE]
>
>的名称 `PredicateEvaluator` 是谓词名称，在构建查询时使用。

1. 替代:

   ```java
   public String getXPathExpression(Predicate predicate, EvaluationContext context)
   ```

   在覆盖方法中，您构建 `Xpath` 表达式基于 `Predicate` 在论据中给出。

### 复制元数据的自定义谓词计算器示例 {#example-of-a-custom-predicate-evalutor-for-replication-metadata}

此功能的完整实施 `PredicateEvaluator` 可能类似于以下类。

src/main/java/com/adobe/aem/docs/search/ReplicationPredicateEvaluator.java

```
/*
 * #%L
 * aem-docs-custom-predicate-evaluator
 * %%
 * Copyright (C) 2013 Adobe Research
 * %%
 * Licensed under the Apache License, Version 2.0 (the "License");
 * you may not use this file except in compliance with the License.
 * You may obtain a copy of the License at
 *
 *      https://www.apache.org/licenses/LICENSE-2.0
 *
 * Unless required by applicable law or agreed to in writing, software
 * distributed under the License is distributed on an "AS IS" BASIS,
 * WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
 * See the License for the specific language governing permissions and
 * limitations under the License.
 * #L%
 */

package com.adobe.aem.docs.search;

import org.apache.felix.scr.annotations.Component;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

import com.day.cq.search.Predicate;
import com.day.cq.search.eval.AbstractPredicateEvaluator;
import com.day.cq.search.eval.EvaluationContext;

@Component(metatype = false, factory = "com.day.cq.search.eval.PredicateEvaluator/repli")

public class ReplicationPredicateEvaluator extends AbstractPredicateEvaluator {

    static final String PE_NAME = "replic";


    static final String PN_LAST_REPLICATED_BY = "cq:lastReplicatedBy";
    static final String PN_LAST_REPLICATED = "cq:lastReplicated";
    static final String PN_LAST_REPLICATED_ACTION = "cq:lastReplicationAction";

    static final String PREDICATE_BY = "by";
    static final String PREDICATE_SINCE = "since";
    static final String PREDICATE_SINCE_OP = " >= ";
    static final String PREDICATE_ACTION = "action";

    Logger log = LoggerFactory.getLogger(getClass());

    /**
     * Returns a XPath expression filtering by replication metadata.
     *
     * @see com.day.cq.search.eval.AbstractPredicateEvaluator#getXPathExpression(com.day.cq.search.Predicate,
     *      com.day.cq.search.eval.EvaluationContext)
     */

    @Override

    public String getXPathExpression(Predicate predicate,
            EvaluationContext context) {

        log.debug("predicate {}", predicate);

        String date = predicate.get(PREDICATE_SINCE);
        String user = predicate.get(PREDICATE_BY);
        String action = predicate.get(PREDICATE_ACTION);

        StringBuilder sb = new StringBuilder();

        if (date != null) {

            sb.append(PN_LAST_REPLICATED).append(PREDICATE_SINCE_OP);
            sb.append("xs:dateTime('").append(date).append("')");

        }

        if (user != null) {

            addAndOperator(sb);
            sb.append(PN_LAST_REPLICATED_BY);
            sb.append("='").append(user).append("'");

        }

        if (action != null) {

            addAndOperator(sb);
            sb.append(PN_LAST_REPLICATED_ACTION);
            sb.append("='").append(action).append("'");

        }

        String xpath = sb.toString();

        log.debug("xpath **{}**", xpath);

        return xpath;

    }

    /**
     * Add an and operator if the builder is not empty.
     *
     * @param sb a {@link StringBuilder} containing the query under construction
     */

    private void addAndOperator(StringBuilder sb) {

        if (sb.length() != 0) {

            sb.append(" and ");

        }

    }

}
```

[aem-search-custom-predicate-evaluator](https://github.com/Adobe-Marketing-Cloud/aem-search-custom-predicate-evaluator)- [src/main/java/com/adobe/aem/docs/search/ReplicationPredicateEvaluator.java](https://github.com/Adobe-Marketing-Cloud/aem-search-custom-predicate-evaluator/blob/master/src/main/java/com/adobe/aem/docs/search/ReplicationPredicateEvaluator.java)
