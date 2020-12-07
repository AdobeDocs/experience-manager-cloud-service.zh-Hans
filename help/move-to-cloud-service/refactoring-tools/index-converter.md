---
title: 索引转换器
description: 索引转换器
translation-type: tm+mt
source-git-commit: adfc453729b88a9cc457783806eb7b4d69150b21
workflow-type: tm+mt
source-wordcount: '170'
ht-degree: 0%

---


# 索引转换器{#index-converter}

Index Converter是为迁移客户的索引定义而开发的实用程序，为迁移到AEM作为Cloud Service做准备。

## 简介 {#introduction}

索引转换器允许AEM开发人员将现有的自定义Oak索引定义迁移到AEM，作为Cloud Service兼容的自定义Oak索引定义。

>[!NOTE]
>索引转换器仅转换&#x200B;*lucene*&#x200B;类型自定义Oak索引定义，这些定义位于`/apps`或`/oak:index`下。 它不转换为`nt:base`创建的&#x200B;*lucene*&#x200B;类型索引。

有两种方法可创建自定义Oak索引定义：

* `under /apps` （通过任何自定义内容包）
* 位于`/oak:index`路径下

>[!NOTE]
>请参阅[确保Oak Index](https://adobe-consulting-services.github.io/acs-aem-commons/features/ensure-oak-index/index.html)，了解如何定义和创建Oak Definitions

## 使用索引转换器{#using-index-converter}

>[!NOTE]
>尽管建议通过[AIO CLI插件使用索引转换器工具进行源迁移](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration)，但也可以单独执行。

请参阅&#x200B;**[Git资源：aem-cs-source-migration-index-converter](https://git.corp.adobe.com/vavarshn/aem-cloud-service-source-migration/blob/master/packages/index-converter/README.md)**&#x200B;了解如何安装和使用插件。

