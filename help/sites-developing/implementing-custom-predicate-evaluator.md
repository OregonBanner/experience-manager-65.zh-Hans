---
title: 为查询生成器实施自定义谓词计算器
description: 查询生成器提供了一种查询内容存储库的简单方法
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
docset: aem65
exl-id: 72cbe589-14a1-40f5-a7cb-8960f02e0ebb
source-git-commit: b66ec42c35b5b60804015d340b8194bbd6ef3e28
workflow-type: tm+mt
source-wordcount: '762'
ht-degree: 1%

---

# 为查询生成器实施自定义谓词计算器{#implementing-a-custom-predicate-evaluator-for-the-query-builder}

本节介绍如何扩展 [查询生成器](/help/sites-developing/querybuilder-api.md) 通过实施自定义谓词计算器。

## 概述 {#overview}

此 [查询生成器](/help/sites-developing/querybuilder-api.md) 提供了一种查询内容存储库的简单方法。 CQ附带一组谓词评估器，可帮助您处理数据。

但是，您可能希望通过实施自定义谓词计算器来简化查询，该计算器可以隐藏一些复杂性并确保更好的语义。

自定义谓词还可以执行其他不能直接使用XPath执行的操作，例如：

* 从某个服务中查找一些数据
* 基于计算的自定义筛选

>[!NOTE]
>
>实施自定义谓词时必须考虑性能问题。

>[!NOTE]
>
>您可以在以下位置找到查询示例： [查询生成器](/help/sites-developing/querybuilder-api.md) 部分。

GITHUB上的代码

您可以在 GitHub 上找到此页面的代码。

* [在GitHub上打开aem-search-custom-predicate-evaluator项目](https://github.com/Adobe-Marketing-Cloud/aem-search-custom-predicate-evaluator)
* 将项目下载为 [ZIP文件](https://github.com/Adobe-Marketing-Cloud/aem-search-custom-predicate-evaluator/archive/master.zip)

### 谓词计算器详细信息 {#predicate-evaluator-in-detail}

谓词计算器处理某些谓词的计算，这些谓词是查询的定义约束。

它将更高级别的搜索限制（例如“宽度> 200”）映射到适合实际内容模型的特定JCR查询(例如，元数据/@width > 200)。 或者，它可以手动筛选节点并检查其约束。

>[!NOTE]
>
>欲知关于 `PredicateEvaluator` 和 `com.day.cq.search` 包，请参见 [Java™文档](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/index.html?com/day/cq/search/package-summary.html).

### 为复制元数据实施自定义谓词计算器 {#implementing-a-custom-predicate-evaluator-for-replication-metadata}

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

此查询有效但难以读取，并且不会突出显示三个复制属性之间的关系。 实施自定义谓词计算器可降低复杂性并改善此查询的语义。

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
以下文档介绍了使用maven设置新的Adobe Experience Manager (AEM)项目 [如何使用Apache Maven构建AEM项目](/help/sites-developing/ht-projects-maven.md).

首先，更新项目的Maven依赖项。 此 `PredicateEvaluator` 是 `cq-search` 构件，因此必须将其添加到Maven pom.xml文件中。

>[!NOTE]
>
范围 `cq-search` 依赖关系设置为 `provided` 因为 `cq-search` 由 `OSGi` 容器。

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

[aem-search-custom-predicate-evaluator](https://github.com/Adobe-Marketing-Cloud/aem-search-custom-predicate-evaluator) - [pom.xml](https://raw.githubusercontent.com/Adobe-Marketing-Cloud/aem-search-custom-predicate-evaluator/7aed6b35b4c8dd3655296e1b10cf40c0dd1eaa61/pom.xml)

#### 编写ReplicationPredicateEvaluator {#writing-the-replicationpredicateevaluator}

此 `cq-search` 项目包含 `AbstractPredicateEvaluator` 抽象类。 只需几个步骤即可扩展此功能以实施您自己的自定义谓词计算器 `(PredicateEvaluator`)。

>[!NOTE]
>
以下过程说明如何构建 `Xpath` 用于筛选数据的表达式。 另一种选择是实施 `includes` 逐行选择数据的方法。 请参阅 [Java™文档](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/search/eval/PredicateEvaluator.html#includes28comdaycqsearchpredicatejavaxjcrqueryrowcomdaycqsearchevalevaluationcontext29) 以了解更多信息。

1. 创建扩展的Java™类 `com.day.cq.search.eval.AbstractPredicateEvaluator`
1. 使用为类添加批注 `@Component` 如下所示

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

[aem-search-custom-predicate-evaluator](https://github.com/Adobe-Marketing-Cloud/aem-search-custom-predicate-evaluator) - [src/main/java/com/adobe/aem/docs/search/ReplicationPredicateEvaluator.java](https://raw.githubusercontent.com/Adobe-Marketing-Cloud/aem-search-custom-predicate-evaluator/ec70fac35fbd0d132e00c6066a204804e9cbe70f/src/main/java/com/adobe/aem/docs/search/ReplicationPredicateEvaluator.java)

>[!NOTE]
>
此 `factory`必须为以开头的唯一字符串 `com.day.cq.search.eval.PredicateEvaluator/`并以您的自定义名称结尾 `PredicateEvaluator`.

>[!NOTE]
>
的名称 `PredicateEvaluator` 是构建查询时使用的谓词名称。

1. 替代:

   ```java
   public String getXPathExpression(Predicate predicate, EvaluationContext context)
   ```

   在覆盖方法中，您构建 `Xpath` 表达式基于 `Predicate` 在论证中给出。

### 复制元数据的自定义谓词计算器示例 {#example-of-a-custom-predicate-evalutor-for-replication-metadata}

此的完整实施 `PredicateEvaluator` 可能与以下类类似。

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

[aem-search-custom-predicate-evaluator](https://github.com/Adobe-Marketing-Cloud/aem-search-custom-predicate-evaluator) - [src/main/java/com/adobe/aem/docs/search/ReplicationPredicateEvaluator.java](https://github.com/Adobe-Marketing-Cloud/aem-search-custom-predicate-evaluator/blob/master/src/main/java/com/adobe/aem/docs/search/ReplicationPredicateEvaluator.java)
