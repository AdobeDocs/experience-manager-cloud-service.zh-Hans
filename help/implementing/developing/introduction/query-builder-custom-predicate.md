---
title: 为查询 Builder实施自定义谓词计算器
description: AEM中的查询 Builder优惠了一种轻松、可自定义的查询内容存储库的方式
translation-type: tm+mt
source-git-commit: 6b754a866be7979984d613b95a6137104be05399
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# 为查询 Builder {#implementing-a-custom-predicate-evaluator-for-the-query-builder}实施自定义谓词计算器

本文档介绍如何通过实现自定义谓词计算器来扩展[查询生成器](query-builder-api.md)。

## 概述 {#overview}

[查询 Builder](query-builder-api.md)优惠一种轻松的内容存储库查询方式。 AEM附带有一组[谓词计算器](#query-builder-predicates.md)，可帮助您查询数据。

但是，您可能希望通过实现隐藏某些复杂性并确保更好的语义的自定义谓词计算器来简化查询。

自定义谓词还可以执行XPath无法直接执行的其他操作，例如：

* 从其他服务查询数据
* 基于计算的自定义过滤

>[!NOTE]
>
>实施自定义谓词时必须考虑性能问题。

>[!TIP]
>
>您可以在[查询生成器](query-builder-api.md)文档中找到查询示例。

>[!TIP]
>
>您可以在GitHub上找到此页面的代码
>
>* [在GitHub上打开aem-search-custom-predicate-evaluator项目](https://github.com/Adobe-Marketing-Cloud/aem-search-custom-predicate-evaluator)
>* 将项目下载为[ZIP文件](https://github.com/Adobe-Marketing-Cloud/aem-search-custom-predicate-evaluator/archive/master.zip)


>[!NOTE]
>
>此链接的GitHub代码和此文档中的代码片段仅供演示之用。

### 详细信息{#predicate-evaluator-in-detail}中的谓词计算器

谓词计算器处理特定谓词的计算，这些谓词是查询的定义约束。

它将更高级别的搜索约束（如`width>200`）映射到符合实际内容模型(如`metadata/@width > 200`)。 也可以手动过滤节点并检查其约束。

>[!TIP]
>
>有关`PredicateEvaluator`和`com.day.cq.search`包的详细信息，请参阅[Java文档](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/index.html?com/day/cq/search/package-summary.html)。

### 为复制元数据{#implementing-a-custom-predicate-evaluator-for-replication-metadata}实施自定义谓词计算器

例如，本节介绍如何创建自定义谓词计算器，以帮助基于复制元数据的数据：

* `cq:lastReplicated` 存储上次复制操作的日期
* `cq:lastReplicatedBy` 存储触发上次复制操作的用户的id
* `cq:lastReplicationAction` 存储上次复制操作(例如激活、取消激活)

#### 使用默认谓词计算器{#querying-replication-metadata-with-default-predicate-evaluators}查询复制元数据

以下查询获取自年初起由`admin`激活的`/content`分支中节点的列表。

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

此查询有效但难以读取，不会突出显示三个复制属性之间的关系。 实现自定义谓词求值器将降低该查询的复杂性和语义。

#### 目标{#objectives}

`ReplicationPredicateEvaluator`的目标是使用以下语法支持上述查询。

```xml
path=/content

replic.by=admin
replic.since=2013-01-01T00:00:00.000+01:00
replic.action=Activate
```

使用自定义谓词计算器将复制元数据谓词分组有助于创建有意义的查询。

#### 更新Maven依赖项{#updating-maven-dependencies}

>[!TIP]
>
>WKND教程](develop-wknd-tutorial.md)中详细说明了包括使用maven在内的新AEM项目的设置。[

首先，您需要更新项目的Maven依赖项。 `PredicateEvaluator`是`cq-search`项目的一部分，因此需要将它添加到Maven pom文件。

>[!NOTE]
>
>`cq-search`依赖关系的范围设置为`provided`，因为`cq-search`将由`OSGi`容器提供。

以下代码片断显示了`pom.xml`文件中以[统一diff格式](https://en.wikipedia.org/wiki/Diff#Unified_format)的差异

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

#### 写入ReplicationPredicateEvaluator {#writing-the-replicationpredicateevaluator}

`cq-search`项目包含`AbstractPredicateEvaluator`抽象类。 可以通过几个步骤扩展该功能，以实现您自己的自定义谓词计算器`(PredicateEvaluator`)。

>[!NOTE]
>
>以下过程说明了如何构建`Xpath`表达式来筛选数据。 另一个选项是实现`includes`方法，该方法以行为基础选择数据。 有关详细信息，请参阅[Java文档](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/search/eval/PredicateEvaluator.html)。

1. 创建扩展`com.day.cq.search.eval.AbstractPredicateEvaluator`的新Java类
1. 使用[统一diff格式](https://en.wikipedia.org/wiki/Diff#Unified_format)中显示的类似代码片段注释类`@Component`

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
   >`factory`必须是以`com.day.cq.search.eval.PredicateEvaluator/`开头并以自定义`PredicateEvaluator`的名称结尾的唯一字符串。

   >[!NOTE]
   >
   >`PredicateEvaluator`的名称是谓词名称，在生成查询时使用。

1. 替代:

   ```java
   public String getXPathExpression(Predicate predicate, EvaluationContext context)
   ```

   在覆盖方法中，根据参数中给定的`Predicate`构建`Xpath`表达式。

### 复制元数据{#example-of-a-custom-predicate-evaluator-for-replication-metadata}的自定义谓词计算器示例

此`PredicateEvaluator`的完整实现可能类似于以下类。

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
