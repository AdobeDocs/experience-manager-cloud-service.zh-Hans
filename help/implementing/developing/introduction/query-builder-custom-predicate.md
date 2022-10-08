---
title: 为查询生成器实施自定义谓词计算器
description: AEM中的查询生成器提供了一种简单且可自定义的方式来查询内容存储库
exl-id: 8c2f8c22-1851-4313-a1c9-10d6d9b65824
source-git-commit: ca849bd76e5ac40bc76cf497619a82b238d898fa
workflow-type: tm+mt
source-wordcount: '669'
ht-degree: 0%

---

# 为查询生成器实施自定义谓词计算器 {#implementing-a-custom-predicate-evaluator-for-the-query-builder}

本文档介绍如何扩展 [查询生成器](query-builder-api.md) 通过实施自定义谓词计算器。

## 概述 {#overview}

的 [查询生成器](query-builder-api.md) 提供了一种查询内容存储库的简单方法。 AEM附带 [一组谓词评估器](#query-builder-predicates.md) 以帮助您查询数据。

但是，您可能希望通过实施自定义谓词计算器来简化查询，该计算器可隐藏一些复杂性并确保更好的语义。

自定义谓词还可以执行XPath无法直接执行的其他操作，例如：

* 从其他服务查询数据
* 基于计算的自定义过滤

>[!NOTE]
>
>实施自定义谓词时必须考虑性能问题。

>[!TIP]
>
>您可以在 [查询生成器](query-builder-api.md) 文档。

>[!TIP]
>
>您可以在GitHub上找到此页面的代码
>
>* [在GitHub上打开aem-search-custom-predicate-evaluator项目](https://github.com/Adobe-Marketing-Cloud/aem-search-custom-predicate-evaluator)
>* 将项目下载为 [ZIP文件](https://github.com/Adobe-Marketing-Cloud/aem-search-custom-predicate-evaluator/archive/master.zip)


>[!NOTE]
>
>GitHub上的此链接代码和本文档中的代码片段仅供演示之用。

### 谓词计算器（详情） {#predicate-evaluator-in-detail}

谓词计算器处理特定谓词的计算，这些谓词是查询的定义约束。

它会映射更高级别的搜索约束(例如 `width>200`)到符合实际内容模型的特定JCR查询(例如， `metadata/@width > 200`)。 或者，它可以手动筛选节点并检查其约束。

>[!TIP]
>
>有关 `PredicateEvaluator` 和 `com.day.cq.search` 包请参阅 [Java文档](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/index.html?com/day/cq/search/package-summary.html).

### 为复制元数据实施自定义谓词计算器 {#implementing-a-custom-predicate-evaluator-for-replication-metadata}

例如，本节将介绍如何创建自定义谓词计算器，以帮助基于复制元数据的数据：

* `cq:lastReplicated` 用于存储上次复制操作的日期
* `cq:lastReplicatedBy` 用于存储触发上次复制操作的用户ID
* `cq:lastReplicationAction` 存储上次复制操作（例如，激活、停用）

#### 使用默认谓词计算器查询复制元数据 {#querying-replication-metadata-with-default-predicate-evaluators}

以下查询将获取 `/content` 已激活的分支 `admin` 从年初开始。

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

目标 `ReplicationPredicateEvaluator` 使用以下语法支持上述查询。

```xml
path=/content

replic.by=admin
replic.since=2013-01-01T00:00:00.000+01:00
replic.action=Activate
```

使用自定义谓词计算器对复制元数据谓词进行分组有助于创建有意义的查询。

#### 更新Maven依赖项 {#updating-maven-dependencies}

>[!TIP]
>
>新的AEM项目（包括使用maven）的设置详见 [WKND教程。](develop-wknd-tutorial.md)

首先，您需要更新项目的Maven依赖项。 的 `PredicateEvaluator` 是 `cq-search` 项目，因此需要将其添加到Maven pom文件中。

>[!NOTE]
>
>的范围 `cq-search` 依赖关系设置为 `provided` 因为 `cq-search` 将由 `OSGi` 容器。

以下代码片段显示了 `pom.xml` 文件，在 [统一差异格式](https://en.wikipedia.org/wiki/Diff#Unified_format)

```text
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

#### 编写ReplicationPredicateEvaluator {#writing-the-replicationpredicateevaluator}

的 `cq-search` 项目包含 `AbstractPredicateEvaluator` 抽象类。 可以通过以下步骤来扩展此功能，以实施您自己的自定义谓词计算器 `(PredicateEvaluator`)。

>[!NOTE]
>
>以下过程说明如何构建 `Xpath` 过滤数据的表达式。 另一种选择是实施 `includes` 方法。 请参阅 [Java文档](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/search/eval/PredicateEvaluator.html) 以了解更多信息。

1. 创建新的Java类，该类扩展 `com.day.cq.search.eval.AbstractPredicateEvaluator`
1. 使用 `@Component` 与 [统一差异格式](https://en.wikipedia.org/wiki/Diff#Unified_format)

   ```text
   @@ -19,8 +19,11 @@
     */
    package com.adobe.aem.docs.search;
   
   +import org.apache.felix.scr.annotations.Component;
   +import com.day.cq.search.eval.AbstractPredicateEvaluator;
   
   +@Component(metatype = false, factory = "com.day.cq.search.eval.PredicateEvaluator/repli")
    public class ReplicationPredicateEvaluator extends AbstractPredicateEvaluator {
   
    }
   ```

   >[!NOTE]
   >
   >的 `factory`必须是以开头的唯一字符串 `com.day.cq.search.eval.PredicateEvaluator/`并以自定义名称结尾 `PredicateEvaluator`.

   >[!NOTE]
   >
   >的名称 `PredicateEvaluator` 是谓词名称，用于生成查询。

1. 替代:

   ```java
   public String getXPathExpression(Predicate predicate, EvaluationContext context)
   ```

   在覆盖方法中，您生成 `Xpath` 基于的表达式 `Predicate` 在论据中给出。

### 复制元数据的自定义谓词计算器示例 {#example-of-a-custom-predicate-evaluator-for-replication-metadata}

此功能的完整实施 `PredicateEvaluator` 可能与以下类类似。

```java
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
