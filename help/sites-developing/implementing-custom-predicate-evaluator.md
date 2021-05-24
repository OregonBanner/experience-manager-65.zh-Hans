---
title: 为查询生成器实施自定义谓词计算器
seo-title: 为查询生成器实施自定义谓词计算器
description: 查询生成器提供了一种轻松的内容存储库查询方法
seo-description: 查询生成器提供了一种轻松的内容存储库查询方法
uuid: e71be518-027c-4792-9e02-06405804d9d2
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: ef253905-87da-4fa2-9f6c-778f1b12bd58
docset: aem65
exl-id: 72cbe589-14a1-40f5-a7cb-8960f02e0ebb
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '795'
ht-degree: 0%

---

# 为查询生成器{#implementing-a-custom-predicate-evaluator-for-the-query-builder}实施自定义谓词计算器

本节介绍如何通过实施自定义谓词计算器来扩展[查询生成器](/help/sites-developing/querybuilder-api.md)。

## 概述 {#overview}

[查询生成器](/help/sites-developing/querybuilder-api.md)提供了一种查询内容存储库的简单方法。 CQ附带一组谓词计算器，可帮助您处理数据。

但是，您可能希望通过实施自定义谓词计算器来简化查询，该计算器可隐藏一些复杂性并确保更好的语义。

自定义谓词还可以执行XPath无法直接执行的其他操作，例如：

* 从某些服务中查找一些数据
* 基于计算的自定义过滤

>[!NOTE]
>
>实施自定义谓词时必须考虑性能问题。

>[!NOTE]
>
>您可以在[查询生成器](/help/sites-developing/querybuilder-api.md)部分中找到查询示例。

GITHUB上的代码

您可以在GitHub上找到此页面的代码

* [在GitHub上打开aem-search-custom-predicate-evaluator项目](https://github.com/Adobe-Marketing-Cloud/aem-search-custom-predicate-evaluator)
* 将项目下载为[a ZIP文件](https://github.com/Adobe-Marketing-Cloud/aem-search-custom-predicate-evaluator/archive/master.zip)

### 详细信息{#predicate-evaluator-in-detail}中的谓词计算器

谓词计算器处理特定谓词的计算，这些谓词是查询的定义约束。

它会将更高级别的搜索约束（如“宽度> 200”）映射到符合实际内容模型(例如，元数据/@width > 200)的特定JCR查询。 或者，它可以手动筛选节点并检查其约束。

>[!NOTE]
>
>有关`PredicateEvaluator`和`com.day.cq.search`包的更多信息，请参阅[Java文档](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/search/package-summary.html)。

### 为复制元数据{#implementing-a-custom-predicate-evaluator-for-replication-metadata}实施自定义谓词计算器

例如，本节将介绍如何创建自定义谓词计算器，以帮助基于复制元数据的数据：

* `cq:lastReplicated` 用于存储上次复制操作的日期

* `cq:lastReplicatedBy` 用于存储触发上次复制操作的用户ID

* `cq:lastReplicationAction` 存储上次复制操作（例如激活、停用）

#### 使用默认谓词计算器{#querying-replication-metadata-with-default-predicate-evaluators}查询复制元数据

以下查询将获取自年初以来由`admin`激活的`/content`分支中的节点列表。

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

此查询有效，但很难读取，并且不会突出显示三个复制属性之间的关系。 实施自定义谓词计算器将降低此查询的复杂性并提高其语义。

#### 目标 {#objectives}

`ReplicationPredicateEvaluator`的目标是使用以下语法支持上述查询。

```xml
path=/content

replic.by=admin
replic.since=2013-01-01T00:00:00.000+01:00
replic.action=Activate
```

使用自定义谓词计算器对复制元数据谓词进行分组有助于创建有意义的查询。

#### 更新Maven依赖项{#updating-maven-dependencies}

>[!NOTE]
>
>[如何使用Apache Maven](/help/sites-developing/ht-projects-maven.md)构建AEM项目中介绍了使用Maven的新AEM项目的设置。

首先，您需要更新项目的Maven依赖项。 `PredicateEvaluator`是`cq-search`项目的一部分，因此需要将其添加到Maven pom文件中。

>[!NOTE]
>
>`cq-search`依赖项的范围设置为`provided`，因为`cq-search`容器将提供`OSGi`。

pom.xml

以下代码片段以[unified diff format](https://en.wikipedia.org/wiki/Diff#Unified_format)的形式显示了差异

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

[aem-search-custom-predice-evaluator](https://github.com/Adobe-Marketing-Cloud/aem-search-custom-predicate-evaluator) -  [pom.xml](https://github.com/Adobe-Marketing-Cloud/aem-search-custom-predicate-evaluator/raw/7aed6b35b4c8dd3655296e1b10cf40c0dd1eaa61/pom.xml)

#### 编写ReplicationPredicateEvaluator {#writing-the-replicationpredicateevaluator}

`cq-search`项目包含`AbstractPredicateEvaluator`抽象类。 可通过以下步骤来扩展该函数，以实施您自己的自定义谓词计算器`(PredicateEvaluator`。

>[!NOTE]
>
>以下过程说明如何构建`Xpath`表达式以过滤数据。 另一个选项是实施`includes`方法，该方法可逐行选择数据。 有关更多信息，请参阅[Java文档](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/eval/PredicateEvaluator.html#includes28comdaycqsearchpredicatejavaxjcrqueryrowcomdaycqsearchevalevaluationcontext29)。

1. 创建扩展`com.day.cq.search.eval.AbstractPredicateEvaluator`的新Java类
1. 使用`@Component`之类的对类进行注释，如下所示

   src/main/java/com/adobe/aem/docs/search/ReplicationPredicateEvaluator.java

   以下代码片段以[unified diff format](https://en.wikipedia.org/wiki/Diff#Unified_format)的形式显示了差异

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

[aem-search-custom-predice-evaluator](https://github.com/Adobe-Marketing-Cloud/aem-search-custom-predicate-evaluator) -  [src/main/java/com/adobe/aem/docs/search/ReplicationPredicateEvaluator.java](https://github.com/Adobe-Marketing-Cloud/aem-search-custom-predicate-evaluator/raw/ec70fac35fbd0d132e00c6066a204804e9cbe70f/src/main/java/com/adobe/aem/docs/search/ReplicationPredicateEvaluator.java)

>[!NOTE]
>
>`factory`必须是以`com.day.cq.search.eval.PredicateEvaluator/`开头并以自定义`PredicateEvaluator`名称结尾的唯一字符串。

>[!NOTE]
>
>`PredicateEvaluator`的名称是谓词名称，用于生成查询。

1. 替代:

   ```java
   public String getXPathExpression(Predicate predicate, EvaluationContext context)
   ```

   在覆盖方法中，您可以根据参数中给定的`Predicate`构建`Xpath`表达式。

### 复制元数据的自定义谓词计算器示例{#example-of-a-custom-predicate-evalutor-for-replication-metadata}

此`PredicateEvaluator`的完整实现可能类似于以下类。

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

[aem-search-custom-predice-evaluator](https://github.com/Adobe-Marketing-Cloud/aem-search-custom-predicate-evaluator) -  [src/main/java/com/adobe/aem/docs/search/ReplicationPredicateEvaluator.java](https://github.com/Adobe-Marketing-Cloud/aem-search-custom-predicate-evaluator/blob/master/src/main/java/com/adobe/aem/docs/search/ReplicationPredicateEvaluator.java)
