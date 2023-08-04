---
title: 索引转换器
description: 了解如何迁移索引定义，为迁移到AEMas a Cloud Service做准备。
exl-id: ac02ca41-eb35-4f24-bf17-d00ce318423d
source-git-commit: 8c73805b6ed1b7a03c65b4d21a4252c1412a5742
workflow-type: tm+mt
source-wordcount: '290'
ht-degree: 1%

---

# 索引转换器 {#index-converter}

Index Converter是一个实用程序，用于迁移客户的索引定义，为迁移到AEMas a Cloud Service做准备。

## 简介 {#introduction}

索引转换器允许AEM开发人员将现有自定义Oak索引定义迁移到与AEMas a Cloud Service兼容的自定义Oak索引定义。

>[!NOTE]
>仅索引转换器转换 *lucene* 键入Custom Oak Index Definitions，它们位于 `/apps` 或 `/oak:index`. 它不会转换 *lucene* 为创建的类型索引 `nt:base`.

创建自定义Oak索引定义的方法有两种：

* `under /apps` （通过任何自定义内容包）
* 直接在 `/oak:index` 路径

如果 [确保Oak索引](https://adobe-consulting-services.github.io/acs-aem-commons/features/ensure-oak-index/index.html) 使用，请确保AEMas a Cloud Service上不支持定义。 因此，必须首先将它们转换为Oak索引定义，然后迁移到与AEMas a Cloud Service兼容的自定义Oak索引定义，如下面的指南中所述：

* 如果属性忽略设置为 `true`，忽略或跳过确保定义
* 更新 `jcr:primaryType` 到 `oak:QueryIndexDefinition`
* 按照OSGi配置中所述，删除要忽略的任何属性
* 删除子树 `/facets/jcr:content` 从确保定义

## 使用索引转换器 {#using-index-converter}

* 通过Adobe I/OCLI ：建议通过以下方式使用索引转换器： `aio-cli-plugin-aem-cloud-service-migration` (用于Adobe I/OCLI的AEMas a Cloud Service代码重构插件)。

  请参阅 **[Git资源：aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration#introduction)** 了解如何安装和使用该插件。

* 作为独立实用程序：索引转换器也可以作为独立实用程序执行。

  请参阅 **[Git资源：aem-cs-source-migration-index-converter](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/index-converter)** 以了解如何使用此工具。
