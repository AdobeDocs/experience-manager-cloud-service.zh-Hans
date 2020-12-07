---
title: 索引转换器
description: 索引转换器
translation-type: tm+mt
source-git-commit: 21bd9392d913369a5e8e0ebd9badbbe30fd4bba3
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 0%

---


# 索引转换器{#index-converter}

Index Converter是为迁移客户的索引定义而开发的实用程序，为迁移到AEM作为Cloud Service做准备。

## 简介 {#introduction}

索引转换器允许AEM开发人员将现有的自定义Oak索引定义迁移到AEM，作为Cloud Service兼容的自定义Oak索引定义。

>[!NOTE]
>索引转换器仅转换&#x200B;*lucene*&#x200B;类型自定义Oak索引定义，这些定义位于`/apps`或`/oak:index`下。 它不转换为`nt:base`创建的&#x200B;*lucene*&#x200B;类型索引。

## 使用索引转换器{#using-index-converter}

请参阅&#x200B;**[Git资源：aem-cs-source-migration-index-converter](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration#introduction)**&#x200B;了解如何安装和使用插件。

