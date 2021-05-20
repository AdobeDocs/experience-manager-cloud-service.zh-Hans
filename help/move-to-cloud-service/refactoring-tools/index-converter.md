---
title: 索引转换器
description: 索引转换器
exl-id: e6a3ec6d-cc02-4f5b-8b1d-ea481d6884ca
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '279'
ht-degree: 0%

---

# 索引转换器{#index-converter}

索引转换器是一个实用程序，旨在迁移客户的索引定义，以便为迁移到AEM as aCloud Service做准备。

## 简介 {#introduction}

索引转换器允许AEM开发人员将现有的自定义Oak索引定义作为与自定义Oak索引定义兼容的Cloud Service迁移到AEM。

>[!NOTE]
>索引转换器仅转换&#x200B;*lucene*&#x200B;类型的自定义Oak索引定义，这些定义位于`/apps`或`/oak:index`下。 它不会转换为`nt:base`创建的&#x200B;*lucene*&#x200B;类型索引。

有两种方法可创建自定义Oak索引定义：

* `under /apps` （通过任何自定义内容包）
* `/oak:index`路径下

如果使用了[确保Oak索引](https://adobe-consulting-services.github.io/acs-aem-commons/features/ensure-oak-index/index.html)，请注意确保AEM作为Cloud Service不支持定义，因此需要先将定义转换为Oak索引定义，然后需要迁移到自定义Oak索引定义，这些定义与AEM作为Cloud Service兼容，如下指南所示：

* 如果将属性忽略设置为`true`，则忽略或跳过“确保定义”
* 将`jcr:primaryType`更新为`oak:QueryIndexDefinition`
* 按照OSGi配置中所述，删除要忽略的所有属性
* 从“确保定义”中删除子树`/facets/jcr:content`

## 使用索引转换器{#using-index-converter}

* 通过Adobe I/OCLI :建议通过`aio-cli-plugin-aem-cloud-service-migration`使用索引转换器(将AEM用作Adobe I/OCLI的Cloud Service代码重构插件)。

   请参阅&#x200B;**[Git资源：aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration#introduction)** ，以了解如何安装和使用插件。

* 作为独立实用程序：索引转换器也可以作为独立实用程序执行。

   请参阅&#x200B;**[Git资源：aem-cs-source-migration-index-converter](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/index-converter)**&#x200B;以了解如何使用此工具。
