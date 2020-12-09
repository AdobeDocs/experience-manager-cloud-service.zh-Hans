---
title: 索引转换器
description: 索引转换器
translation-type: tm+mt
source-git-commit: 1117f03b2eff37f8b25726c3dc60d5a3fe98a5d1
workflow-type: tm+mt
source-wordcount: '279'
ht-degree: 0%

---


# 索引转换器{#index-converter}

Index Converter是为迁移客户的索引定义而开发的实用程序，为迁移到AEM作为Cloud Service做准备。

## 简介 {#introduction}

索引转换器允许AEM开发者将现有的自定义Oak索引定义迁移到AEM作为Cloud Service兼容的自定义Oak索引定义。

>[!NOTE]
>索引转换器仅转换&#x200B;*lucene*&#x200B;类型自定义Oak索引定义，这些定义位于`/apps`或`/oak:index`下。 它不转换为`nt:base`创建的&#x200B;*lucene*&#x200B;类型索引。

有两种方法可创建自定义Oak索引定义：

* `under /apps` （通过任何自定义内容包）
* 位于`/oak:index`路径下

如果使用了[确保Oak Index](https://adobe-consulting-services.github.io/acs-aem-commons/features/ensure-oak-index/index.html)，请注意，AEM上不支持将定义作为Cloud Service，因此需要先将其转换为Oak Index Definitions，然后需要将其迁移到自定义Oak Index Definitions，该Custom Oak Index Definitions与AEM作为Cloud Service兼容，如下所示：

* 如果属性ignore设置为`true`，则忽略或跳过“确保定义”
* 将`jcr:primaryType`更新为`oak:QueryIndexDefinition`
* 删除OSGi配置中提到的要忽略的所有属性
* 从“确保定义”中删除子树`/facets/jcr:content`

## 使用索引转换器{#using-index-converter}

* 通过Adobe I/OCLI:建议通过`aio-cli-plugin-aem-cloud-service-migration`使用索引转换器(AEM作为Adobe I/OCLI的Cloud Service代码重构插件)。

请参阅&#x200B;**[Git资源：aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration#introduction)**&#x200B;了解如何安装和使用插件。

* 作为独立实用程序：索引转换器也可以作为独立实用程序执行。

请参阅&#x200B;**[Git资源：aem-cs-source-migration-index-converter](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/index-converter)**&#x200B;了解如何使用此工具。



