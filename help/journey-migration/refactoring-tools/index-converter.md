---
title: 索引转换器
description: 索引转换器
exl-id: ac02ca41-eb35-4f24-bf17-d00ce318423d
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '279'
ht-degree: 2%

---

# 索引转换器 {#index-converter}

索引转换器是一个实用程序，旨在迁移客户的索引定义，以便为迁移到AEMas a Cloud Service做准备。

## 简介 {#introduction}

索引转换器允许AEM开发人员将现有的自定义Oak索引定义迁移到与AEMas a Cloud Service兼容的自定义Oak索引定义。

>[!NOTE]
>仅转换索引转换器 *绿色* 类型自定义Oak索引定义，它位于 `/apps` 或 `/oak:index`. 它不会转换 *绿色* 为创建的类型索引 `nt:base`.

有两种方法可创建自定义Oak索引定义：

* `under /apps` （通过任何自定义内容包）
* 直接下 `/oak:index` 路径

如果 [确保Oak索引](https://adobe-consulting-services.github.io/acs-aem-commons/features/ensure-oak-index/index.html) 已使用，请注意，AEMas a Cloud Service不支持“确保定义”，因此需要先将这些定义转换为Oak索引定义，然后再将其迁移到与AEMas a Cloud Service兼容的自定义Oak索引定义，如下所述：

* 如果将属性忽略设置为 `true`，忽略或跳过确保定义
* 更新 `jcr:primaryType` to `oak:QueryIndexDefinition`
* 按照OSGi配置中所述，删除要忽略的所有属性
* 删除子树 `/facets/jcr:content` 从“确保定义”

## 使用索引转换器 {#using-index-converter}

* 通过Adobe I/OCLI :建议通过 `aio-cli-plugin-aem-cloud-service-migration` (AEMas a Cloud Service代码重构插件，用于Adobe I/OCLI)。

   请参阅 **[Git资源：aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration#introduction)** 了解如何安装和使用插件。

* 作为独立实用程序：索引转换器也可以作为独立实用程序执行。

   请参阅 **[Git资源：aem-cs-source-migration-index-converter](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/index-converter)** 了解如何使用此工具。
