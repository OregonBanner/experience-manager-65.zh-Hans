---
title: 为Query builder实施自定义谓词计算器
seo-title: 为Query builder实施自定义谓词计算器
description: Query builder提供了一种轻松的内容存储库查询方法
seo-description: Query builder提供了一种轻松的内容存储库查询方法
uuid: e71be518-027c-4792-9e02-06405804d9d2
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: ef253905-87da-4fa2-9f6c-778f1b12bd58
docset: aem65
translation-type: tm+mt
source-git-commit: ec528e115f3e050e4124b5c232063721eaed8df5

---


# 为Query builder实施自定义谓词计算器{#implementing-a-custom-predicate-evaluator-for-the-query-builder}

本节介绍如何通过实现自定 [义谓词求值器来扩展Query Builder](/help/sites-developing/querybuilder-api.md) 。

## 概述 {#overview}

Query [Builder](/help/sites-developing/querybuilder-api.md) 提供了一种轻松的内容存储库查询方式。 CQ附带一组谓词计算器，可帮助您处理数据。

但是，您可能希望通过实现自定义谓词求值器来简化查询，它隐藏了某些复杂性并确保了更好的语义。

自定义谓词还可以执行XPath不能直接实现的其他操作，例如：

* 从某些服务中查找一些数据
* 基于计算的自定义过滤

>[!NOTE]
>
>实施自定义谓词时必须考虑性能问题。

>[!NOTE]
>
>您可以在 [Query Builder部分中查找查询示例](/help/sites-developing/querybuilder-api.md) 。

GITHUB上的代码

您可以在GitHub上找到此页面的代码

* [在GitHub上打开aem-search-custom-predicate-evaluator项目](https://github.com/Adobe-Marketing-Cloud/aem-search-custom-predicate-evaluator)
* 将项目下载为 [ZIP文件](https://github.com/Adobe-Marketing-Cloud/aem-search-custom-predicate-evaluator/archive/master.zip)

### 详细的谓词计算器 {#predicate-evaluator-in-detail}

谓词计算器处理特定谓词的计算，这些谓词是查询的定义约束。

它将更高级别的搜索约束（如“宽度> 200”）映射到符合实际内容模型的特定JCR查询（例如，元数据/@width > 200）。 或者，它可以手动过滤节点并检查其约束。

>[!NOTE]
>
>有关该和包的更 `PredicateEvaluator` 多信息， `com.day.cq.search` 请参阅 [Java文档](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/search/package-summary.html)。

### 为复制元数据实施自定义谓词计算器 {#implementing-a-custom-predicate-evaluator-for-replication-metadata}

作为示例，本节介绍如何创建自定义谓词求值器，以帮助根据复制元数据生成数据：

* `cq:lastReplicated` 存储上次复制操作的日期

* `cq:lastReplicatedBy` 存储触发上次复制操作的用户的ID

* `cq:lastReplicationAction` 存储上次复制操作（例如，激活、取消激活）

#### 使用默认谓词计算器查询复制元数据 {#querying-replication-metadata-with-default-predicate-evaluators}

以下查询获取分支中自年 `/content` 初以来已激活 `admin` 的节点的列表。

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

此查询有效但难以读取，并且不会突出显示三个复制属性之间的关系。 实现自定义谓词求值器将降低查询的复杂度，提高查询的语义。

#### 目标 {#objectives}

其目标是使 `ReplicationPredicateEvaluator` 用以下语法支持上述查询。

```xml
path=/content

replic.by=admin
replic.since=2013-01-01T00:00:00.000+01:00
replic.action=Activate
```

使用自定义谓词计算器将复制元数据谓词分组有助于创建有意义的查询。

#### 更新Maven依赖关系 {#updating-maven-dependencies}

>[!NOTE]
>
>如何使用Apache Maven构建AEM项目，介绍了使用maven [设置新的AEM项目的过程](/help/sites-developing/ht-projects-maven.md)。

首先，您需要更新项目的Maven依赖关系。 这 `PredicateEvaluator` 是藏物的一 `cq-search` 部分，因此它需要添加到您的Maven pom文件。

>[!NOTE]
>
>依赖关系的范 `cq-search` 围设置为，因 `provided` 为 `cq-search` 将由容器提供 `OSGi` 。

pom.xml

以下代码片断以统一的差异格式 [显示差异](https://en.wikipedia.org/wiki/Diff#Unified_format)

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

#### 编写ReplicationPredicateValuator {#writing-the-replicationpredicateevaluator}

项 `cq-search` 目包含抽 `AbstractPredicateEvaluator` 象类。 只需几个步骤即可扩展该功能，以实现您自己的自定义谓词计算 `(PredicateEvaluator`器)。

>[!NOTE]
>
>下面的过程介绍如何构建用于过 `Xpath` 滤数据的表达式。 另一个选项是实现按 `includes` 行选择数据的方法。 See the [Java documentation](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/eval/PredicateEvaluator.html#includes28comdaycqsearchpredicatejavaxjcrqueryrowcomdaycqsearchevalevaluationcontext29) for more information.

1. 创建新的Java类，它扩展了 `com.day.cq.search.eval.AbstractPredicateEvaluator`
1. 使用类似以下内容 `@Component` 为您的类添加注释

   src/main/java/com/adobe/aem/docs/search/ReplicationPredicateEvaluator.java

   以下代码片断以统一的差异格式 [显示差异](https://en.wikipedia.org/wiki/Diff#Unified_format)

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
>该字 `factory`符串必须是以自定义 `com.day.cq.search.eval.PredicateEvaluator/`名称开头并以其结尾的唯一字符串 `PredicateEvaluator`。

>[!NOTE]
>
>谓词名称是 `PredicateEvaluator` 构建查询时使用的谓词名称。

1. 覆盖：

   ```java
   public String getXPathExpression(Predicate predicate, EvaluationContext context)
   ```

   在覆盖方法中，您将基于 `Xpath` 参数中给定的 `Predicate` 表达式构建表达式。

### 复制元数据的自定义谓词评估器示例 {#example-of-a-custom-predicate-evalutor-for-replication-metadata}

此功能的完整实 `PredicateEvaluator` 现可能与以下类类似。

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
 *      http://www.apache.org/licenses/LICENSE-2.0
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
