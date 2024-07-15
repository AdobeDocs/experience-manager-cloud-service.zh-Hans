---
title: 索引转换器
description: 了解如何迁移索引定义，为迁移到AEM as a Cloud Service做准备。
exl-id: ac02ca41-eb35-4f24-bf17-d00ce318423d
feature: Migration
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 1%

---

# 索引转换器 {#index-converter}

Index Converter是一个实用程序，用于迁移客户的索引定义，为迁移到AEM as a Cloud Service做准备。

## 简介 {#introduction}

索引转换器允许AEM开发人员将现有自定义Oak索引定义迁移到与AEM as a Cloud Service兼容的自定义Oak索引定义。

>[!NOTE]
>索引转换器只转换`/apps`或`/oak:index`下的&#x200B;*lucene*&#x200B;类型自定义Oak索引定义。 它不转换为`nt:base`创建的&#x200B;*lucene*&#x200B;类型索引。

可通过两种方式创建自定义Oak索引定义：

* `under /apps` （通过任何自定义内容包）
* 直接位于`/oak:index`路径下

如果[确保使用了Oak索引](https://adobe-consulting-services.github.io/acs-aem-commons/features/ensure-oak-index/index.html)，请确保AEM as a Cloud Service上不支持定义。 因此，必须首先将它们转换为Oak索引定义，然后迁移到与AEM as a Cloud Service兼容的自定义Oak索引定义，如下面的准则所述：

* 如果属性ignore设置为`true`，请忽略或跳过确保定义
* 将`jcr:primaryType`更新为`oak:QueryIndexDefinition`
* 按照OSGi配置中所述，删除要忽略的任何属性
* 从确保定义中删除子树`/facets/jcr:content`

## 使用索引转换器 {#using-index-converter}

* 通过Adobe I/OCLI ：Adobe建议通过`aio-cli-plugin-aem-cloud-service-migration`的方式使用索引转换器(用于Adobe I/OCLI的AEM as a Cloud Service代码重构插件)。

  请参阅&#x200B;**[Git资源：aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration#introduction)**&#x200B;以了解如何安装和使用插件。

* 作为独立实用程序：索引转换器也可以作为独立实用程序执行。

  请参阅&#x200B;**[Git资源：aem-cs-source-migration-index-converter](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/index-converter)**&#x200B;以了解如何使用此工具。
